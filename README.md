# Projet-web-scraping-abdessamad

Le projet décrit est une initiative de collecte et d'analyse de données météorologiques pour les villes de France en utilisant l'API OpenWeather. Les données sont ensuite stockées dans une base de données Cassandra. En plus de la collecte de données, une API Flask est mise en place pour permettre la récupération des informations météorologiques depuis la base de données.


# Les composants clés du projet incluent :

Base de données Cassandra : Une base de données NoSQL utilisée pour stocker les données météorologiques collectées.
Service de Crawling : Un service écrit en Python qui récupère les données de l'API OpenWeather et les insère dans la base de données Cassandra.
Service Flask-API : Un service Python qui extrait les données météorologiques de la base de données Cassandra et répond aux requêtes API.
Docker Compose : Utilisé pour orchestrer la communication entre la base de données Cassandra et le service de Crawling.
Dockerfiles : Des fichiers de configuration pour créer des conteneurs Docker pour Cassandra et le service de Crawling.
Prérequis :
Docker et Docker Compose.
Configuration de Cassandra :
Cassandra est conteneurisée avec l'image Docker officielle, configurée pour fonctionner sur le port 9042 et accessible via le nom d'hôte 'cassandra' dans le réseau Docker. Un mécanisme de vérification de l'état de santé s'assure que la base de données est prête avant de commencer le Crawling.
Initialisation de Cassandra :
Le script init_db.py est crucial pour créer l'espace de clés et les tables de la base de données. Après configuration, un espace de clés weather_db et une table weather_table sont créés, avec des champs pour les paramètres météorologiques comme la température et l'humidité.
Service de Crawling :
Le fichier Dockerfile du répertoire 'crawler' conteneurise le service de Crawling avec une image Python 3.6-slim. Le script crawler.py gère la récupération et l'insertion des données météorologiques en utilisant des fonctions pour récupérer les données, filtrer les villes françaises et écrire dans Cassandra. Les 100 premiers enregistrements sont traités et stockés.
Service Flask-API :
Conteneurisé de manière similaire au service de Crawling, il attend la fin du Crawling pour éviter les problèmes de connexion. Le script main.py dans le dossier 'flask-api' établit l'API pour récupérer des données météorologiques spécifiques à partir de la base de données.
Exécution :
Pour lancer le projet, on utilise la commande docker-compose up dans le répertoire du projet pour démarrer les services nécessaires.


Le projet a donc pour objectif la mise en œuvre d'une infrastructure automatisée pour l'exploration de données météorologiques avec une facilité d'accès via une API Flask, le tout encapsulé dans des conteneurs Docker pour une intégration et un déploiement simplifiés.
