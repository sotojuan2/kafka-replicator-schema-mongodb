# Replicator Schema demo

## Proposal

Confirm the connect.name forces the replicated namespace in the destination schema.

## Running the demo

```shell
    ./start-cluster.sh
```

Then add source and sink connector

### Source connector.

Create source connector on source cluster.

```shell
cd mongodb
curl -X POST -H "Content-Type: application/json" -d @cdc-source.json http://localhost:9083/connectors 
```

### Sink connector.

Create sink connector on target cluster.

```shell
cd mongodb
curl -X POST -H "Content-Type: application/json" -d @cdc-sink.json http://localhost:8083/connectors 
```

Confirm the MongoDB connectors are running.

Create, update and delete documents on source collection and it will be replicated on target collection.

### Clean-up

1. Stop the consumer (control C)
2. Clean the docker cluster `docker-compose down -v`

## Fix

Set the `connect.name` schema property as `namespace` + `name` 

