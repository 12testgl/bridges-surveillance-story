# Bridge Management Logistics

---


[![Generic badge](https://img.shields.io/static/v1.svg?label=GitHub&message=Bridge%20Surveillance%20Story%20🌉&color=informational)](https://github.com/jesperancinha/bridges-surveillance-story)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

[![bridge-logistics-app](https://github.com/jesperancinha/bridges-surveillance-story/actions/workflows/bridge-logistics-app.yml/badge.svg)](https://github.com/jesperancinha/bridges-surveillance-story/actions/workflows/bridge-logistics-app.yml)
[![e2e-bridge-logistics-app](https://github.com/jesperancinha/bridges-surveillance-story/actions/workflows/bridge-logistics-e2e.yml/badge.svg)](https://github.com/jesperancinha/bridges-surveillance-story/actions/workflows/bridge-logistics-e2e.yml)

[![Codacy Badge](https://app.codacy.com/project/badge/Grade/56395dd932804738979bbcb3bec4bc5f)](https://www.codacy.com/gh/jesperancinha/bridges-surveillance-story/dashboard?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=jesperancinha/bridges-surveillance-story&amp;utm_campaign=Badge_Grade)

[![Codacy Badge](https://app.codacy.com/project/badge/Coverage/56395dd932804738979bbcb3bec4bc5f)](https://www.codacy.com/gh/jesperancinha/bridges-surveillance-story/dashboard?utm_source=github.com&utm_medium=referral&utm_content=jesperancinha/bridges-surveillance-story&utm_campaign=Badge_Coverage)
[![codecov](https://codecov.io/gh/jesperancinha/bridges-surveillance-story/branch/master/graph/badge.svg?token=rSu5dH7N7q)](https://codecov.io/gh/jesperancinha/bridges-surveillance-story/tree/master)
[![Coverage Status](https://coveralls.io/repos/github/jesperancinha/bridges-surveillance-story/badge.svg?branch=master)](https://coveralls.io/github/jesperancinha/bridges-surveillance-story?branch=master)

[![GitHub language count](https://img.shields.io/github/languages/count/jesperancinha/bridges-surveillance-story.svg)](#)
[![GitHub top language](https://img.shields.io/github/languages/top/jesperancinha/bridges-surveillance-story.svg)](#)
[![GitHub top language](https://img.shields.io/github/languages/code-size/jesperancinha/bridges-surveillance-story.svg)](#)


## Technologies used

Please check the [TechStack.md](TechStack.md) file for details.

## Introduction

This application uses event sourcing to serve the logistics for a bridge management system. This is what in general this
project is responsible for

1.  Count passengers going through a bridge
2.  Register transport type
3.  Register merchandise before crossing the bridge
4.  Register events per configured range area
5.  Inform trains of the train Schedule changes

Passengers are registered by numbers and if they carry extra merchandise or a bike Transport can be a train, bus, boat,
bike, truck, etc. Merchandise should be registered if it's destined to commercial exchanges. Events can be anything that
may happen in a configured range around the bridge

1.  For passengers, a development area will be created called PCS(Passenger Control Service).
2.  For merchandise, a development area will be created called MCS(Merchandise Control Service).
3.  For bridge timetables and ranges, a development area will be created called DCS(Domain Control Service).


<details>
<summary><b>Stable Releases</b></summary>

This repo is also the official support repo to my article on medium:

[![](https://img.shields.io/badge/The%20streaming%20bridges%20—%20A%20Kafka,%20RabbitMQ,%20MQTT%20and%20CoAP%20example-12100E?style=for-the-badge&logo=medium&logoColor=white)](https://medium.com/swlh/the-streaming-bridges-a-kafka-rabbitmq-mqtt-and-coap-example-9077a598169)

#### Stable releases

-   [1.0.0](https://github.com/jesperancinha/bridges-surveillance-story/tree/1.0.0) - [441f1dfc85467d69e93a445a5db6489ebf2a7211](https://github.com/jesperancinha/bridges-surveillance-story/tree/1.0.0)
-   [2.0.0](https://github.com/jesperancinha/bridges-surveillance-story/tree/2.0.0) - [a8544e6611d0856809b6a3c7b5dd124a3d7067c1](https://github.com/jesperancinha/bridges-surveillance-story/tree/2.0.0)
-   [3.0.0](https://github.com/jesperancinha/bridges-surveillance-story/tree/3.0.0) - [12cb8d3c481fac4587787683d2a114ca2f7e6952](https://github.com/jesperancinha/bridges-surveillance-story/tree/3.0.0) - Java / JDK17 / Scala / Python / Spring Boot 2.7.4
-   [4.0.0](https://github.com/jesperancinha/bridges-surveillance-story/tree/4.0.0) - [591e0ff5797f736577669500826b5bca90a9b4e9](https://github.com/jesperancinha/bridges-surveillance-story/tree/4.0.0) - Kotlin 1.8.0 / JDK17 / Scala / Python / Spring Boot 2.7.4

</details>

## A detective case

I have created an investigation Game. It's not a difficult one to solve. Basic math will get you through to find the
thief.

> A passenger unsuspectingly travelling in a train carrying a leather suitcase with an old 5Kg computer filled with
> classified information has had its bag stolen.
> The suspect jumps off the train while it passes through a connecting bridge
> In the far we see a person in a parachute falling down through the air into a boat which catches this person a moves
> away
> The passenger, a special agent keeps their cover and worries if this secret spy will ever be caught

You, the player are responsible for finding the secret spy! 🕵️‍ 🔍

Steps:

1.  Go to PostgresSQL database on schema `bllogistics` in table `trains_log`. Filter
   by `check_in_out='CHECKIN' or check_in_out='CHECKOUT'`
    1.  You will find two carriages with different weights at `CHECKIN` and at `CHECKOUT`.
    2.  On carriage has a weight reduction of two people.
    3.  This is because, while passing through the bridge, the `spy` takes the bag from the `special agent` and run to
       the next carriage.
    4.  The `special agent` follows the `spy` and chases the `spy`.
    5.  In another carriage, there is an increase in weight, but just for the special agent
    6.  The secret spy has escaped through the toilet's window and with precision jumped off the bridge in a parachute.
    7.  The formula is: SPY_WEIGHT = (CARRIAGE_1_CHECKIN_WEIGHT - CARRIAGE_1_CHECKOUT_WEIGHT) - (
       CARRIAGE_2_CHECKOUT_WEIGHT - CARRIAGE_2_CHECKIN_WEIGHT).
2.  Calculate the difference in weight
3.  Go to Cassandra database on keyspace `readings` in table `passengers`. Filter by the weight you find. These are the
   suspects
4.  If you only have one suspect. Then congratulations you have found the secret agent who stole the bag.
5.  Type your answer in the following format `firstName` + ` ` + `lastName`

Note that the story I’ve created is purely fictional. Any similarity between events and the characters generated and the
locations described is purely coincidental. It is practically impossible to make a random scenario that doesn’t have
anything in common with anyone’s personal life. This is the reason why it is so important that the reader of this
article understands that. This is also the reason why all the names in this exercise are automatically randomly
generated, precisely to reduce the possibility of such similarities to occur. You DO NEED to generate the names first.
By running file [passenger_generator.py](./bl-simulation-data/passenger_generator.py), you will find 4 files in
the [passengers](./bl-simulation-data/passengers) folder. In this file, you will find automatically generated names. If
you want to make this more fun you can add your own chosen names. Just remember that each line must be a single name.

## Modules

### Docker Images

1.  [bl-central-server](./bl-central-server): The central server containing all centralized data
    1.  [bl-central-cassandra](./bl-central-server/bl-central-cassandra) - Cassandra database image (Contains calculated
       and dynamic data)
    2.  [bl-central-psql](./bl-central-server/bl-central-psql) - Postgres database image (Contains static information
       about passengers, vehicles, trains and bridges)
    3.  [bl-central-streaming](./bl-central-server/bl-central-streaming) - RabbitMQ strams for train, vehicle and bridge
    4.  [kafka](./bl-central-server/kafka) - A kafka streaming engine. It creates topics TEMPERATURE, HUMIDITY,
       WINDSPEED, WINDDIRECTION, PASSENGER. It is centralized to take data from the bridge and the moving train. Two
       brokers make use of ports 9092 and 9093.

### Libraries

1.  [bl-central-server](./bl-central-server): The central server containing all centralized data
    1.  [bl-domain-repository](./bl-central-server/bl-domain-repository) - Java domain model to use in the different Java
       processes. Contains all the PostgreSQL database model DAO's

### Services

1.  [bl-central-server](./bl-central-server): The central server containing all centralized data
    1.  [bl-merchandise-data-collector](./bl-central-server/bl-merchandise-data-collector) - Java service responsible for
       collecting merchandise info and sending it through RabbitMQ to the centralized services.
    2.  [bl-sensor-data-collector](./bl-central-server/bl-sensor-data-collector) - Java service responsible for
       collecting check-in and check-out data from trains entering and leaving the bridge and sending it through
       RabbitMQ to the centralized services.
    3.  [bl-passengers-readings-service](./bl-central-server/bl-passengers-readings-service) - Scala service responsible
       for collecting passenger data from the Kafka (via the train) streams and sending it to cassandra
    4.  [bl-meters-readings-service](./bl-central-server/bl-meters-readings-service) - Scala service responsible for
       collecting meter data from the Kafka (via the bridge) streams and sending it to cassandra
    5.  [bl-web-app](./bl-central-server/bl-web-app) - Java service which checks if the bridge is open for vehicle
       crossing. It is open in port 9000
    6.  [bl-web-ui](./bl-central-server/bl-web-ui) - Angular (?) - For future visualizations -
       Check [ReviewLogs.md](./ReviewLogs.md) for details about Roadmap to version 3.0.0

---

2.  [bl-bridge-server](./bl-bridge-server): A server installed on each bridge
    1.  [bl-bridge-humidity-mqtt](./bl-bridge-server/bl-bridge-humidity-mqtt) - Node JS - Receives humidity readings from
       the [mosquitto](./bl-bridge-server/mosquitto) broker on port 1883 and sends it to Kafka via the HUMIDITY topic
    2.  [bl-bridge-temperature-coap](./bl-bridge-server/bl-bridge-temperature-coap) - Node JS - Receives temperature
       readings from a COAP protocol port 5683 and sends it to Kafka via the TEMPERATURE topic
    3.  [mosquitto](./bl-bridge-server/mosquitto) - A simple mosquitto broker with bare minimal configuration and
       authentication turned off. Opens port 1883 for
       the [bl-bridge-humidity-mqtt](./bl-bridge-server/bl-bridge-humidity-mqtt) service
    4.  [rabbitmq](./bl-bridge-server/rabbitmq) - The federated RabbitMQ service connecting to the central RabbitMQ
       services

---

3.  [bl-train-server](./bl-train-server): A server installed on each train
    1.  [rabbitmq](./bl-train-server/rabbitmq): RabbitMQ - RabbitMQ to send sensor information about train checking in
       and out of the bridge

---

4.  [bl-demo-server](./bl-demo-server): This server ensures that a simulated train passes through the bridge. It will use
   all different container ports to execute the simulation and create a different case everytime the simulation is run.

## How to quickly start

Make sure you have enough resources and that you are
running [Docker desktop](https://www.docker.com/products/docker-desktop):

1.  At least 6Gb available memory
2.  At least 8 cores
3.  At least 5Gb to 10Gb of free diskspace

Please check the [Makefile](./Makefile) and make sure you understand the available options before calling them.

This whole demo is quite a heavy example to run. Because it can be difficult to run, given the amount of resources
consumed, I have made a [Checkups](./Checkups.md) guide and an example [Guide](./Guide.md) file. Please read through
them before running the demo.

## Walk through

In order to make it easy to understand this example, I've made a [Walkthrough](./WalkThrough.md) document. This is
intended to help understand the basic goal of this example.

## Constraints

1.  Trains go over static bridges which are mostly open. They can be closed for exceptional reasons.
2.  When trains go over bridge, we need to know how long the whole train took to cross it.
3.  We also need to know the complete weight being passed across the bridge in regard to merchandise.
4.  We aso need to know the complete weight being passed across the bridge in regard to people.
5.  The exact number of people will be an approximation and will be a result from a triangulation of passing through heat
   sensors and light sensors.
6.  Timetables and merchandise exchanges will be done via RabbitMQ.
7.  Sensor information will be sent via Kafka.
8.  People data will be sent via Kafka Streams.
9.  All Kafka streamed information will be handled via Apache Spark.
10. Bridge opening times are subject to conflict detection. Upon detecting one conflict between opening times. The
    bridge remains closed until the conflict becomes resolved.
11. Conflict registration changes state but never gets removed

## Installation Notes

To run this demo, you only need to have a docker engine installed or something that comes with it like Docker Desktop.
Further you need JDK 11 and JDK 16. This demo has been tested using [SDK-MAN](https://sdkman.io/) Java SDK version
16.0.1.hs-adpt:

```shell
sdk install 11.0.11.hs-adpt
sdk use 11.0.11.hs-adpt
```

```shell
sdk install java 16.0.1.hs-adpt
sdk use java 16.0.1.hs-adpt
```

Use Java 16 as the default. You'll only need Java 11 for the Kafka Readers. If you want to install everything locally
without the help of containers then please check help file [InstallationNotes.md](./docs/InstallationNotes.md). Further
Documentation is available at
the [wiki](https://github.com/jesperancinha/bridges-surveillance-story/-/wikis/Installation-notes).

Install python libraries:

```shell
pip install virtualenv
pip install virtualenvwrapper
```

Install virtualenv:

```shell
virtualenv venv --python=python3.7
source venv/bin/activate
pip3 install requests
pip3 install pika
pip3 install kafka-python
pip3 install aiocoap
pip3 install mqtt
pip3 install paho-mqtt
pip3 install asyncio
pip3 install distlib
pip3 install --upgrade pip
```

Exit virtualenv:

```shell
deactivate
```

## Review Logs

Follow the updates on the [ReviewLogs](./ReviewLogs.md) file.

## Author notes

I hope you enjoyed the article and that you were able to start this demo. I try my best to make these demos run as
smoothly as possible. This is why I actually invite you to open an issue on this repo, should you run into difficulties
running this demo, playing the game or even if you just have some suggestions for improvement. Note that while a version
is ongoing as of now with 2.0.0., there are constant changes until an official tagged release.

## References

-   [What is Apache Kafka? Why is it so popular? Should you use it?](https://techbeacon.com/app-dev-testing/what-apache-kafka-why-it-so-popular-should-you-use-it)
-   [RabbitMQ](https://en.wikipedia.org/wiki/RabbitMQ#History)
-   [Rabbit Technologies](https://www.crunchbase.com/organization/rabbit-technologies#section-overview)
-   [Advanced Message Queuing Protocol](https://www.amqp.org/)
-   [RabbitMQ for beginners - What is RabbitMQ?](https://www.cloudamqp.com/blog/2015-05-18-part1-rabbitmq-for-beginners-what-is-rabbitmq.html)
-   [Advanced Message Queuing Protocol](https://en.wikipedia.org/wiki/Advanced_Message_Queuing_Protocol)
-   [Understanding AMQP, the protocol used by RabbitMQ](https://spring.io/blog/2010/06/14/understanding-amqp-the-protocol-used-by-rabbitmq/)
-   [Get to Know MQTT: The Messaging Protocol for the Internet of Things](https://thenewstack.io/mqtt-protocol-iot/)
-   [Constrained Application Protocol](https://en.wikipedia.org/wiki/Constrained_Application_Protocol)
-   [RFC 7252 Constrained Application Protocol](https://coap.technology/)
-   [CoAP RFC 7252](https://iottestware.readthedocs.io/en/master/coap_rfc.html)
-   [The Constrained Application Protocol (CoAP)](https://datatracker.ietf.org/doc/rfc7252/)
-   [Message Oriented Middleware](https://www.trustradius.com/message-oriented-middleware#overview)
-   [John O' Hara, Chairman - AMQP Working Group](https://qconlondon.com/london-2007/speakers/show_speakerddb0.html?oid=180)
-   [How does protocol mediation work?](https://www.dpstele.com/snmp/transition/how-does-mediation-work.php)
-   [Ingress Traffic](https://www.techopedia.com/definition/2415/ingress-traffic)
-   [When to use RabbitMQ or Apache Kafka](https://www.cloudamqp.com/blog/2019-12-12-when-to-use-rabbitmq-or-apache-kafka.html)
-   [Part 4: RabbitMQ Exchanges, routing keys and bindings](https://www.cloudamqp.com/blog/2015-09-03-part4-rabbitmq-for-beginners-exchanges-routing-keys-bindings.html)
-   [Scalability of Kafka Messaging using Consumer Groups](https://blog.cloudera.com/scalability-of-kafka-messaging-using-consumer-groups/)
-   [UIC classification of goods wagons](https://en.wikipedia.org/wiki/UIC_classification_of_goods_wagons)
-   [DB Cargon freight wagons](https://nl.dbcargo.com/resource/blob/1430008/9767e97bb070ccbbf77efd84e7d64948/freight_wagon_catalog_v2011-data.pdf)
-   [How are freight cars classifed by IR?](https://www.irfca.org/faq/faq-stock2.html)
-   [Hornby Wagons](https://www.hornby.com/uk-en/)
-   [Goods wagon](https://en.wikipedia.org/wiki/Goods_wagon)
-   [Python online compiler](https://www.programiz.com/python-programming/online-compiler/)
-   [Java 16 Records with JPA and jOOQ](https://72.services/java-16-records-with-jpa-and-jooq/)
-   [JDK 17 - What's new features in Java 17](https://www.techgeeknext.com/java/java17-features)
-   [Spring Tips: Java 14 (or: Can Your Java Do This?)](https://spring.io/blog/2020/03/11/spring-tips-java-14-or-can-your-java-do-this)
-   [Share Link Generator!](http://sharelinkgenerator.com/)
-   [Docker Desktop for Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac)
-   [Kafka vs. RabbitMQ: Architecture, Performance & Use Cases](https://www.upsolver.com/blog/kafka-versus-rabbitmq-architecture-performance-use-case)
-   [Real-Time Analysis of Popular Uber Locations using Apache APIs: Spark Structured Streaming, Machine Learning, Kafka and MapR Database](https://mapr.com/blog/real-time-analysis-popular-uber-locations-spark-structured-streaming-machine-learning-kafka-and-mapr-db/)
-   [IoT architecture: building blocks and how they work](https://www.scnsoft.com/blog/iot-architecture-in-a-nutshell-and-how-it-works)
-   [Top 15 Standard IoT Protocols That You Must Know About](https://www.ubuntupit.com/top-15-standard-iot-protocols-that-you-must-know-about/)
-   [Using Apache Kafka as a Scalable, Event-Driven Backbone for Service Architectures](https://www.confluent.io/blog/apache-kafka-for-service-architectures/)
-   [MQTT](https://www.npmjs.com/package/mqtt)
-   [Internet of Things: Where Does the Data Go?](https://www.wired.com/insights/2015/03/internet-things-data-go/)
-   [Apache Kafka Documentation](https://kafka.apache.org/documentation/)
-   [Apache Kafka Installation on Mac using Homebrew](https://medium.com/@Ankitthakur/apache-kafka-installation-on-mac-using-homebrew-a367cdefd273 )
-   [Offset Management For Apache Kafka With Apache Spark Streaming](https://blog.cloudera.com/offset-management-for-apache-kafka-with-apache-spark-streaming/)
-   [Confluent Tutorial: Creating a Streaming Data Pipeline](https://docs.confluent.io/current/streams/quickstart.html)
-   [Spark Streaming + Kafka Integration Guide (Kafka broker version 0.10.0 or higher)](https://spark.apache.org/docs/2.2.0/streaming-kafka-0-10-integration.html)
-   [Spark Streaming Programming Guide](https://spark.apache.org/docs/2.2.0/streaming-programming-guide.html)
-   [Apache Spark Tutorial](https://www.javatpoint.com/apache-spark-tutorial)
-   [Java EE vs Spring Testing](https://antoniogoncalves.org/2018/01/16/java-ee-vs-spring-testing/)
-   [Arquillian JUnit5 Hacks](https://github.com/OndroMih/arquillian-junit5-hacks)
-   [Java Libhunt Arquillian Alternatives](https://java.libhunt.com/arquillian-github-com-alternatives)
-   [Eclipse EE4J](https://projects.eclipse.org/projects/ee4j)
-   [Arquillian](http://arquillian.org/)
-   [Java™ EE at a Glance](https://www.oracle.com/java/technologies/java-ee-glance.html)
-   [JMS vs RabbitMQ](https://dzone.com/articles/jms-vs-rabbitmq)
-   [Get Started with RabbitMQ](https://www.rabbitmq.com/getstarted.html)
-   [Microservice Architecture by Kong](https://microservices.io/)
-   [Integrate ActiveMQ with WildFly](http://www.mastertheboss.com/jboss-server/jboss-jms/integrate-activemq-with-wildfly)
-   [SQL Server Table and Column Naming Conventions](https://www.codeproject.com/Articles/1065295/SQL-Server-Table-and-Column-Naming-Conventions)
-   [The Power of a Good SQL Naming Convention](https://www.xaprb.com/blog/2008/10/26/the-power-of-a-good-sql-naming-convention/)
-   [Integration Testing for Java EE](https://www.oracle.com/technetwork/articles/java/integrationtesting-487452.html)
-   [How to create Docker Images with a Dockerfile](https://www.howtoforge.com/tutorial/how-to-create-docker-images-with-dockerfile/)
-   [How to create a Docker image for PostgreSQL and persist data](https://www.andreagrandi.it/2015/02/21/how-to-create-a-docker-image-for-postgresql-and-persist-data/)
-   [Dockerize PostgreSQL](https://docs.docker.com/engine/examples/postgresql_service/)

## About me

[![GitHub followers](https://img.shields.io/github/followers/jesperancinha.svg?label=Jesperancinha&style=for-the-badge&logo=github&color=grey "GitHub")](https://github.com/jesperancinha)
