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
   
<img width="928" alt="image" src="https://github.com/Userkaoutar/Activit-pratique-N-1-Event-Driven-Architecture/assets/101696114/18d59b7d-d824-4318-b50f-610d27258b20">


2.1 Création du fichier docker-compose.yml
Créez un fichier docker-compose.yml avec le contenu suivant :
```bash
version: '3'
services:
  zookeeper:
    image: confluentinc/cp-zookeeper:7.3.0
    container_name: zookeeper
    environment:
      ZOOKEEPER_CLIENT_PORT: 2181
      ZOOKEEPER_TICK_TIME: 2000

  broker:
    image: confluentinc/cp-kafka:7.3.0
    container_name: broker
    ports:
      - "9092:9092"
    depends_on:
      - zookeeper
    environment:
      KAFKA_BROKER_ID: 1
      KAFKA_ZOOKEEPER_CONNECT: 'zookeeper:2181'
      KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: PLAINTEXT:PLAINTEXT,PLAINTEXT_INTERNAL:PLAINTEXT
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://localhost:9092,PLAINTEXT_INTERNAL://broker:29092
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1
      KAFKA_TRANSACTION_STATE_LOG_MIN_ISR: 1
      KAFKA_TRANSACTION_STATE_LOG_REPLICATION_FACTOR: 1
```

Démarrer les conteneurs docker : zookeeper et kafka-broker:
```bash
docker-compose up

```

<img width="646" alt="image" src="https://github.com/Userkaoutar/Activit-pratique-N-1-Event-Driven-Architecture/assets/101696114/0ea26528-f1e8-4e97-9e63-5b345306afc0">


<img width="666" alt="image" src="https://github.com/Userkaoutar/Activit-pratique-N-1-Event-Driven-Architecture/assets/101696114/4e78dfcf-eec3-446f-8acb-1d8c75bb1437">


2.2 Démarrage des conteneurs Docker
Dans le répertoire contenant le fichier docker-compose.yml, exécutez la commande suivante :

bash
Copy code
docker-compose up -d
2.3 Test avec kafka-console-producer et kafka-console-consumer
Utilisez le kafka-console-producer :

![Capture d'écran 2023-12-28 160859](https://github.com/Userkaoutar/Activit-pratique-N-1-Event-Driven-Architecture/assets/101696114/2d35b236-d020-472b-a2d0-2d74672a4363)



Conclusion
Ce guide couvre les bases de l'utilisation de Kafka localement, avec Docker, et son intégration avec Spring Cloud Streams. Vous pouvez maintenant explorer davantage ces technologies
