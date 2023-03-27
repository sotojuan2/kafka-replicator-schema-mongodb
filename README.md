# Replicator Schema demo

## Proposal

Confirm the connect.name forces the replicated namespace in the destination schema.

## Running the demo

```shell
    ./start-cluster.sh
```

Then add some content

```shell
docker-compose exec srcSchemaregistry kafka-avro-console-producer --broker-list srcKafka:19092 --topic topic-test --property schema.registry.url=http://srcSchemaregistry:8085 --property value.schema="$(cat data/schema.json)"
{"field1" : "a0", "field2": "b0"}
```

Confirm the namespaces are different:

```shell
curl http://localhost:8085/subjects/topic-test-value/versions/1/schema | jq
curl http://localhost:8086/subjects/topic-test-value/versions/1/schema | jq
```

### Clean-up

1. Stop the consumer (control C)
2. Clean the docker cluster `docker-compose down -v`

## Fix

Set the `connect.name` schema property as `namespace` + `name` 

