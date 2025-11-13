### **Scalability**

Based on [Harvard's CS75 Scalability Lecture](https://www.youtube.com/watch?v=-W9F__D3oY4) of the series _Building Dynamic Websites_  by David J. Malan

_For more concepts and definitions can look at the other docs in the folder._

What if your service quickly grows in popularity? How would you handle that?
**Answer:** Scalability

Scaling a service can take many forms, and often times, it is about repeating a same idea at different magnitudes. Further, any change comes with its ups and downsides. This lecture will explore an overview of all of this.

### **Vertical Scaling** (7:30 - 13:30)

The first line of defense thanks to its simplicity is vertical scaling. It consists of increasing resources (CPU, RAM, Disk, etc.) of the server or machine in use.
- **Pros:** 
	- It's the simplest approach - no need to redesign the system.
	- Works great for small to medium scale.
- **Cons:** 
	- Limited by cost and hardware limits — one machine can only get so powerful.
    - Hardware upgrades may require downtime.

Increasing resources may look like:
	 - **CPU:** 
		 - Adding cores: It can handle more threads/processes in parallel.
		 - Increasing clock speed: each core can execute instructions faster.
	 - **RAM:** 
		 - Increasing memory allows more data to be accessed more readily than from disk.
	 - **Disk:**
		 - Increasing RPMs, which equates to faster reads and writes.
		 - Hard vs solid state drive
		 - Improving interfaces: SAS (Serial Attached SCSI) > SATA (Serial ATA)> PATA (Parallel ATA)

### **Horizontal scaling** (13:30 - 15:00)

As mentioned, vertical scaling runs into some heavy hardware limitations. So, to bypass that, horizontal scaling can be used. In short, it consists of increasing the number of machines or servers and distributing tasks among them.
- **Pros:** 
	- Can use cheaper hardware.
	- Higher expansion capacity - can always add more servers.
- **Cons:** 
	- Higher complexity - need to coordinate all services.
	- Data needs to be consistent too.
	- Communication between servers adds latency

So this seems to be very beneficial to scaling, but, how may one go about coordinating such servers? Among the most common solutions, it's the load balancer.

### **Load balancing** (15:00 - 29:00)

A **load balancer** is a type of **reverse proxy** that distributes incoming client requests across servers to prevent any single one to become overloaded. It acts as the entry point for the public, hiding and protecting the backend servers from direct user access.

**How load balancers work**

When a client sends a request, it reaches the load balancer first. It then decides which server should handle the request based on some balancing strategy. It then forwards the request to the server, receives the response, and routes it back to the client.

In this way, the load balancer:
* Improves performance by distributing the workload.
* Increases reliability and availability (if one server goes down, traffic can be rerouted).
* Enhances security by isolating the backend servers from direct access.

**Common load balancing strategies**
- **Round Robin** – The simplest strategy: requests are distributed sequentially across servers.
    - _Pros:_ Easy to implement and works well for servers of similar capacities.
    - _Cons:_ Doesn’t account for server load — one server might get overwhelmed.

- **Least Connections / Least Load** – Sends traffic to the server currently handling the fewest active connections or least load.
    - _Pros:_ Adapts to server usage.
    - _Cons:_ Requires real-time monitoring, which adds overhead.

- **Hashing (e.g., IP Hash)** – Hashes the client IP or session ID to route them to the same server.
    - _Pros:_ Good for session persistence (“sticky sessions”).
    - _Cons:_ Uneven distribution if hash space isn’t balanced.

- **Weighted Round Robin / Weighted Least Connections** – Assigns weights to servers based on capacity (e.g., CPU, RAM), sending more requests to stronger machines.
    - _Pros:_ Makes efficient use of the stronger servers.
    - _Cons:_ Requires careful tuning of weights.
    
- **Task-Based Routing (Functional Partitioning)** – Has dedicated servers for tasks and routes requests accordingly.    
    - _Pros:_ Specialization improves efficiency.
    - _Cons:_ More complex architecture; each tier must scale independently.

**Load Balancing Technologies** (44:00 - 45:00)
Load balancers can be **software-based** or **hardware-based**.
- **Software Load Balancers**
    - **HAProxy** – Open-source, high-performance TCP/HTTP load balancer widely used in production.
    - **LVS (Linux Virtual Server)** – Kernel-level load balancing for large clusters.
    - **ELB (Elastic Load Balancer)** – AWS-managed load balancer that automatically scales and integrates with cloud services.
- **Hardware Load Balancers**
    - **F5**, **Citrix**, **Cisco**, **Barracuda**, and others provide specialized devices optimized for high throughput and security.

When we add a load balancer and multiple servers, a new problem shows up: **session state**. 
That is, as traffic is distributed to different servers, how can the session state be kept?

### **Shared session state** (29:00-34:00)

A **session** keeps track of information about a user across multiple requests (like whether they’re logged in, what’s in their cart, or what page they were on).

Normally, this data is stored **in memory on the server** that the user’s request hits. So, with a single server this is fine. But oncer there are multiple servers behind a load balancer, a user’s next request might go to a _different_ server — one that doesn’t have their session data. So, suddenly, all their new data might seem to disappear.

**How to solve it**
There are a few main ways to handle shared session state:
1. **Stickiness (Session Affinity):** Keep sending the same user to the same server.
	* **How:** The load balancer can track users by IP, or store a session ID in a **cookie** that points to a specific server.
	- **Pros:** Simple and fast as there's no need to share session data.
	- **Cons:** If that server goes down, the session is lost. It can also cause uneven load (some servers may get more users or 'power' users that store a lot).
2. **Centralized Session Store:** Store sessions in a shared database or cache.    
    - **How:** Can use any of the following tools.
	    - **Databases:** MySQL, PostgreSQL.
	    - **Caches:** Redis, Memcached.
	    - **File Systems:** NFS (Network File System), iSCSI, Fibre Channel (FC).    
	- **Pros:** Any server can retrieve a user’s session so no need to distribute to the 'correct' one.
	- **Cons:** The session store itself becomes a **single point of failure**. 
3. **Client-Side Sessions:** Store session data directly on the client, instead of the server.
	* **How:** Put the session info directly in the user’s **cookie** (often as a token or encrypted blob).
	- **Pros:** No need for shared storage (stateless servers).
	- **Cons:** Can’t store much data; must be secure (never trust client input); and every request carries that data around, increasing network overhead.

Despite there being multiple solutions, one can see again the pattern of them having upsides and downsides. A single point of failure is a big one. But, what if one could add more servers or databases? 

That is, one can fix that with **replication** or **redundancy**, but that adds complexity. So, in the next section this will be explored for the centralized session, and how to add replication or redundancy.



Redundancy
uptime if everything breaks

**Redundant Array of Independent Disks (RAID)** (34:00 - 40:30)

What's redundancy or replication

What's RAID
Variants - assume multiple hard drives
RAID0 - 2 hard drives of identical size, striping data between them to allow faster writing, but only get the size of 1
RAID1 - 2 hard drives, but mirror data, performance overhead but now have redundancy
RAID5 - 1 drive for redundancy,
RAID6 - 2 drives for redundancy
RAID10 - Combination of 0 and 1, so 4 hard drives, get both striping and duplication.

There's still issues: 
	upside - decrease probability of downtime
	downside - still have failing pieces: electricity, RAM, motherboard,

shared storage tech ([42:00](https://www.youtube.com/watch?v=-W9F__D3oY4&t=2520s)) 
Actual data centers servers
have multiple hard drives, ram, and power supplies (can pull it out and put a new one in)

Database replication (43:00 - 44:00 &)

Have copies of the servers!
Replication

**Caching (53:00 -)**
.html - straight up save the whole compiled code / static content and spit it out. Web servers are pretty good at this. Downside: storing a lot of space and memory. Lots of repeated stuff. To change something have to change everything - have to replace or regenerate tens of thousands of files.

MYSQL query cache - saves queries results and gives them back

**memcached - (1:00:00)**
mechanism that stores whatever you want in RAM

key-value storage mechanism that caches into RAM

issue: what if it's full? / run out of RAM
garbage collection - least recently used
or expire objects


optimizing mySQL

myISAM - full table locks
InnoDB - supports transactions

storage engine - underlying format to store DB data

**Replication (1:11-)**
Master-Slave - master where reads and writes are done, while slaves copy it
	Pros: Have identical backups - redundancy. Can do reading from slaves
	Cons: Slower writes and single point of failure for writes (when master fails)
Master-Master - can write on either, copy it on the other, slaves copy it all.
	Pros: 
	Cons:

1:16-1:21
Load-balancing + replication: 
Client -> Load Balancer -> Web Servers 
	-> read queries -> Load Balancer -> MySQL Slaves
	-> write queries -> MySQL Master -> Replication on Slaves


Web servier tiers
Multi tier architecture

Single points of failure - look at bottleneckes
Load balancing: Active: active
send heart beats - if one stops hearing them, other gets in charge
active: passive - detects no more heart beats from active, replace it

**Partitioning** (1:21 -1:24)
have different server for each school (for facebook)
Scale horizontally
catch: what if wants to connect between networks?
common in DBs
balance load on high level info

High Availability - service checking on the other and can take on the whole load if one fails


Ensuring you not only have scalability, but redundancy, higher probabilities of uptime, resilience against failure,

(1:33 - 1:39)
Data center redundancy - the whole thing could go down
	how to distribute load?
	DNS! Geography based load balancing
	CDN

Same ideas at different scales

**Security** 1:40-1:45
Outside to data center
tcp:40, 443
SSL
SSH:22, SSL VPN,

data center to LBs: Only data center
unencrypted - faster
web server to DB: SQL Queries - TCP 3306 (MySQL port number)

Firewall?
Networking concepts
Principle of least priviledge - only have doors that people should have access to





VPS? - review first 7mins

Web Hosts - bluehost, dreamhost, go daddy, host gator, pair networks

Features to expect:
	Accessibility - what if certain IPs are blocked - not everyone can use it
	SFTP - Secure File Transfer Protocol - all traffic is encrypted. Important for user data
	Virtual hosting issues? - resource contention, and others may be able to access

Alternatives
Virtual Private Server - VPS
DreamHost, Go Daddy, Host Gator, Linode, Pair Networks, Slicehost, VPSLAND
get own copy of OS
super fast server and chop it into many servers with hypervisor
virtual machines on a virtual machine
get own slice, sys admins still have access to VM, files, etc.
even more privacy? need to operate their own server


**Topics covered:**
    - Vertical scaling (7:30 - 13:30)
    - Horizontal scaling (14:00- )
    - Caching 
    - Load balancing 
    - Database replication
    - Database partitioning

**Timeline breakdown**
	- horizontal scaling ([13:00](https://www.youtube.com/watch?v=-W9F__D3oY4&t=780s) - [21:00](https://www.youtube.com/watch?v=-W9F__D3oY4&t=1260s)) 
	- load balancing & caching ([21:00](https://www.youtube.com/watch?v=-W9F__D3oY4&t=1260s) – [29:00](https://www.youtube.com/watch?v=-W9F__D3oY4&t=1740s)) 
	- shared session state ([29:00](https://www.youtube.com/watch?v=-W9F__D3oY4&t=1740s) – [34:00](https://www.youtube.com/watch?v=-W9F__D3oY4&t=2040s)) 
	- RAID ([36:00](https://www.youtube.com/watch?v=-W9F__D3oY4&t=2160s) – [40:00](https://www.youtube.com/watch?v=-W9F__D3oY4&t=2400s)) 
	- shared storage tech ([42:00](https://www.youtube.com/watch?v=-W9F__D3oY4&t=2520s)) 
	- database replication ([43:00](https://www.youtube.com/watch?v=-W9F__D3oY4&t=2580s)) 
	- load balancing tech ([44:00](https://www.youtube.com/watch?v=-W9F__D3oY4&t=2640s) – [45:00](https://www.youtube.com/watch?v=-W9F__D3oY4&t=2700s)) 
	- session affinity ([46:00](https://www.youtube.com/watch?v=-W9F__D3oY4&t=2760s) – [51:00](https://www.youtube.com/watch?v=-W9F__D3oY4&t=3060s)) 
	- in-memory caching ([59:00](https://www.youtube.com/watch?v=-W9F__D3oY4&t=3540s) – [1:00](https://www.youtube.com/watch?v=-W9F__D3oY4&t=60s)) 
	- data replication – active:passive ([1:11](https://www.youtube.com/watch?v=-W9F__D3oY4&t=71s) - [1:14](https://www.youtube.com/watch?v=-W9F__D3oY4&t=74s)), 
	- active:active ([1:16](https://www.youtube.com/watch?v=-W9F__D3oY4&t=76s) - [1:21](https://www.youtube.com/watch?v=-W9F__D3oY4&t=81s)) 
	- partitioning ([1:21](https://www.youtube.com/watch?v=-W9F__D3oY4&t=81s) – [1:34](https://www.youtube.com/watch?v=-W9F__D3oY4&t=94s)) 
	- data center redundancy ([1:33](https://www.youtube.com/watch?v=-W9F__D3oY4&t=93s) – [1:39](https://www.youtube.com/watch?v=-W9F__D3oY4&t=99s)) 
	- security ([1:39](https://www.youtube.com/watch?v=-W9F__D3oY4&t=99s) – [1:44](https://www.youtube.com/watch?v=-W9F__D3oY4&t=104s))