
# Key concepts to be known for sys design 

## Load balancer

1. operates at L4 : Layer 4 load balancers look at info at the transport layer to decide how to distribute requests. Generally, this involves the source, destination IP addresses, and ports in the header, but not the contents of the packet. 

2. or L7 of OSI model, most operate at L7 : Layer 7 load balancers look at the application layer to decide how to distribute requests. This can involve contents of the header, message, and cookies. Layer 7 load balancers terminate network traffic, reads the message, makes a load-balancing decision, then opens a connection to the selected server. For example, a layer 7 load balancer can direct video traffic to servers that host videos while directing more sensitive user billing traffic to security-hardened servers.

At the cost of flexibility, layer 4 load balancing requires less time and computing resources than Layer 7, although the performance impact can be minimal on modern commodity hardware.

2. Round Robin / load based / Sessions

    * NGINX
    * HAProxy

To protect against failures, it's common to set up multiple load balancers, either in active-passive or active-active mode.


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

* Features: Ask interviewer about the features of the system. Its important to define those as much as possible early on
* Defining API: What are the API's, who would be calling them and how they are going to use it

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


## consistency patterns

1. Weak consistency: VoIP, video chat, RT multiplayer game. For example, if you are on a phone call and lose reception for a few seconds, when you regain connection you do not hear what was spoken during connection loss.

2. Eventual consistency: After a write, reads will eventually see it (typically within milliseconds). Data is replicated asynchronously. EX. DNS, Emails. (Seen in high available systems)

3. Strong consistency: Data is replicated synchronously.  Works well in systems that need transactions. 

## Availability Pattern: 
There are two complementary patterns to support high availability: fail-over and replication.

1. Fail-Over:
* Master - Slave (Active - Passive)
* Master - Master (Active - Active)
* Adds cost of extra hardware

2. replication: 


# Domain Name Systems:
A Domain Name System (DNS) translates a domain name such as www.example.com to an IP address.

Services such as CloudFlare and Route 53 provide managed DNS services


# Outline Use case, constraints and assumptions:

1. Who is the user ?
1. How are they going to use it ?
1. How many users are there ?
1. What does the system do ?
1. What are the ips and ops of the system ?
1. How much data do we expect ?
1. How many requests per second do we expect ?
1. What is the expected read to write ratio ?



## Example

1. Why do we need it ? ( Not required to ask it everytime, its for understanding the system)

1. Requirements and goals of the system
1. Capacity estimation (Should it be this early in the game ? )
1. System API (CRUD API)
1. Database design
1. Basic System Design and Algorithm (This can involve a lot of details)
1. Data partitioning and replication 
1. Cache
1. Load balancer
1. Purging or Cleaning Database





# Key concepts
## Storage:
    1. Can be relational or No SQL (use Relational when ACID is paramount)
    2. Assume a single db server can store 4TB of data (so Number of machines = data / 4TB)
    3. Horizontal sharding (shard based on what attribute)
        * Keeps keys unique by using a key generation service

### DB replication (salve master)

* One master many slaves.
* For strong consistency always read from the master or memcache data, as replications may not have been updated. 
(E.G. User updated his profile and now immediately wants to see the changes)
* can use caching and replication to scale out reads. (with multiple copies we can logically scale to infinite reads)

* use of transactions in SQL to manage concurrency
    1. row level lock
    


## Messaging systems:
    * Need of session service which keeps a track of which user is connected to which server.
    * Use web sockets
    * Need a mechanism to generate messafe sequence


## NewsFeed generation: 
    * Such system have a high requirement of cache 
    * Need a special service to generate the feeds

