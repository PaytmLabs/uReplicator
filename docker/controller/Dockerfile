FROM docker.paytmlabs.com/oracle-jdk

ARG zookeeper
ENV ZOOKEEPER $zookeeper
ARG helix_cluster
ENV HELIX_CLUSTER $helix_cluster
ARG port
ENV PORT $port

ADD uReplicator-Distribution/target/uReplicator-Distribution-pkg /opt/ureplicator
ADD config /opt/ureplicator/config

WORKDIR /opt/ureplicator

CMD /opt/ureplicator/bin/start-controller.sh -zookeeper $ZOOKEEPER -helixClusterName $HELIX_CLUSTER -port $PORT

