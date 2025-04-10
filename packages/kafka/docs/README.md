# Kafka integration

This integration collects logs and metrics from [Kafka](https://kafka.apache.org) servers.

## Compatibility

The `log` dataset is tested with logs from Kafka 0.9, 1.1.0 and 2.0.0.

The `broker`, `consumergroup`, `partition` datastreams are tested with Kafka 0.10.2.1, 1.1.0, 2.1.1, 2.2.2 and 3.6.0.

The `broker` metricset requires Jolokia to fetch JMX metrics. Refer to the Metricbeat documentation about Jolokia for more information.

## Logs

### log

The `log` dataset collects and parses logs from Kafka servers.

**ECS Field Reference**

Please refer to the following [document](https://www.elastic.co/guide/en/ecs/current/ecs-field-reference.html) for detailed information on ECS fields.

**Exported fields**

| Field | Description | Type |
|---|---|---|
| @timestamp | Event timestamp. | date |
| cloud.image.id | Image ID for the cloud instance. | keyword |
| data_stream.dataset | Data stream dataset. | constant_keyword |
| data_stream.namespace | Data stream namespace. | constant_keyword |
| data_stream.type | Data stream type. | constant_keyword |
| event.dataset | Event dataset | constant_keyword |
| event.module | Event module | constant_keyword |
| host.containerized | If the host is a container. | boolean |
| host.os.build | OS build information. | keyword |
| host.os.codename | OS codename, if any. | keyword |
| kafka.log.class | Java class the log is coming from. | keyword |
| kafka.log.component | Component the log is coming from. | keyword |
| kafka.log.thread | Thread name the log is coming from. | keyword |
| kafka.log.trace.class | Java class the trace is coming from. | keyword |
| kafka.log.trace.message | Message part of the trace. | text |


## Metrics

### broker

The `broker` dataset collects JMX metrics from Kafka brokers using Jolokia.

An example event for `broker` looks as following:

```json
{
    "@timestamp": "2020-05-15T15:12:12.270Z",
    "agent": {
        "ephemeral_id": "178ff0e9-e3dd-4bdf-8e3d-8f67a6bd72ef",
        "id": "5aba67f2-2050-4d19-8953-ba20f0a5483c",
        "name": "kafka-01",
        "type": "metricbeat",
        "version": "8.0.0"
    },
    "ecs": {
        "version": "8.11.0"
    },
    "event": {
        "dataset": "kafka.broker",
        "duration": 4572918,
        "module": "kafka"
    },
    "kafka": {
        "broker": {
            "mbean": "kafka.server:name=BytesOutPerSec,topic=messages,type=BrokerTopicMetrics",
            "topic": {
                "net": {
                    "out": {
                        "bytes_per_sec": 0.6089809926927563
                    }
                }
            }
        }
    },
    "metricset": {
        "name": "broker",
        "period": 10000
    },
    "service": {
        "address": "localhost:8778",
        "type": "kafka"
    }
}
```

**ECS Field Reference**

Please refer to the following [document](https://www.elastic.co/guide/en/ecs/current/ecs-field-reference.html) for detailed information on ECS fields.

**Exported fields**

| Field | Description | Type | Metric Type |
|---|---|---|---|
| @timestamp | Event timestamp. | date |  |
| agent.id |  | keyword |  |
| cloud.account.id | The cloud account or organization id used to identify different entities in a multi-tenant environment.  Examples: AWS account id, Google Cloud ORG Id, or other unique identifier. | keyword |  |
| cloud.availability_zone | Availability zone in which this host is running. | keyword |  |
| cloud.image.id | Image ID for the cloud instance. | keyword |  |
| cloud.instance.id | Instance ID of the host machine. | keyword |  |
| cloud.provider | Name of the cloud provider. Example values are aws, azure, gcp, or digitalocean. | keyword |  |
| cloud.region | Region in which this host is running. | keyword |  |
| container.id | Unique container id. | keyword |  |
| data_stream.dataset | Data stream dataset. | constant_keyword |  |
| data_stream.namespace | Data stream namespace. | constant_keyword |  |
| data_stream.type | Data stream type. | constant_keyword |  |
| event.dataset | Event dataset | constant_keyword |  |
| event.module | Event module | constant_keyword |  |
| host.containerized | If the host is a container. | boolean |  |
| host.name | Name of the host.  It can contain what `hostname` returns on Unix systems, the fully qualified domain name, or a name specified by the user. The sender decides which value to use. | keyword |  |
| host.os.build | OS build information. | keyword |  |
| host.os.codename | OS codename, if any. | keyword |  |
| kafka.broker.address | Broker advertised address | keyword |  |
| kafka.broker.id | Broker id | long |  |
| kafka.broker.log.flush_rate | The log flush rate | float | gauge |
| kafka.broker.mbean | Mbean that this event is related to | keyword |  |
| kafka.broker.messages_in | The incoming message rate | float | gauge |
| kafka.broker.net.in.bytes_per_sec | The incoming byte rate | float | gauge |
| kafka.broker.net.out.bytes_per_sec | The outgoing byte rate | float | gauge |
| kafka.broker.net.rejected.bytes_per_sec | The rejected byte rate | float | gauge |
| kafka.broker.replication.leader_elections | The leader election rate | float | gauge |
| kafka.broker.replication.unclean_leader_elections | The unclean leader election rate | float | gauge |
| kafka.broker.request.channel.queue.size | The size of the request queue | long | gauge |
| kafka.broker.request.fetch.failed | The number of client fetch request failures | float | counter |
| kafka.broker.request.fetch.failed_per_second | The rate of client fetch request failures per second | float | gauge |
| kafka.broker.request.produce.failed | The number of failed produce requests | float | counter |
| kafka.broker.request.produce.failed_per_second | The rate of failed produce requests per second | float | gauge |
| kafka.broker.session.zookeeper.disconnect | The ZooKeeper closed sessions per second | float | gauge |
| kafka.broker.session.zookeeper.expire | The ZooKeeper expired sessions per second | float | gauge |
| kafka.broker.session.zookeeper.readonly | The ZooKeeper readonly sessions per second | float | gauge |
| kafka.broker.session.zookeeper.sync | The ZooKeeper client connections per second | float | gauge |
| kafka.broker.topic.messages_in | The incoming message rate per topic | float | gauge |
| kafka.broker.topic.net.in.bytes_per_sec | The incoming byte rate per topic | float | gauge |
| kafka.broker.topic.net.out.bytes_per_sec | The outgoing byte rate per topic | float | gauge |
| kafka.broker.topic.net.rejected.bytes_per_sec | The rejected byte rate per topic | float | gauge |
| kafka.partition.id | Partition id. | long |  |
| kafka.partition.topic_broker_id | Unique id of the partition in the topic and the broker. | keyword |  |
| kafka.partition.topic_id | Unique id of the partition in the topic. | keyword |  |
| kafka.topic.error.code | Topic error code. | long |  |
| kafka.topic.name | Topic name | keyword |  |
| service.address | Address where data about this service was collected from. This should be a URI, network address (ipv4:port or [ipv6]:port) or a resource path (sockets). | keyword |  |


### consumergroup

An example event for `consumergroup` looks as following:

```json
{
    "@timestamp": "2020-05-15T15:18:13.919Z",
    "agent": {
        "ephemeral_id": "178ff0e9-e3dd-4bdf-8e3d-8f67a6bd72ef",
        "id": "5aba67f2-2050-4d19-8953-ba20f0a5483c",
        "name": "kafka-01",
        "type": "metricbeat",
        "version": "8.0.0"
    },
    "ecs": {
        "version": "8.11.0"
    },
    "event": {
        "dataset": "kafka.consumergroup",
        "duration": 8821045,
        "module": "kafka"
    },
    "kafka": {
        "broker": {
            "address": "kafka-01:9092",
            "id": 0
        },
        "consumergroup": {
            "client": {
                "host": "127.0.0.1",
                "id": "consumer-console-consumer-99447-1",
                "member_id": "consumer-console-consumer-99447-1-208fdf91-2f28-4336-a2ff-5e5f4b8b71e4"
            },
            "consumer_lag": 112,
            "error": {
                "code": 0
            },
            "id": "console-consumer-99447",
            "meta": "",
            "offset": -1
        },
        "partition": {
            "id": 0,
            "topic_id": "0-messages"
        },
        "topic": {
            "name": "messages"
        }
    },
    "metricset": {
        "name": "consumergroup",
        "period": 10000
    },
    "service": {
        "address": "localhost:9092",
        "type": "kafka"
    }
}
```

**ECS Field Reference**

Please refer to the following [document](https://www.elastic.co/guide/en/ecs/current/ecs-field-reference.html) for detailed information on ECS fields.

**Exported fields**

| Field | Description | Type | Metric Type |
|---|---|---|---|
| @timestamp | Event timestamp. | date |  |
| agent.id |  | keyword |  |
| cloud.account.id | The cloud account or organization id used to identify different entities in a multi-tenant environment.  Examples: AWS account id, Google Cloud ORG Id, or other unique identifier. | keyword |  |
| cloud.availability_zone | Availability zone in which this host is running. | keyword |  |
| cloud.image.id | Image ID for the cloud instance. | keyword |  |
| cloud.instance.id | Instance ID of the host machine. | keyword |  |
| cloud.provider | Name of the cloud provider. Example values are aws, azure, gcp, or digitalocean. | keyword |  |
| cloud.region | Region in which this host is running. | keyword |  |
| container.id | Unique container id. | keyword |  |
| data_stream.dataset | Data stream dataset. | constant_keyword |  |
| data_stream.namespace | Data stream namespace. | constant_keyword |  |
| data_stream.type | Data stream type. | constant_keyword |  |
| event.dataset | Event dataset | constant_keyword |  |
| event.module | Event module | constant_keyword |  |
| host.containerized | If the host is a container. | boolean |  |
| host.name | Name of the host.  It can contain what `hostname` returns on Unix systems, the fully qualified domain name, or a name specified by the user. The sender decides which value to use. | keyword |  |
| host.os.build | OS build information. | keyword |  |
| host.os.codename | OS codename, if any. | keyword |  |
| kafka.broker.address | Broker advertised address | keyword |  |
| kafka.broker.id | Broker id | long |  |
| kafka.consumergroup.client.host | Client host | keyword |  |
| kafka.consumergroup.client.id | Client ID (kafka setting client.id) | keyword |  |
| kafka.consumergroup.client.member_id | internal consumer group member ID | keyword |  |
| kafka.consumergroup.consumer_lag | consumer lag for partition/topic calculated as the difference between the partition offset and consumer offset | long | gauge |
| kafka.consumergroup.error.code | kafka consumer/partition error code. | long |  |
| kafka.consumergroup.id | Consumer Group ID | keyword |  |
| kafka.consumergroup.meta | custom consumer meta data string | keyword |  |
| kafka.consumergroup.offset | consumer offset into partition being read | long | gauge |
| kafka.partition.id | Partition id. | long |  |
| kafka.partition.topic_broker_id | Unique id of the partition in the topic and the broker. | keyword |  |
| kafka.partition.topic_id | Unique id of the partition in the topic. | keyword |  |
| kafka.topic.error.code | Topic error code. | long |  |
| kafka.topic.name | Topic name | keyword |  |
| service.address | Address where data about this service was collected from. This should be a URI, network address (ipv4:port or [ipv6]:port) or a resource path (sockets). | keyword |  |


### partition

An example event for `partition` looks as following:

```json
{
    "@timestamp": "2020-05-15T15:19:44.240Z",
    "agent": {
        "ephemeral_id": "178ff0e9-e3dd-4bdf-8e3d-8f67a6bd72ef",
        "id": "5aba67f2-2050-4d19-8953-ba20f0a5483c",
        "name": "kafka-01",
        "type": "metricbeat",
        "version": "8.0.0"
    },
    "ecs": {
        "version": "8.11.0"
    },
    "event": {
        "dataset": "kafka.partition",
        "duration": 11263377,
        "module": "kafka"
    },
    "kafka": {
        "broker": {
            "address": "kafka-01:9092",
            "id": 0
        },
        "partition": {
            "id": 0,
            "offset": {
                "newest": 111,
                "oldest": 0
            },
            "partition": {
                "insync_replica": true,
                "is_leader": true,
                "leader": 0,
                "replica": 0
            },
            "topic_broker_id": "0-messages-0",
            "topic_id": "0-messages"
        },
        "topic": {
            "name": "messages"
        }
    },
    "metricset": {
        "name": "partition",
        "period": 10000
    },
    "service": {
        "address": "localhost:9092",
        "type": "kafka"
    }
}
```

**ECS Field Reference**

Please refer to the following [document](https://www.elastic.co/guide/en/ecs/current/ecs-field-reference.html) for detailed information on ECS fields.

**Exported fields**

| Field | Description | Type | Metric Type |
|---|---|---|---|
| @timestamp | Event timestamp. | date |  |
| agent.id |  | keyword |  |
| cloud.account.id | The cloud account or organization id used to identify different entities in a multi-tenant environment.  Examples: AWS account id, Google Cloud ORG Id, or other unique identifier. | keyword |  |
| cloud.availability_zone | Availability zone in which this host is running. | keyword |  |
| cloud.image.id | Image ID for the cloud instance. | keyword |  |
| cloud.instance.id | Instance ID of the host machine. | keyword |  |
| cloud.provider | Name of the cloud provider. Example values are aws, azure, gcp, or digitalocean. | keyword |  |
| cloud.region | Region in which this host is running. | keyword |  |
| container.id | Unique container id. | keyword |  |
| data_stream.dataset | Data stream dataset. | constant_keyword |  |
| data_stream.namespace | Data stream namespace. | constant_keyword |  |
| data_stream.type | Data stream type. | constant_keyword |  |
| event.dataset | Event dataset | constant_keyword |  |
| event.module | Event module | constant_keyword |  |
| host.containerized | If the host is a container. | boolean |  |
| host.name | Name of the host.  It can contain what `hostname` returns on Unix systems, the fully qualified domain name, or a name specified by the user. The sender decides which value to use. | keyword |  |
| host.os.build | OS build information. | keyword |  |
| host.os.codename | OS codename, if any. | keyword |  |
| kafka.broker.address | Broker advertised address | keyword |  |
| kafka.broker.id | Broker id | long |  |
| kafka.partition.id | Partition id. | long |  |
| kafka.partition.offset.newest | Newest offset of the partition. | long | gauge |
| kafka.partition.offset.oldest | Oldest offset of the partition. | long | gauge |
| kafka.partition.partition.error.code | Error code from fetching partition. | long |  |
| kafka.partition.partition.insync_replica | Indicates if replica is included in the in-sync replicate set (ISR). | boolean |  |
| kafka.partition.partition.is_leader | Indicates if replica is the leader | boolean |  |
| kafka.partition.partition.leader | Leader id (broker). | long |  |
| kafka.partition.partition.replica | Replica id (broker). | long |  |
| kafka.partition.topic_broker_id | Unique id of the partition in the topic and the broker. | keyword |  |
| kafka.partition.topic_id | Unique id of the partition in the topic. | keyword |  |
| kafka.topic.error.code | Topic error code. | long |  |
| kafka.topic.name | Topic name | keyword |  |
| service.address | Address where data about this service was collected from. This should be a URI, network address (ipv4:port or [ipv6]:port) or a resource path (sockets). | keyword |  |


### consumer

The `consumer` dataset collects JMX metrics from Kafka consumers using Jolokia.

An example event for `consumer` looks as following:

```json
{
    "@timestamp": "2024-11-26T05:51:59.816Z",
    "agent": {
        "ephemeral_id": "f45cfc11-360f-4f24-8fe1-68b586fd9e1f",
        "id": "fd4ec33d-d5ff-483b-aa6e-e08f8d0210f5",
        "name": "EPINPUNW06A8",
        "type": "metricbeat",
        "version": "8.15.4"
    },
    "ecs": {
        "version": "8.0.0"
    },
    "event": {
        "agent_id_status": "verified",
        "dataset": "kafka.consumer",
        "duration": 4557113,
        "ingested": "2024-11-26T05:51:59Z",
        "module": "kafka"
    },
    "kafka": {
        "consumer": {
            "bytes_consumed": 83,
            "fetch_rate": 2.0042522,
            "mbean": "kafka.consumer:client-id=console-consumer,type=consumer-fetch-manager-metrics",
            "records_consumed": 4
        }
    },
    "metricset": {
        "name": "consumer",
        "period": 10000
    },
    "service": {
        "address": "http://127.0.0.1:8774/jolokia/",
        "type": "kafka"
    }
}
```

**ECS Field Reference**

Please refer to the following [document](https://www.elastic.co/guide/en/ecs/current/ecs-field-reference.html) for detailed information on ECS fields.

**Exported fields**

| Field | Description | Type |
|---|---|---|
| @timestamp | Event timestamp. | date |
| agent.id |  | keyword |
| cloud.account.id | The cloud account or organization id used to identify different entities in a multi-tenant environment.  Examples: AWS account id, Google Cloud ORG Id, or other unique identifier. | keyword |
| cloud.availability_zone | Availability zone in which this host is running. | keyword |
| cloud.image.id | Image ID for the cloud instance. | keyword |
| cloud.instance.id | Instance ID of the host machine. | keyword |
| cloud.provider | Name of the cloud provider. Example values are aws, azure, gcp, or digitalocean. | keyword |
| cloud.region | Region in which this host is running. | keyword |
| container.id | Unique container id. | keyword |
| data_stream.dataset | Data stream dataset. | constant_keyword |
| data_stream.namespace | Data stream namespace. | constant_keyword |
| data_stream.type | Data stream type. | constant_keyword |
| event.dataset | Event dataset | constant_keyword |
| event.module | Event module | constant_keyword |
| host.containerized | If the host is a container. | boolean |
| host.name | Name of the host.  It can contain what `hostname` returns on Unix systems, the fully qualified domain name, or a name specified by the user. The sender decides which value to use. | keyword |
| host.os.build | OS build information. | keyword |
| host.os.codename | OS codename, if any. | keyword |
| kafka.broker.address | Broker advertised address | keyword |
| kafka.broker.id | Broker id | long |
| kafka.consumer.bytes_consumed | The average number of bytes consumed for a specific topic per second | float |
| kafka.consumer.fetch_rate | The minimum rate at which the consumer sends fetch requests to a broker | float |
| kafka.consumer.in.bytes_per_sec | The rate of bytes coming in to the consumer | float |
| kafka.consumer.kafka_commits | The rate of offset commits to Kafka | float |
| kafka.consumer.max_lag | The maximum consumer lag | float |
| kafka.consumer.mbean | Mbean that this event is related to | keyword |
| kafka.consumer.messages_in | The rate of consumer message consumption | float |
| kafka.consumer.records_consumed | The average number of records consumed per second for a specific topic | float |
| kafka.consumer.zookeeper_commits | The rate of offset commits to ZooKeeper | float |
| kafka.partition.id | Partition id. | long |
| kafka.partition.topic_broker_id | Unique id of the partition in the topic and the broker. | keyword |
| kafka.partition.topic_id | Unique id of the partition in the topic. | keyword |
| kafka.topic.error.code | Topic error code. | long |
| kafka.topic.name | Topic name | keyword |
| service.address | Address where data about this service was collected from. This should be a URI, network address (ipv4:port or [ipv6]:port) or a resource path (sockets). | keyword |


### producer

The `producer` dataset collects JMX metrics from Kafka producers using Jolokia.

An example event for `producer` looks as following:

```json
{
    "@timestamp": "2024-11-26T05:49:08.893Z",
    "agent": {
        "ephemeral_id": "f45cfc11-360f-4f24-8fe1-68b586fd9e1f",
        "id": "fd4ec33d-d5ff-483b-aa6e-e08f8d0210f5",
        "name": "EPINPUNW06A8",
        "type": "metricbeat",
        "version": "8.15.4"
    },
    "ecs": {
        "version": "8.0.0"
    },
    "event": {
        "agent_id_status": "verified",
        "dataset": "kafka.producer",
        "duration": 3162940,
        "ingested": "2024-11-26T05:49:09Z",
        "module": "kafka"
    },
    "kafka": {
        "producer": {
            "available_buffer_bytes": 33554432,
            "batch_size_avg": 83,
            "batch_size_max": 84,
            "io_wait": 1271956426,
            "mbean": "kafka.producer:client-id=console-producer,type=producer-metrics",
            "record_error_rate": 0,
            "record_retry_rate": 0,
            "record_send_rate": 0,
            "record_size_avg": 100,
            "record_size_max": 101,
            "records_per_request": 1,
            "request_rate": 0,
            "response_rate": 0
        }
    },
    "metricset": {
        "name": "producer",
        "period": 10000
    },
    "service": {
        "address": "http://127.0.0.1:8775/jolokia/",
        "type": "kafka"
    }
}
```

**ECS Field Reference**

Please refer to the following [document](https://www.elastic.co/guide/en/ecs/current/ecs-field-reference.html) for detailed information on ECS fields.

**Exported fields**

| Field | Description | Type |
|---|---|---|
| @timestamp | Event timestamp. | date |
| agent.id |  | keyword |
| cloud.account.id | The cloud account or organization id used to identify different entities in a multi-tenant environment.  Examples: AWS account id, Google Cloud ORG Id, or other unique identifier. | keyword |
| cloud.availability_zone | Availability zone in which this host is running. | keyword |
| cloud.image.id | Image ID for the cloud instance. | keyword |
| cloud.instance.id | Instance ID of the host machine. | keyword |
| cloud.provider | Name of the cloud provider. Example values are aws, azure, gcp, or digitalocean. | keyword |
| cloud.region | Region in which this host is running. | keyword |
| container.id | Unique container id. | keyword |
| data_stream.dataset | Data stream dataset. | constant_keyword |
| data_stream.namespace | Data stream namespace. | constant_keyword |
| data_stream.type | Data stream type. | constant_keyword |
| event.dataset | Event dataset | constant_keyword |
| event.module | Event module | constant_keyword |
| host.containerized | If the host is a container. | boolean |
| host.name | Name of the host.  It can contain what `hostname` returns on Unix systems, the fully qualified domain name, or a name specified by the user. The sender decides which value to use. | keyword |
| host.os.build | OS build information. | keyword |
| host.os.codename | OS codename, if any. | keyword |
| kafka.broker.address | Broker advertised address | keyword |
| kafka.broker.id | Broker id | long |
| kafka.partition.id | Partition id. | long |
| kafka.partition.topic_broker_id | Unique id of the partition in the topic and the broker. | keyword |
| kafka.partition.topic_id | Unique id of the partition in the topic. | keyword |
| kafka.producer.available_buffer_bytes | The total amount of buffer memory | float |
| kafka.producer.batch_size_avg | The average number of bytes sent | float |
| kafka.producer.batch_size_max | The maximum number of bytes sent | long |
| kafka.producer.io_wait | The producer I/O wait time | float |
| kafka.producer.mbean | Mbean that this event is related to | keyword |
| kafka.producer.message_rate | The producer message rate | float |
| kafka.producer.out.bytes_per_sec | The rate of bytes going out for the producer | float |
| kafka.producer.record_error_rate | The average number of retried record sends per second | float |
| kafka.producer.record_retry_rate | The average number of retried record sends per second | float |
| kafka.producer.record_send_rate | The average number of records sent per second | float |
| kafka.producer.record_size_avg | The average record size | float |
| kafka.producer.record_size_max | The maximum record size | long |
| kafka.producer.records_per_request | The average number of records sent per second | float |
| kafka.producer.request_rate | The number of producer requests per second | float |
| kafka.producer.response_rate | The number of producer responses per second | float |
| kafka.topic.error.code | Topic error code. | long |
| kafka.topic.name | Topic name | keyword |
| service.address | Address where data about this service was collected from. This should be a URI, network address (ipv4:port or [ipv6]:port) or a resource path (sockets). | keyword |
