
# SQL vs NoSQL

Basis                                 | SQL                                                                                                                                                                                     | NoSQL                                                                                                                                                                             |
---------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
Data Type | Normalized, Structured Data                                                                                                                                                             | Denormalized, Unstructured data                                                                                                                                                   |
Schema | `Fixed Schema`                                                                                                                                                                            | Dynamic Schema ( with hierarchical storage supported )                                                                                                                            |                                                                                             |
Ideal Use Cases | SQL is best suitable for complex queries, multi-row transactions, joins etc. Data is structured ( like e-commerce, financial applications etc.) and also when data reporting is needed. | NoSQL is best suited for unstructured data or documents ( or large volume of data ). Not ideal for complex queries.                                                               |                                                                                             |
Write Performance | Okay<br/>- Every write is not just an append to a table but also an update to multiple index which might require locking and hence might interfere with other reads and other writes    | Very Good<br/>- Writes are cheaper                                                                                                                                                |                                                                                             |
Querying | Very Powerful                                                                                                                                                                           | Okay                                                                                                                                                                              |                                                                                             |
Scalability | Vertically Scalable ( increase memory, CPU of machine ) or Master-Slave technique ( 1 write DB, multiple read DBs )                                                                     | Horrizontally Scalable ( through in-built data sharding technique )                                                                                                               |                                                                                             |
Properties | SQL enables [ACID (atomicity, consistency, isolation, and durability)](../SystemDesignGlossaries.md#acid-properties-of-the-transaction) transaction properties.                         | NonSQL follows [CAP (consistency, availability, partition tolerance)](../SystemDesignGlossaries.md#cap-theorem-of-the-distributed-systems) properties of the distributed systems. |                                                                                             |
Best Features | Secure, Cross Platform Support, Free                                                                                                                                                    | High Performance, Flexible, Easy to use                                                                                                                                           |
Built-in Single Machine Failure | Supported                                                                                                                                                                               | Not-Supported                                                                                                                                                                     |

# SQL - Intro

<img title="SQL - Different Types" alt="Alt text" src="SQL - Different Types.drawio.png">

Relational databases store data in rows and columns.
- Each row contains all the information about one entity and each column contains all the separate data points.
- Some of the most popular relational databases are `AWS RDS`, `Postgres`, `MySQL`, `Oracle`, `MS SQL Server`, `SQLite` and `MariaDB`.

# NoSQL - Intro, Different NoSQL types

<img title="NoSQL - Different DB types" alt="Alt text" src="NoSQL - Different DB types.drawio.png">

## Key-Value Stores 
- Data is stored in an array of key-value pairs. 
- The `key` is an attribute name which is linked to a `value`. 
- Well-known key-value stores include `AWS Dynamo DB`, `Redis` etc.

## Document Databases 
- In these databases, data is stored in documents (instead of rows and columns in a table) and these documents are grouped together in collections. 
- Each document can have an entirely different structure. 
- Document databases include `MongoDB`, `CouchDB` etc.

## Wide-Column Databases 
- Instead of `tables`, we have column families in column databases, which are containers for rows. 
- Examples - `Apache Casandra`, `Apache HBase` etc.

## Graph Databases 
- These databases are used to store data whose relations are best represented in a graph ( like parent-child relationship of aadhaar etc.)
- Data is saved in graph structures with nodes (entities), properties (information about the entities), and lines (connections between the entities).

# SQL - Different Databases

## MySQL vs PostgreSQL
- [PostgreSQL is twice as fast as MySQL](https://itnext.io/benchmark-databases-in-docker-mysql-postgresql-sql-server-7b129368eed7).

# References
- [Groking the System Design](https://www.educative.io/courses/grokking-the-system-design-interview/YQlK1mDPgpK)
- [SQL vs NoSQL](https://www.interviewbit.com/blog/sql-vs-nosql/)
- [Scaling Your Amazon RDS Instance Vertically and Horizontally](https://aws.amazon.com/blogs/database/scaling-your-amazon-rds-instance-vertically-and-horizontally/)
- [10 use cases where NoSQL will outperform SQL](https://www.networkworld.com/article/2999856/10-use-cases-where-nosql-will-outperform-sql.html)
- [Why is NoSQL faster than SQL?](https://softwareengineering.stackexchange.com/questions/175542/why-is-nosql-faster-than-sql)
- [Why and How to Migrate from Apache Cassandra to Amazon DynamoDB - AWS Online Tech Talks](https://www.youtube.com/watch?v=WuDGvG_4kC8)