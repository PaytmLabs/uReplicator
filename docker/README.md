# uReplicator Docker

## Local setup

### Prerequisites

#### Build Zookeeper+Kafka 0.9
```bash
docker build -t spotify/kafka:0.9 docker/zk-kafka/kafka/
```

#### Build uReplicator controller
```bash
docker build \
  --build-arg zookeeper="zookeeper:2181" \
  --build-arg helix_cluster="helixTest" \
  --build-arg port=9000 \
  -t ureplicator-controller -f docker/controller/Dockerfile .
```

```bash
docker build -t ureplicator-controller -f docker/controller/Dockerfile .
```

### Build uReplicator worker with config files
```bash
docker build -t ureplicator-worker -f docker/worker/Dockerfile .
```

### Quick start

1. Start Kafka/Zookeeper 0.9
```bash
docker run -d --name zk-kafka \
 --env ADVERTISED_HOST=kafka \
 --env ADVERTISED_PORT=9092 \
 -p 2181:2181 -p 9092:9092 spotify/kafka:0.9
```

2. Start uReplicator controller
```bash
docker run -d \
 --link zk-kafka:zookeeper \
  -e "port=9000" -e "zookeeper=zookeeper:2181" \
  -p 9000:9000 ureplicator-controller
```

3. Start uReplicator worker(s)
```bash
docker run \
 --link zk-kafka:zookeeper \
 --link zk-kafka:kafka \
 -v config:/opt/ureplicator/config \
 ureplicator-worker
```
