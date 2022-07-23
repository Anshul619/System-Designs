# System-Designs

This repo contains the various system design questions and solutions. [Read system design glossaries](src/DesignComponents/SystemDesignGlossaries.md).

# Various components & Performance Metrics

| Component                                                                                                           | Strength                         | Component Type                                                | Very Rough Throughput (QPS)                       | Latency | Free |
|---------------------------------------------------------------------------------------------------------------------|----------------------------------|---------------------------------------------------------------|---------------------------------------------------|----------------|------|
| [Kafka](src/DesignComponents/Kafka)                            | High-Throughput MQ               | Message Queue (Pub-Sub)            | 1000K ( 1 million ) messages ( write ) per second | ~5ms | Yes   |
| [RabbitMQ](src/DesignComponents/Kafka#kafka-vs-rabbitmq)       | Low-Latency MQ                   | Message Queue (Point-2-Point)         | 20K messages ( write ) per second                 | ~1ms |  Yes   |
| [Redis](src/DesignComponents/Redis)                           | In-Memory fast Data-Store        | Caching                          | 100K queries per second                           | -|  Yes   |
| [MySQL](https://www.mysql.com/)                                                                                     | -                                | SQL DB                           | 1000 concurrent requests ( 100 as default )       | [< 10ms ( to get a row from 1 million records )](https://www.quora.com/How-can-we-calculate-the-throughput-of-MySQL?share=1)|Yes|
| [DynomoDB](src/DesignComponents/SQLvsNoSQL/ReadMe.md#dynomodb) | Predictable performance and cost | NoSQL DB as a Service ( AWS )  | More than 20 million requests per second          | less than 10-20 ms | No  |
| [MongoDB](https://www.mongodb.com)                                                                                  | -                                | NoSQL DB                         | -                                                 | -|  No                                      |
| [ElasticSearch](src/DesignComponents/ElasticSearch)           | -                                | Search Engine                    | -                                                 |-|No|
| [Apache](https://apache.org/)                                                                                       | -                                | Web Server                       | 512 concurrent requests                           |-|Yes|

# Tech Guidelines ( from Scalability perspective )
- Develop the microservice based architecture
- Generally, we should aim for `MAXIMAL throughput` with `ACCEPTABLE latency`.
- We must consider `cloud-agnostic approach` ( & onPerm customer approach ) while designing the solution.
- If it's a READ heavy microservice, the best decision would be to use `Redis` or `multi-read database instances`.
- If it's WRITE heavy microservice ( `HIGH throughput` ), the best decision would be to use either `Kafka` ( as message queue ) or `DynamoDB` ( as data store ). 
  - Both can handle `HIGH throughput`.

## Design Components
- [SQL vs NoSQL - MySQL, PostgreSQL, DynomoDB, Casandra, MongoDB etc.](src/DesignComponents/SQLvsNoSQL)
- [MQs like Kafka, RabbitMQ, Amazon MQ, SQS, SNS etc.](src/DesignComponents/Kafka)
- [ElasticSearch - "NoSQL" Search Engine](src/DesignComponents/ElasticSearch)
- [In-Memory Cache like Redis, MemCache etc.](src/DesignComponents/Redis)
- [AWS Storage Options - S3 vs EFS vs EBS](src/DesignComponents/EFSvsS3)
- [AWS - Various Components, Guide](src/DesignComponents/AWS.md)
- [Monolothic to MicroService](src/DesignComponents/MonolothicToMicroservice)
- [Design a system that scales to million of users on AWS](src/DesignComponents/DesignScalableSystemWithRDMS)

## HLD - Design Problems
- [Zomoto HLD Design](src/ZomatoDesign)
- [Twillo Send Message API](src/TwilloSendMessageAPI)
- [Rate Limiter API](src/RateLimiterAPI)
- [Notification System](src/NotificationSystem)
- [Logging Solution](src/LoggingSolution)
- [MakeMyTrip Search](src/MakeMyTripSearch)
- [URL Shortening Service](src/URLShorteningService)

## Engineering Principles
- [SOLID](https://github.com/Anshul619/System-Designs/blob/main/src/DesignComponents/SOLID.md)
- [OOPS](https://github.com/Anshul619/System-Designs/blob/main/src/DesignComponents/OOPS.md)
- [Design Patterns](https://github.com/Anshul619/System-Designs/tree/main/src/DesignComponents/DesignPatterns)
- [DRY](https://github.com/Anshul619/System-Designs/blob/main/src/DesignComponents/DRY.md)

## LLD - Design Problems
- [LLD Design - Tips & Techniques](https://github.com/Anshul619/System-Designs/tree/main/src/DesignLLDProblems/LLDDesignTipsAndTechniques.md)
- [Chess Game](https://github.com/Anshul619/System-Designs/tree/main/src/DesignLLDProblems/ChessGame)
- [Snack & Ladder Game](https://github.com/Anshul619/System-Designs/tree/main/src/DesignLLDProblems/SnackAndLadderGame)
- [Book My Show](https://github.com/Anshul619/System-Designs/tree/main/src/DesignLLDProblems/BookMyShow)
- [Car Rental System](https://github.com/Anshul619/System-Designs/tree/main/src/DesignLLDProblems/CarRentalSystem)
- [Vendor Machine](https://github.com/Anshul619/System-Designs/tree/main/src/DesignLLDProblems/VendorMachine)
- [Hotel Booking System](https://github.com/Anshul619/System-Designs/tree/main/src/DesignLLDProblems/HotelBookingSystem)
- [Parking Lot](https://github.com/Anshul619/System-Designs/tree/main/src/DesignLLDProblems/ParkingLot)
- Others
  - [Insurance Agent Flow](https://github.com/Anshul619/System-Designs/tree/main/src/DesignLLDProblems/InsuranceAgentFlow.md)

## Tech Skills
- [Spring Boot & Microservices](https://github.com/Anshul619/System-Designs/tree/main/src/DesignComponents/SpringBootAndMicroServices)
- [Java](https://github.com/Anshul619/System-Designs/tree/main/src/DesignComponents/Java)
- [Hibernate](https://github.com/Anshul619/System-Designs/blob/main/src/DesignComponents/Hiberate.md)
- [JS](https://github.com/Anshul619/System-Designs/tree/main/src/DesignComponents/JavaScript)
- [Testing](https://github.com/Anshul619/System-Designs/blob/main/src/DesignComponents/Testing.md)
- [JavaScript](https://github.com/Anshul619/System-Designs/blob/main/src/DesignComponents/JavaScript)
- [TypeScript](https://github.com/Anshul619/System-Designs/blob/main/src/DesignComponents/TypeScript.md)
- [Angular8](https://github.com/Anshul619/System-Designs/blob/main/src/DesignComponents/Angular8.md)

# References
- [System Design Primer](https://github.com/donnemartin/system-design-primer)
- [Grokking the System Design](https://www.educative.io/courses/grokking-the-system-design-interview/39RwZr5PBwn)
- [System Design by Gaurav Sen](https://www.youtube.com/watch?v=xpDnVSmNFX0&list=PLMCXHnjXnTnvo6alSjVkgxV-VH6EPyvoX)
- [Benchmarking Apache Kafka, Apache Pulsar, and RabbitMQ: Which is the Fastest?](https://www.confluent.io/blog/kafka-fastest-messaging-system/)
- [System Design - Interview Questions](https://leetcode.com/discuss/interview-question/system-design?currentPage=1&orderBy=hot&query=)
