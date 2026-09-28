🚀 I thought I understood Kafka — until I tried to deploy it.
Kafka ko theory mein samajhna kaafi simple lagta hai:
Producer → Topic → Partition → Consumer
But while implementing Kafka on Kubernetes using Strimzi, I came across a bigger architectural question:
“If Kafka itself is a distributed system, who manages the Kafka cluster?”
Earlier Kafka deployments used ZooKeeper for cluster coordination and metadata management.
The architecture looked roughly like:

        ZooKeeper
            |
    +-------+-------+
    |       |       |
 Broker1 Broker2 Broker3

Then Kafka introduced KRaft — Kafka Raft.

The architecture became:

     KRaft Controllers
        /    |    \
       /     |     \
   Broker1 Broker2 Broker3

So the interesting change is not simply:

ZooKeeper → KRaft

The bigger question is:

How does Kafka manage cluster metadata and coordination without a separate ZooKeeper system?

That is what I wanted to understand practically.

So I deployed Kafka on Kubernetes/GKE using Strimzi, created:

Kafka cluster
3 partitions
Replication factor of 3
Kafka topic
Producer
Consumer

And then started testing what actually happens when messages are produced, consumed, replicated and eventually when a broker fails.

My learning so far:

ZooKeeper architecture

Kafka + ZooKeeper

vs.

Modern KRaft architecture

Kafka + KRaft Controllers

In the next post, I'll show the actual Kubernetes implementation — from installing Strimzi to creating the Kafka topic and sending the first message.

#Kafka #KRaft #ZooKeeper #Kubernetes #GKE #Strimzi #DevOps #Cloud #PlatformEngineering #DistributedSystems

Next → Kafka implementation on Kubernetes: Strimzi + KafkaTopic + Producer + Consumer
