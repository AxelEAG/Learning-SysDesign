Based on [Harvard's CS75 Scalability Lecture](https://www.youtube.com/watch?v=-W9F__D3oY4) of the series _Building Dynamic Websites_  by David J. Malan

_For more concepts and definitions can look at the other docs in the folder._

What if your service quickly grows in popularity? How would you handle that?
**Answer:** Scalability

Scaling a service can take many forms, and often times, it is about repeating a same idea at different magnitudes. Further, any change comes with its ups and downsides. This lecture will explore an overview of all of this.

**Vertical Scaling** (7:30 - 13:30)
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

**Horizontal scaling** (13:30 - 15:00)
As mentioned, vertical scaling runs into some heavy hardware limitations. So, to bypass that, horizontal scaling can be used. In short, it consists of increasing machines or servers and distributing tasks among them.
- **Pros:** 
	- Can use cheaper hardware.
	- Higher expansion capacity - can always add more servers.
- **Cons:** 
	- Higher complexity - need to coordinate all services.
	- Data needs to be consistent too.
	- Communication between servers adds latency

To address how this coordination between servers may occur, new components need to be added. Among the most common ones is the load balancer.

**Load balancing:** (15:00 - 29:00)
	allows to distribute / balance the traffic load to the servers
	Open to the public / client
	Decides who to send it to - what are the strategies?
		Round Robin - 
			BIND example - have multiple sequential IP addresses, so by default it would return one after another upon requests
			downside - by pure luck one server could get overloaded. Caching can store much more than necessary
		Dedicated servers - by tasks / available uses
		Busyness
		Load? Busiest to least busy
	Sends request to server and receives a response
	Sends response back into the client

Load balancing tech (44:00 - )
Software: ELB, HAProxy, LVS
Hardware: Barracuda, Cisco, Citrix, F5

**Shared session state** (29:00-34:00)

Load balancing breaks session state,
how to solve? Sessions are typically implemented per server. How to share it?
store session state somewhere else, not on the server
what if this somewhere else breaks?
solved shared state but sacrificed robustness / redundancy

Redundancy
uptime if everything breaks

**Redundant Array of Independent Disks (RAID)** (34:00 - 40:30)
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

**Shared state** - FC, iSCSI, MySQL, NFS,
cookies? - store which server to get in - what if it's down, still could cause unbalanced load to one server, 
what if IP changes and have to make IP public store key instead have actual IP on load balancer

It's still a single point of failure 
How to share state?

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