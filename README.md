# Kafka Docker Python

This script can guide you through setting up a basic kafka producer and consumer in Python, and running them within a docker image.

Project tree:

- docker-kafka-setup
    - kafka-python
        - producers.py
        - consumers.py
        - data_generator.py
    - docker-compose.yml
    - README.md

# 1. Set up docker compose

```yaml
version: '3'

services:
  zookeeper:
    image: wurstmeister/zookeeper
    container_name: zookeeper
    ports:
      - "2181:2181"
  kafka:
    image: wurstmeister/kafka
    container_name: kafka
    ports:
      - "9092:9092"
    environment:
      KAFKA_ADVERTISED_HOST_NAME: localhost
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
```

In WSL2, use the command:

```yaml
docker compose -f docker-compose.yml up -d
```

# 2. Docker CLI

Some CLI to interactive with kafka

docker exec to kafka container:  

`docker exec -it kafka /bin/sh`

Access to kafka folder:

```bash
 /opt/kafka_2.13-2.8.1/bin
```

****Creating a topic****

```bash
kafka-topics.sh --create --zookeeper zookeeper:2181 --replication-factor 1 --partitions 1 --topic message
```

****Listing Kafka topics****

`kafka-topics.sh --list --zookeeper zookeeper:2181`

****Getting details on a Kafka topic****

`kafka-topics.sh --describe --zookeeper zookeeper:2181 --topic messages`

****Deleting a Kafka topic****

`kafka-topics.sh --delete --zookeeper zookeeper:2181 --topic messages`

****Kafka console Producers:****

`kafka-console-producer.sh --broker-list kafka:9092 --topic messages`

**Kafka console Consumers:**

`kafka-console-consumer.sh --bootstrap-server kafka:9092 --topic messages`

# 3. Kafka-Python

**Install kafka-python:**

```bash
pip3 install kafka-python
```

Once the "messages" topic has been created, you can execute

'''bash
python3 consumers.py
'''
'''bash
python3 producers.py
'''

to run the scripts. You might need to navigate into the kafka_python folder to run these commands successfully.

# 4. Reference

The original script for setting up a producer and consumer in python can be found [here](https://github.com/better-data-science/Apache-Kafka-in-Python).

# 5. Getting Stuck?

Try these links.

1: [How to Install Kafka Using Docker](https://betterdatascience.com/how-to-install-apache-kafka-using-docker-the-easy-way/)
2: [Apache Kafka From the Shell](https://betterdatascience.com/master-the-kafka-shell-in-5-minutes-topics-producers-and-consumers-explained/)