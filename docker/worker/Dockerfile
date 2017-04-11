FROM docker.paytmlabs.com/oracle-jdk

ADD uReplicator-Distribution/target/uReplicator-Distribution-pkg /opt/ureplicator
ADD config /opt/ureplicator/config

WORKDIR /opt/ureplicator

CMD /opt/ureplicator/bin/start-worker.sh startMirrorMakerWorker --consumer.config config/consumer.properties --helix.config config/helix.properties --producer.config config/producer.properties

