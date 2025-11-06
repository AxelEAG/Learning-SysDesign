Based on [Harvard's CS75 Scalability Lecture](https://www.youtube.com/watch?v=-W9F__D3oY4)

What if your service quickly grows in popularity? How would you handle that?
**Answer:** Scalability
	- **Vertical scaling:** increase resources of the server / machine (CPU, RAM, Disk, etc.). 
		- Benefits: simplest approach, works great for small scale .
		- Cons: limits on how good one machine can be or affordability.
	- **Horizontal scaling:** increase machines / servers and distribute tasks among them
		-  Benefits: Cheaper, much higher capacity for expansion.
		-  Cons: Higher complexity - need to coordinate everything.
	- 

Notes (In Progress)

**Vertical Scaling** (7:30 - 13:30)
Vertical scaling consists of increasing resources (CPU, RAM, Disk, etc.) of the server or machine in use.
- **Upsides:**
- **Downsides:**

Disk  - PATA, SATA, SAS, RAID
rpms and meaning? inside disks there's a disk that spins
dbs write to disk so it helps to read and write faster
solid state drive - faster electrically than mechanical
RAM 

actually schedules tasks and does them in order - serially vs parallel
multiple threads / processes?
we don't know what to do with resources?

**Horizontal scaling** (13:30 - 15:00)
HTTP 
DNS - Domain Name System - Translates host names to IPs
IP addresses? public vs private - review other lectures? others cannot address them or cannot be contacted by enemies. 
TCP
TTL - Time to live
nslookup command
Also, world kinda running out of Ip Addresses - look up


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

Shared state - FC, iSCSI, MySQL, NFS,
cookies? - store which server to get in - what if it's down, still could cause unbalanced load to one server, 
what if IP changes and have to make IP public store key instead have actual IP on load balancer

It's still a single point of failure 
How to share state?

Database replication (43:00 - 44:00 &)

Have copies of the servers!
Replication

Caching (53:00 -)
.html - straight up save the whole compiled code / static content and spit it out. Web servers are pretty good at this. Downside: storing a lot of space and memory. Lots of repeated stuff. To change something have to change everything - have to replace or regenerate tens of thousands of files.

MYSQL query cache - saves queries results and gives them back
memcached - (1:00:00)



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