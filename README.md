------------------------------------------------
Séquence 5 : Exercices  
Difficulté : Moyenne (~45 minutes)
---------------------------------------------------
**Complétez et documentez ce fichier README.md** pour répondre aux questions des exercices.  
Faites preuve de pédagogie et soyez clair dans vos explications et procedures de travail.  

**Exercice 1 :**  
Quels sont les composants dont la perte entraîne une perte de données ?  
  
**La perte du pra-data et pra-backup entraine la perte définitive des données.
Si la base est corrompue le backup le sera aussi. Si l'on ne s'en rend pas compte toutes les données peuvent être perdues.
Un problème sur le disque physique qui héberge les données entraîne également la perte des données.**

**Exercice 2 :**  
Expliquez nous pourquoi nous n'avons pas perdu les données lors de la supression du PVC pra-data  
  
**Nous n'avons pas perdu les données grâce à la mise en place de la stratégie de sauvegarde asynchrone.  Le fichier database.sqlite est copié sur pra-backup toute les minutes avec le CronJob. Nous avons ensuite pu le restaurer depuis pra-backup vers pra-data.**

**Exercice 3 :**  
Quels sont les RTO et RPO de cette solution ?  
  
**Le RTO est manuel et dépend donc de l'humain. 
Le RPO est de 1 minute car le CronJob se lance chaque minute.**

**Exercice 4 :**  
Pourquoi cette solution (cet atelier) ne peux pas être utilisé dans un vrai environnement de production ? Que manque-t-il ?   
  
**Les sauvegardes sont au même endroit (même cluster voire même disque). Si un évènement intervient dessus, la production et la backup sont perdus.
Il n'y a pas de monitoring qui alerte en cas d'échec du CronJob.**

  
**Exercice 5 :**  
Proposez une archtecture plus robuste.   
  
**Envoyer les backup vers un stockage externe (par exemple cloud).
Repliquer la base de donnée pour un RPO proche de zéro.
Déployer le cluster sur plusieurs zones de disponibilités pour que le service puisse continuer même si un datacenter tombe en panne.
Mettre en place des tests de restauration automatique pour s'assurer que la procédure mise en place mache bien.**

---------------------------------------------------
Séquence 6 : Ateliers  
Difficulté : Moyenne (~2 heures)
---------------------------------------------------
### **Atelier 1 : Ajoutez une fonctionnalité à votre application**  
**Ajouter une route GET /status** dans votre application qui affiche en JSON :
* count : nombre d’événements en base
* last_backup_file : nom du dernier backup présent dans /backup
* backup_age_seconds : âge du dernier backup

*..**Déposez ici une copie d'écran** de votre réussite..*

---------------------------------------------------
### **Atelier 2 : Choisir notre point de restauration**  
Aujourd’hui nous restaurobs “le dernier backup”. Nous souhaitons **ajouter la capacité de choisir un point de restauration**.

*..Décrir ici votre procédure de restauration (votre runbook)..*  
  
---------------------------------------------------
Evaluation
---------------------------------------------------
Cet atelier PRA PCA, **noté sur 20 points**, est évalué sur la base du barème suivant :  
- Série d'exerices (5 points)
- Atelier N°1 - Ajout d'un fonctionnalité (4 points)
- Atelier N°2 - Choisir son point de restauration (4 points)
- Qualité du Readme (lisibilité, erreur, ...) (3 points)
- Processus travail (quantité de commits, cohérence globale, interventions externes, ...) (4 points) 

