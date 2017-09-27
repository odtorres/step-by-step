# Run
1 bin\windows\zookeeper-server-start.bat config\zookeeper.properties
2 bin\windows\kafka-server-start.bat config\server.properties


# create a topic
bin\windows\kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic topic1

# list topics 
./bin/kafka-topics.sh --list --zookeeper localhost:2181

# remove a topic
1. edit ${kafka_home}/config/server.properties
2. delete.topic.enable=true
bin/kafka-topics.sh --zookeeper 127.0.0.1:2181 --delete --topic crawler-topic

# read
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning

# write
> bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test
This is a message 

## demonio

### start-zookeeper.sh
#!/bin/bash
bin/zookeeper-server-start.sh config/zookeeper.properties

### stop-zookeeper.sh
#!/bin/bash
bin/zookeeper-server-stop config/zookeeper.properties

### start-kafka.sh
#!/bin/bash
bin/kafka-server-start.sh config/server.properties

### stop-kafka.sh
#!/bin/bash
bin/kafka-server-stop.sh config/server.properties

### zookeeper.service

[Unit]
Description=Zookeeper Service
After=network.target

[Service]
#EnvironmentFile=/home/summary-site/summary-site-service/conf/env
WorkingDirectory=/opt/Kafka
ExecStart=/opt/Kafka/start-zookeeper.sh
ExecStop=/opt/Kafka/stop-zookeeper.sh

Restart=on-failure
User=ubuntu
Group=ubuntu

# See http://serverfault.com/a/695863
SuccessExitStatus=143

[Install]
WantedBy=multi-user.target

### kafka.service

[Unit]
Description=Kafka Service
After=network.target

[Service]
#EnvironmentFile=/home/summary-site/summary-site-service/conf/env
WorkingDirectory=/opt/Kafka
ExecStart=/opt/Kafka/start-kafka.sh
ExecStop=/opt/Kafka/stop-kafka.sh

Restart=on-failure
User=ubuntu
Group=ubuntu

# See http://serverfault.com/a/695863
SuccessExitStatus=143

[Install]
WantedBy=multi-user.target


##