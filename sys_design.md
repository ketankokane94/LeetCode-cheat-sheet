
# Key concepts to be known for sys design 

## Load balancer

1. operates at L4 or L7 of OSI model, most operate at L7
2. Round Robin / load based

    * NGINX
    * HAProxy

## caching

1. can be distributed or central
2. should not be the source of the truth
3. Should be small

        1. memcached 2. reddis

### CDN for media caching

*Mostly based on geographically*

## database

1. primary key 2. Indexes
* Data consistency is a big issue with multiple db nodes

### DB replication (salve master)

* One master many slaves.
* For strong consistency always read from the master or memcache data, as replications may not have been updated. 
(E.G. User updated his profile and now immediately wants to see the changes)
* can use caching and replication to scale out reads. (with multiple copies we can logically scale to infinite reads)

#### Problem of scaling DB writes

##### Sharding

1. Vertical sharding   2. Horizontal sharding  

## Servers

1. Web server(Stateless) - can be scaled using the load balancer
2. Db server - can use caching and replication to scale out reads. (with multiple copies we can logically scale to infinite reads)
3. Images server (asset server) - CDN

## No Sql Servers

* Cannot do range query as they are mainly key value pairs and are not relational use.

1. MongoDB 2. Amazon

## ABCD of Sys Design

* A : Ask good questions
    1. What features to work on (define minimal viable product)
    2. How much the system to scale (Get sense of how much data)

* B : BuzzWords (DON'T USE THEM DURING THE INTERVIEW)

* C : Clear and organized Thinking
    * Have a 50K ft view of the system

* D : Drive discussion
    * Talk 80 % of the time in the sys design interview

*Features: Ask interviewer about the features of the system. Its important to define those as much as possible early on
*Defining API: What are the API's, who would be calling them and how they are going to use it

**First 10 mins of the interview can be thought of OOD** 

* Availability: Once you have a system ready, work on how are going to make and keep in available, think of scalability
* Latency Performance: If background then dont care
* scalability: Is the system/API going to work for 1 million users
* Durability: How important it is to not lose any data
* Class diagrams: This is basically for OOD


### CAP thorem

### ACID vs BASE

### Partitioning/Sharding data

* How do you split your data
* consistent hashing is one technique

### Optimisitic vs pessimitic locking

### Strong vs Eventual consistency

### Retional vs NoSQL

### NoSQL

1. K, V based
2. Document based
3. Graph based

### DNS Lookup

* Convert URL/endpoint to an ip-address

### PKI (Public Key Infrastruture)

### PAKOS

* Leader election over distributed hosts

