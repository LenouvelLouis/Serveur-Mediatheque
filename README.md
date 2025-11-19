# Serveur Médiathèque

Application client serveur en Java pour gérer une médiathèque simple (abonnés et documents) avec persistance des données dans une base MySQL.

Ce projet a été réalisé dans le cadre d’un travail d’architecture logicielle.  
Il illustre la séparation des responsabilités entre :

- un **serveur** de médiathèque (logique métier, accès base de données)
- un **client** Java (interface console simple)
- une **base de données** MySQL (abonnés, documents, emprunts)

---

## 🧩 Fonctionnalités principales

- Gestion des **abonnés** :
  - Enregistrement des abonnés (nom, date de naissance)
  - Gestion des abonnés bannis (`AbonneBanisException`)
- Gestion des **documents** :
  - Stockage des documents (table `document`)
  - Différenciation documents **adultes** / tous publics
  - Association éventuelle à un emprunteur (`Emprunteur`)
- Règles métier :
  - Vérification des **restrictions d’âge** (`RestrictionException`)
  - Gestion concurrente de l’accès aux documents (`ConcurrentDocument`)
- Persistance :
  - Base MySQL décrite dans le fichier `mediatheque.sql`
  - Données d’exemple déjà fournies (abonnés + documents)

---

## 🏗 Architecture du projet

```text
Serveur-Mediatheque/
├── Client/                     # Projet client (Eclipse)
│   ├── src/Client/Client.java  # Point d'entrée côté client
│   └── bin/                    # .class générés par Eclipse
│
├── bin/                        # .class côté serveur
│   ├── documentAbstract/       # Classes métier de base (Document, ConcurrentDocument, …)
│   └── mediatheque/            # Classes liées aux abonnés, exceptions, interfaces, …
│
├── jar/                        # Dépendances Java
│   ├── activation-1.0.2.jar
│   ├── bserveur.jar
│   ├── bttp.jar
│   ├── javax.mail.jar
│   └── mysql-connector-j-8.0.31.jar
│
├── mediatheque.sql             # Script SQL de création et remplissage de la base MySQL
├── Rapport Archi Logicielle.pdf# Rapport de conception (architecture logicielle)
└── readMe.txt                  # Ancien mini-readme d'origine
```
## 🧱 Base de données

Le script mediatheque.sql contient :

La création de la base et des tables principales :

 - abonne : informations sur les abonnés (id, nom, dateNaissance)
 - document : documents de la médiathèque (id, titre, adulte, Emprunteur)
 - Des données de test (abonnés et documents pré-remplis)

Pour initialiser la base :

1. Créer une base, par exemple mediatheque, dans MySQL.

2. Importer le fichier mediatheque.sql via phpMyAdmin ou la ligne de commande :
```
mysql -u <user> -p mediatheque < mediatheque.sql
```

## 🛠 Prérequis

 - Java (JDK 8 ou supérieur recommandé)
 - MySQL 8.x
 - (Optionnel) Eclipse ou un autre IDE Java si tu veux ouvrir le projet client
