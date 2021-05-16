# Start zookeeper
zookeeper-server-start.sh config/zookeeper.properties


# Start kafka
kafka-server-start.sh config/server.properties


# Topic
kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic first_topic --create --partitions 3 --replication-factor 1

kafka-topics.sh --zookeeper 127.0.0.1:2181 --list

kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic first_topic --describe

kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic firnew_topic --delete


# Producer
kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic first_topic

kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic first_topic --producer-property acks=all

kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic new_topic


# Consumer
kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic first_topic

kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic first_topic --from-beginning


# Consumer group: consume once and balance load
kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-first-application
kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-first-application


#### Consumer group have offset
#### --from-beginning is valid during group creating only else new group reads new only
kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-second-application --from-beginning
kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-second-application

# Consumer group
kafka-consumer-groups.sh --bootstrap-server 127.0.0.1:9092 --list

kafka-consumer-groups.sh --bootstrap-server 127.0.0.1:9092 --describe --group my-second-application


# Offset
kafka-consumer-group.sh --bootstrap-server 127.0.0.1:9092 --group my-fisrt-application --reset-offsets --to-earliest --execute --topic first_topic


# Producer with key
kafka-console-producer --broker-list 127.0.0.1:9092 --topic first_topic --property parse.key=true --property key.separator=,


# Consumer with key
kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --from-beginning --property print.key=true --property key.separator=,