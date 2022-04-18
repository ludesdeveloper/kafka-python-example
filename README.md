# PYTHON KAFKA EXAMPLE
### **Requirements**
1. Java version 8+ installed
2. Python3 installed
### **Step by Step**
1. Create new directory
```
mkdir learn-python-kafka
```
2. Change directory
```
cd learn-python-kafka
```
3. Download kafka
```
wget https://dlcdn.apache.org/kafka/3.1.0/kafka_2.13-3.1.0.tgz
```
4. Untar kafka
```
tar -xzf kafka_2.13-3.1.0.tgz
```
5. Open server.properties with vim
```
vim kafka_2.13-3.1.0/config/server.properties
```
6. Update server.properties
```
#listeners=PLAINTEXT://:9092
#advertised.listeners=PLAINTEXT://your.host.name:9092
```
to
```
listeners=PLAINTEXT://:9092
advertised.listeners=PLAINTEXT://:9092
```
> So far, this is working config for kafka
7. Run the following commands in order to start all services in the correct order inside kafka_2.13-3.1.0 folder
```
bin/zookeeper-server-start.sh config/zookeeper.properties
```
8. Open another terminal session and run inside kafka_2.13-3.1.0 folder
```
bin/kafka-server-start.sh config/server.properties
```
9. Install kafka-python
```
pip install kafka-python
```
9. Create consumer.py file
```
from kafka import KafkaConsumer

TOPIC_NAME = 'items'

consumer = KafkaConsumer(TOPIC_NAME)
for message in consumer:
    print(message)
```
10. Create producer.py file
```
from kafka import KafkaProducer

TOPIC_NAME = "items"
KAFKA_SERVER = "localhost:9092"

producer = KafkaProducer(bootstrap_servers=KAFKA_SERVER)

producer.send(TOPIC_NAME, b'Test Message')
producer.flush()
```
11. Run consumer.py in new terminal
12. Run producer.py in new terminal
13. Take a look consumer.py terminal, you'll look output like this
```
ConsumerRecord(topic='items', partition=0, offset=0, timestamp=1650308405263, timestamp_type=0, key=None, value=b'Test Message', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=12, serialized_header_size=-1)
```