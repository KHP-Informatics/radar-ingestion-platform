# radar-ingestion-platform

##Dependencies
- Docker
- Java version >=1.7
- Git

## This package includes
- Shimmer
- Confluent

## Installation

`git clone https://github.com/cbitstech/radar-ingestion-platform`

### Install and start Shimmer

For convenience, this repo includes a copy of the Shimmer stack

For more information on Shimmer or to git a newer version, visit http://www.getshimmer.co/.

Prepare environment variables, replacing host with the IP or domain name of your Docker host.

`eval "$(docker-machine env host)`

If in Docker <=1.4 compose your Docker files using the included shell script

`./shimmer/update-compose-files.sh`

Download and start the containers by running (If you want to see logs and keep the containers in the foreground, omit the -d.)

`shimmer/docker-compose up -d`

###Install and start Confluent platform

For convenience, this repository includes a copy of the current Confluent platform.

For more information on Confluent and its installation, check out http://docs.confluent.io/3.0.0/quickstart.html#quickstart

Start Zookeeper

`./confluent-3.0.0/bin/zookeeper-server-start confluent-3.0.0/etc/kafka/zookeeper.properties`

Start Kafka

`./confluent-3.0.0/bin/kafka-server-start confluent-3.0.0/etc/kafka/server.properties`

Start Schema Registry

`./confluent-3.0.0/bin/schema-registry-start confluent-3.0.0/etc/schema-registry/schema-registry.properties` 

Configure Kafka Connect (create a copy of the default properties file and add monitoring features to Kafka Connect first)

`mkdir cfg`
`cp /confluent-3.0.0/etc/schema-registry/connect-avro-distributed.properties /cfg/connect-distributed.properties`
`echo "" >> /cfg/connect-distributed.properties`
`cat <<EOF >> /cfg/connect-distributed.properties consumer.interceptor.classes=io.confluent.monitoring.clients.interceptor.MonitoringConsumerInterceptor producer.interceptor.classes=io.confluent.monitoring.clients.interceptor.MonitoringProducerInterceptor EOF`

Start Kafka Connect

`./confluent-3.0.0/bin/connect-distributed /cfg/connect-distributed.properties`

Start Confluent Control Center
``

##Usage

###Shimmer
Access your active Shimmer instance at: http://<your-docker-host-ip>:8083


You will need to authorize at least 1 device listed in order to capture data

###Confluent

Add a valid schema to the Schema Registry:

For this case we'll use the op

`./confluent-3.0.0/bin/kafka-avro-console-producer --broker-list localhost:9092 --topic test --property value.schema='{"type":"record","name":"myrecord","fields":[{"name":"f1","type":"string"}]}'`

In this case the object that the schema registry expects requires a key of f1 and a string.
Anything else will throw an error.






