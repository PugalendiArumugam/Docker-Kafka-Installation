Docker Kafka
===============
Create a folder KAFKA-DOCKER 
And open vs code

Create yml file with docker-compose.yaml
version: "4"
services:
  kafka:
    image: bitnami/kafka
    container_name: kafka
    ports:
      - 9092:9092

    environment:
      - KAFKA_ENABLE_KRAFT=yes
      - KAFKA_CFG_PROCESS_ROLES=broker,controller
      - KAFKA_CFG_CONTROLLER_LISTENER_NAMES=CONTROLLER
      - KAFKA_CFG_LISTENERS=PLAINTEXT://:9092,CONTROLLER://:2181
      - KAFKA_CFG_LISTENER_SECURITY_PROTOCOL_MAP=CONTROLLER:PLAINTEXT,PLAINTEXT:PLAINTEXT
      - KAFKA_CFG_ADVERTISED_LISTENERS=PLAINTEXT://127.0.0.1:9092
      - KAFKA_BROKER_ID=1
      - KAFKA_CFG_CONTROLLER_QUORUM_VOTERS=1@127.0.0.1:2181
      - ALLOW_PLAINTEXT_LISTENER=yes
      - KAFKA_CFG_NODE_ID=1
      - KAFKA_KRAFT_CLUSTER_ID=MkU3OEVBNTcwNTJENDM2Qk
    volumes:
      - ./kafka:/bitnami/kafka


Run Kafka image

Go to KAFKA-DOCKER folder

docker compose -f docker-compose.yaml up -d

Check the images

docker images

bitnami/kafka        latest    f45d5b813412   5 days ago     713MB
tensorflow/serving   nightly   6d9608df490d   3 weeks ago    994MB
hello-world          latest    940c619fbd41   6 months ago   20.4kB
primeimages/rust     1.52.1    4c5139765451   4 years ago    1.6GB
primeimages/rust     latest    4c5139765451   4 years ago    1.6GB

Check the running images
 
docker ps

CONTAINER ID   IMAGE           COMMAND                  CREATED             STATUS          PORTS                                         NAMES
6f6a972b329a   bitnami/kafka   "/opt/bitnami/script…"   About an hour ago   Up 29 minutes   0.0.0.0:9092->9092/tcp, [::]:9092->9092/tcp   kafka

docker rmi 4c5139765451 -f. (Force the image to delete)


To run the Producer and to send message

docker exec -it kafka /bin/sh.  (It integrated terminal)

cd opt/bitnami/kafka/bin

$ kafka-console-producer.sh --topic topic1 --bootstrap-server localhost:9092
>How are you?


To run Consumer

KAFKA-DOCKER

docker exec -it kafka /bin/sh

cd opt/bitnami/kafka/bin

kafka-console-consumer.sh --topic topic1 --bootstrap-server localhost:9092

