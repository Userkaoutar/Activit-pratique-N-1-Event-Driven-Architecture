 Activit-pratique-N-1-Event-Driven-Architecture
##Installation de Kafka
##Téléchargement de Kafka

Pour commencer, téléchargez la dernière version de Kafka depuis le site officiel de Kafka. Dans ce TP, nous utiliserons la version 2.12-2.3.0. Une fois l'archive téléchargée, décompressez-la et accédez au dossier créé.

Lancement de Kafka et Zookeeper
Le fonctionnement de Kafka dépend également du serveur Zookeeper.

Étape 1: Lancement de Zookeeper
Ouvrez un terminal et exécutez la commande suivante pour démarrer le serveur Zookeeper :

```bash

start ./bin/zookeeper-server-start.sh config/zookeeper.properties
```

![image](https://github.com/Userkaoutar/Activit-pratique-N-1-Event-Driven-Architecture/assets/101696114/76c73be1-d1dd-4a58-bf00-8aed66b6c3cc)


Étape 2: Lancement de Kafka
Ouvrez un autre terminal et exécutez la commande suivante pour démarrer le serveur Kafka :

```bash

start./bin/kafka-server-start.sh config/server.properties
```

![image](https://github.com/Userkaoutar/Activit-pratique-N-1-Event-Driven-Architecture/assets/101696114/b1b3468e-fead-4e08-832c-974fac804776)

Conclusion
Une fois ces deux serveurs lancés, votre environnement Kafka devrait être opérationnel. Vous pouvez maintenant commencer à créer des topics, à publier et à consommer des messages. 

1.4 Test avec kafka-console-producer et kafka-console-consumer
Utilisez le kafka-console-producer pour envoyer des messages :

```bash

start bin\windows\kafka-console-producer.bat --broker-list localhost:9092 --topic kaoutar-topic

```

![image](https://github.com/Userkaoutar/Activit-pratique-N-1-Event-Driven-Architecture/assets/101696114/09eabd3e-39ff-483a-82a6-48289c6ba4c7)



Dans un autre terminal, utilisez le kafka-console-consumer pour recevoir les messages :

```bash

start bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic kaoutar-topic --from-beginning


```

![image](https://github.com/Userkaoutar/Activit-pratique-N-1-Event-Driven-Architecture/assets/101696114/0542cf73-6efd-495d-9318-708393c50dc0)


voila:

![image](https://github.com/Userkaoutar/Activit-pratique-N-1-Event-Driven-Architecture/assets/101696114/227368a4-80a1-4e63-b39f-8257af5b836d)


2. Utilisation de Docker
Suivez les étapes ci-dessous pour utiliser Docker avec Kafka.

2.1 Création du fichier docker-compose.yml
Créez un fichier docker-compose.yml avec le contenu suivant :

yaml
Copy code
version: '2'
services:
  zookeeper:
    image: wurstmeister/zookeeper:latest
    ports:
     - "2181:2181"
  kafka:
    image: wurstmeister/kafka:latest
    ports:
     - "9092:9092"
    expose:
     - "9093"
    environment:
      KAFKA_ADVERTISED_LISTENERS: INSIDE://kafka:9093,OUTSIDE://localhost:9092
      KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: INSIDE:PLAINTEXT,OUTSIDE:PLAINTEXT
      KAFKA_LISTENERS: INSIDE://0.0.0.0:9093,OUTSIDE://0.0.0.0:9092
      KAFKA_INTER_BROKER_LISTENER_NAME: INSIDE
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
    volumes:
     - /var/run/docker.sock:/var/run/docker.sock
2.2 Démarrage des conteneurs Docker
Dans le répertoire contenant le fichier docker-compose.yml, exécutez la commande suivante :

bash
Copy code
docker-compose up -d
2.3 Test avec kafka-console-producer et kafka-console-consumer
Utilisez le kafka-console-producer :

bash
Copy code
docker exec -it container_id kafka-console-producer.sh --broker-list localhost:9092 --topic votre_topic
Dans un autre terminal, utilisez le kafka-console-consumer :

bash
Copy code
docker exec -it container_id kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic votre_topic --from-beginning
3. Utilisation de Kafka et Spring Cloud Streams
En utilisant Kafka et Spring Cloud Streams, nous allons créer différents services.

3.1 Service Producer Kafka via un Rest Controller
Créez un service qui produit des messages Kafka via un Rest Controller.

3.2 Service Consumer Kafka
Créez un service qui consomme des messages Kafka.

3.3 Service Supplier Kafka
Créez un service qui agit en tant que fournisseur de données pour Kafka.

3.4 Service de Data Analytics Real-Time Stream Processing avec Kafka Streams
Créez un service qui effectue des analyses en temps réel sur le flux de données Kafka en utilisant Kafka Streams.

3.5 Application Web pour Afficher les Résultats du Stream Data Analytics en Temps Réel
Développez une application web qui affiche les résultats des analyses en temps réel.

Conclusion
Ce guide couvre les bases de l'utilisation de Kafka localement, avec Docker, et son intégration avec Spring Cloud Streams. Vous pouvez maintenant explorer davantage ces technologies
