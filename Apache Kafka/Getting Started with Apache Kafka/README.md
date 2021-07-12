# Getting Started with Apache Kafka

## Author

Ryan Plant

## Course url

<https://app.pluralsight.com/library/courses/apache-kafka-getting-started/table-of-contents>

## Getting started with Apache Kafka

Kafka means Basically a nightmarish situation

![What is Apache kafka](Images/what-is-apache-kafka.png)

### Enterprise Challenges with Data

As large scale enterprise application grows, they create a lot of data that needs to be shared from different sources like in the image given below for different use cases.

![What a typical enterprise looks like](Images/what-a-typical-enterprise-looks-like.png)

These issues can be solved in a lot of different ways, some of which are

- Database replication
  - Supports only RDBMS only
  - Replication support is vendor dependent, so you can forget about cross vendor support
  - Tight coupling of (schema) has ripple effects on the replication stratergy
  - Cumbersome
- Log Shipping
  - Performance challenges depending on the size of the log
  - Cumbersome
- [ETL (Extract, Transform & Load)](<https://www.guru99.com/etl-extract-load-process.html>)
    > ETL is a process that extracts the data from different source systems, then transforms the data (like applying calculations, concatenations, etc.) and finally loads the data into the Data Warehouse system. Full form of ETL is Extract, Transform and Load.
    > It's tempting to think a creating a Data warehouse is simply extracting data from multiple sources and loading into database of a Data warehouse. This is far from the truth and requires a complex ETL process. The ETL process requires active inputs from various stakeholders including developers, analysts, testers, top executives and is technically challenging.
    >In order to maintain its value as a tool for decision-makers, Data warehouse system needs to change with business changes. ETL is a recurring activity (daily, weekly, monthly) of a Data warehouse system and needs to be agile, automated, and well documented.

  - Typically proprietary and costly
  - Lots of custom development, so the solution is not really portable
  - Scalability challenged
  - Performance Challenged
  - Often time require multiple instances
- Messaging
- Custom middleware magic
  ![Messaging systems are a form of middleware](Images/middle-ware-magic.png)
  - Custom middleware written to integrate different applications using either REST, or different data stores etc ..., this requires extensive knowledge of each data model. We will also have to distrubuted cordination logic and get out of easily the more distrubuted the system gets.

### Messaging Limitations and Challenges

- Limited scalability as scalability depends on the scalability of the message broker
- Smaller messages as larger messages can put strain on the message service
- Requires rapid consumption, apps should keep up with messages being published or else it might strain the message broker which can introduce a DDOS attack on itself
- Not fault-tolerant(application) as once the message is delivered/consumed by an application it is lost forever

![Perils of messaging under high volume](Images/perils-of-messaging-under-high-volume.png)

![Perils of messaging with application fault](Images/perils-of-messaging-application-fault.png)

![Middleware challenges](Images/middleware-challenges.png)

### A Use case with linkedin

Isn't there a better way to move data around :

- Cleanly
- Reliably
- Quickly
- Autonomously

![Linkedin volume](Images/linkeding-volume.png)

![Linkedin pre-2010](Images/pre-2010-linkeding-data-architecture.png)

### Apache Kafka as a viable solution

When linkedin created Apache Kafka, they had the following goals in mind

- The message bus should support high throughput
- The message bus should be horizontally scalable unlike old messaging systems
- The messages should be delivered in a reliable and durable manner, in the case of a failure from the consumer end, the message could be recoverable
- Loosely coupled between producers and consumers so no one is dependent on another and adding or removing producers will not bring down other consumers
- Flexible pub-sub semantics, independent data producing apps would send on a topic and consumers could receive those messages by subscribing to those topics

![Post 2010 LinkedIn Data Architecture](Images/post-2010-linked-data-architecture.png)

## Getting to know Apache Kafka's Architecture

Main components of the Apache Kafka eco system

- Producers : Send messages to a specific topic
- Consumers : subscirbe to a specific topic and retrieve them when new messages arrive
- Brokers : The place where kafka keeps and maintains topics is called the broker, which is an exe that runs a dameon service, a.k.a server, it stores the topics in the file system. The Kafka broker is what differentiates kafka from other messaging systems
- Topics : Are addresses to which producers post messages to from which consumers can retrieve them

![How Apache kafka starts to diffentiate](Images/kafka-throughput.png)

- Cluster : A Kafka cluster is a grouping of multiple Kafka brokers, a Kafka cluster can be created by clustering multiple instance of Kafka brokers running in a single physical machine or across multiple physical machines as long as they share the same grouping

![kafka Cluster](Images/kafka-cluster.png)

### Distributed Systems

![What are distributed systems](Images/what-are-distributed-systems.png)

A distribute node to ensure that due process is followed to achive the common goal it achieves, elects a Controller which is also a worker node to handle the administrative functions like

- Inventory of the workers available to take on work
- Maintain a list of work items that have been commited to and assigned to workers
- To maintain active status of the workers and their progress

#### Achieving Reliability in DS like Apache Kafka

![Getting Work done](Images/getting-work-done.png)

How reliability is achived through redundancy

![How reliability is achieved](Images/how-resiliency-is-achieved.gif)

#### Distributed Systems : Communicaion and Consensus

A DS needs communication and consensus between them to function namely on

![consensus](Images/communication-and-consensus.png)

To achieve this in Apache kafka we use

![Apache Zookeeper](Images/apache-zookeeper.png)

![Kafkas distributed architecture](Images/kafkas-distrubuted-architecture.png)

## Understanding Topics, Partitions, and Brokers

### Apache Kafka Topics

- Central Kafka Abstraction
- Named feed or category of messages
  - Producers produce
  - Consumers consume
- Logical entity
- By are physically represented in a log

Message asbtraction if Kafka
 ![Message asbtraction if Kafka](Images/message-abstraction-in-kafka.png)

### Event Sourcing

An architecture style or approach to maintaining an application's state by capturing all  changes as a sequence of time-ordered, immutable events

Zoomed in view of a Message producer

![image](Images/zoomed-in-view-of-a-message-producer.png)

When a producer produces an event, it appends the mesage to a time ordered sequence, the events are immutable, if a produces produces an incorrect message, then it cannot modify the existing message, it can only publish a new message and the onus falls upon the consumer to reconcile this.

### What a Kafka message content looks like

![messge content](Images/message-content.png)

### The Message Offset and Retention Policy

#### The Offset

Is a placeholder for

- The last read message position, think of it like a bookmar in the message queue
- is Maintained by the Kafka Consumer, so each consumer work at its own pace
- The last read position corresponds to the messsage Identifier

![How consumers work](Images/how-consumer-works.png)

#### Message Retention Policy

- Apache kafka retains all published messages regardless of consumption
- The rentention period is configurable
  - Defaults to 168 hours, then the messages starts falling off starting from the oldest
- Retention period is defined on a per-topic basis
- Physical storage resources can constrain message retention

#### Apache Kafka as a distrubted commit log

![alt](Images/rdbms-paralelles-to-apache-kafka.png)
Apache Kafka at its core is a ditributed commit log, a raw database, which
uses Pub/Sub semantices to communicate between consumer and producer. In RDBMS
the log files are nothing but a list of transaction logs which can be replayed to rebuild the database, like backups or replication stratergies.

#### Kafka Partitions

![Apache kafka partition details](Images/kafka-partiaion-details.png)

![Partition details with topics](Images/partition-detail-with-topics.png)

In genera, the scalability of Apache kafka is determined by the number of partitions being managed by multiple broker nodes

![How multiple partitions works](Images/multiple-partitions.png)

How Zookeeper handles request to create multiple partitions

![Alt](Images/how-zookeeper-assignes-brokers-to-partitions.png)

A Producer needs to know about atleast one broker in the clusterso it can find the leaders of the topic partitions. Each broker knows which partitions are owned by which leaders and sends this meta data about the topic to the producer when then can send messages to all the leaders in the cluster to different partitions

![alt](Images/how-producers-initiate-messages-to-brokers-with-partition.png)

This is a bit tricky, the consumer checks with Zookeeper about the brokers and their respective partitions which make up the topics, it will then pull the messages from these partitions based on the message offset per partition, because messages are produced to multiple partitions and at different times, consumers working with multiple partitions will likely consume messages at different orders and will therefore be responsible for handling the order if it is required

![alt](Images/how-consumers-initiate-messages-to-brokers-with-partition.png)

## Producing Messages with Kafka Producers

## Consuming Messages with Kafka Consumers and Consumer Groups

## Exploring the Kafka Ecosystem and Its Future
