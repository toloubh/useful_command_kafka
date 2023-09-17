# useful_command_kafka

1. Create a Topic
```
/opt/kafka/bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --topic topicname --partitions 10 --replication-factor 1 --config retention.ms=180000
```
2. List existing topics
```
/opt/kafka/bin/kafka-topics.sh --bootstrap-server localhost:9092 --list
```
3. Describe a topic
```
/opt/kafka/bin/kafka-topics.sh --bootstrap-server localhost:9092 --describe --topic mytopic 
```
4. Purge a topic
```
/opt/kafka/bin/kafka-topics.sh --bootstrap-server localhost:9092 --alter --topic mytopic --config retention.ms=1000

... wait a minute ...

/opt/kafka/bin/kafka-topics.sh --bootstrap-server localhost:9092 --alter --topic mytopic --delete-config retention.ms
```
5. Alter the Topic Retention
```
/opt/kafka/bin/kafka-configs.sh --alter --bootstrap-server localhost:9092 --add-config retention.ms=1800000 --entity-type topics --entity-name topicname

Completed Updating config for entity: topic ‘topicname’.
```
6. Delete a topic
```
/opt/kafka/bin/kafka-configs.sh --alter --bootstrap-server localhost:9092 --delete --topic mytopic
```
7. Get number of messages in a topic
```
/opt/kafka/bin/kafka-run-class.sh kafka.tools.GetOffsetShell --broker-list localhost:9092 --topic topicname --time -1 --offsets 1 | awk -F  ":" '{sum += $3} END {print sum}'
```
8. Get the earliest offset still in a topic
```
/opt/kafka/bin/kafka-run-class.sh kafka.tools.GetOffsetShell --broker-list localhost:9092 --topic mytopic --time -2
```
9. Get the latest offset still in a topic
```
/opt/kafka/bin/kafka-run-class.sh kafka.tools.GetOffsetShell --broker-list localhost:9092 --topic mytopic --time -1
```
10. Consume messages with the console consumer
```
/opt/kafka/bin/kafka-console-consumer.sh --new-consumer --bootstrap-server localhost:9092 --topic mytopic --from-beginning
```
11. Get the consumer offsets for a topic
```
/opt/kafka/bin/kafka-consumer-offset-checker.sh --bootstrap-server localhost:9092 --topic=mytopic --group=my_consumer_group
```
12. Read from __consumer_offsets
```
Add the following property to config/consumer.properties: exclude.internal.topics=false

/opt/kafka/bin/kafka-console-consumer.sh --consumer.config config/consumer.properties --from-beginning --topic __consumer_offsets --bootstrap-server localhost:9092 --formatter "kafka.coordinator.GroupMetadataManager\$OffsetsMessageFormatter"
```
13. Kafka Consumer Groups
List the consumer groups known to Kafka
```
/opt/kafka/bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --list (old api)

/opt/kafka/bin/kafka-consumer-groups.sh --new-consumer --bootstrap-server localhost:9092 --list (new api)
```
14. View the details of a consumer group
```
/opt/kafka/bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --describe --group <group name>
```
15. kafkacat
Getting the last five message of a topic
```
kafkacat -C -b localhost:9092 -t mytopic -p 0 -o -5 -e
```
16. Zookeeper
Starting the Zookeeper Shell
```
bin/zookeeper-shell.sh localhost:2181
```
