
## Important Points
- `URL Shortening Service` is a read-heavy system. `100:1` ratio between read and write.

# Functional Requirements
- Shortening: Take a url and return a much shorter url. Ex: http://www.interviewbit.com/courses/programming/topics/time-complexity/ => http://goo.gl/GUKA8w/
- Redirection: Take a short url and redirect to the original url.
Ex: http://goo.gl/GUKA8w => http://www.interviewbit.com/courses/programming/topics/time-complexity/"
- Custom url: Allow the users to pick custom shortened url.
Ex: http://www.interviewbit.com/courses/programming/topics/time-complexity/ => http://goo.gl/ib-time"
- Analytics: Usage statistics for site owner.
Ex: How many people clicked the shortened url in the last day?
Gotcha: What if two people try to shorten the same URL?

# Non-Functional Requirements
- The system should be highly available. This is required because, if our service is down, all the URL redirections will start failing.
- URL redirection should happen in real-time with minimal latency.
- Shortened links should not be guessable (not predictable).

# Read vs Writes - URL Shortening is a read-heavy
- There will be lots of redirection requests compared to new URL shortenings.
- Let’s assume a 100:1 ratio between read and write.

# High Level Design

<img title="URL Shortener" alt="Alt text" src="assets/URL Shortener - HLD.drawio.png">

# REST APIs
- `createURL(api_dev_key, original_url, custom_alias=None, user_name=None, expire_date=None)`
- `deleteURL(api_dev_key, url_key)`
- `RedirectionAPI(hash) {redirect_to url_mapping[hash]}

# How do we detect and prevent abuse? 
- To prevent abuse, we can limit users via their `api_dev_key`.
- Each `api_dev_key` can be limited to a certain number of URL creations and redirections per some time period (which may be set to a different duration per developer key).

# Database Schema

## URL table
- Hash ( PK )
- Original URL
- Creation Date
- Expiration Date
- User ID

# Users-Table
- Name
- Email
- DateOfBirth
- CreationDate
- LastLogin

# Which database to use? - SQL vs NoSQL
- `NoSQL` can be used here since we are anticipating a billion of rows & no relationship is needed between rows.
- Read more about [NoSQL vs SQL](../DesignComponents/SQLvsNoSQL/ReadMe.md).

# Key Generation Service
- Whenever we want to shorten a URL, we will take one of the already-generated keys `UnusedKeys` and use it ( & move it to `UsedKeys` table )
- Not only are we not encoding the URL, but we won’t have to worry about `duplications or collisions`.

## Database Tables
KGS can use two tables to store keys:
- `Unused keys` - One for keys that are not used yet
- `Used keys` - One for all the used keys

## Cache Memory - Redis
- `KGS` can always keep some keys in memory ( `Redis` ) to quickly provide them whenever a server needs them.
- As soon as `KGS` loads some keys in memory, those would be marked it can move them to the `used keys` table.

## Concurrency Issues
- `KGS` also has to make sure NOT to give the same key to multiple servers.
- Hence, it must `synchronize (or get a transaction lock on)` the Redis data structure, holding the keys before removing keys from it and giving them to a server.

## How can each cache replica be updated?
- Whenever there is a cache miss, our servers would be hitting a backend database.
- Whenever this happens, we can update the cache and pass the new entry to all the cache replicas.

# Open Question
- How to improve latency of write operation? 
  - Instead of 2, we should have 1 database call? 
  - What if Redis goes down?

# Cleanup Service
- If we chose to continuously search for expired links to remove them, it would put a lot of pressure on our database. 
- Instead, we can slowly remove expired links and do a lazy cleanup. 
- Our service will ensure that only expired links will be deleted, although some expired links can live longer but will never be returned to users.

# Telemetry/Analytics
Some statistics worth tracking:
- country of the visitor,
- date and time of access,
- web page that referred the click,
- browser, or platform from where the page was accessed.

## References
- [Groking the System Design](https://www.educative.io/courses/grokking-the-system-design-interview/m2ygV4E81AR)
- [System Design : Scalable URL shortener service like TinyURL](https://medium.com/@sandeep4.verma/system-design-scalable-url-shortener-service-like-tinyurl-106f30f23a82)