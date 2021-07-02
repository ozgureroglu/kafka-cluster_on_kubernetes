# kafka-cluster_on_kubernetes

Prerequisities
1. install a kubernetes cluster
2. Create a new namespace for cluster
3. kubectl create ns kafka-test
4. Prepare persistent volumes for setup using pv.yml . This yml create a 8 x 1G pvs.
5. kubectl -n kafka-test create -f pv.yml
6. Clone the repository to the kube management machine https://github.com/confluentinc/cp-helm-charts
7. git clone https://github.com/confluentinc/cp-helm-charts
8. Disable the charts that we do not want to deploy and change the parameters for the components, ie,  enable nodeport, change pvclaim sizes
9. helm install kafkademo --namespace kafka-test --set cp-schema-registry.enabled=false,cp-kafka-rest.enabled=false,cp-kafka-connect.enabled=false,cp-control-center.enabled=false,cp-ksql-server.enabled=false,cp-kafka.nodeport.enabled=true,cp-zookeeper.persistence.dataDirSize=1Gi,cp-zookeeper.persistence.dataLogDirSize=1Gi,cp-kafka.persistence.size=1Gi,cp-kafka.prometheus.jmx.enabled=false,cp-zookeeper.prometheus.jmx.enabled=false,cp-kafka.persistence.storageClass="manual",persistence.storageClass="manual",cp-zookeeper.persistence.dataLogDirStorageClass="manual" confluentinc/cp-helm-charts
