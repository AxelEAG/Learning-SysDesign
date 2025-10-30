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

VPS? - review first 7mins

**Vertical Scaling** (7:30 - 13:30)

CPU  - cores, L2 Cache?
Disk  - PATA, SATA, SAS, RAID
rpms and meaning? inside disks there's a disk that spins
dbs write to disk so it helps to read and write faster
solid state drive - faster electrically than mechanical
RAM 

actually schedules tasks and does them in order - serially vs parallel
multiple threads / processes?
we don't know what to do with resources?

**Horizontal scaling** (14:00 - 21:00)
HTTP 
DNS - Domain Name System - Translates host names to IPs
IP addresses? public vs private - review other lectures? others cannot address them or cannot be contacted by enemies. 
TCP
nslookup command
Also, world kinda running out of Ip Addresses - look up
Load balancing: allows to distribute / balance the traffic load to the servers
	Open to the public / client
	Decides who to send it to - what are the strategies?
		Round Robin - 
			BIND example - have multiple sequential IP addresses, so by default it would return one after another upon requests
		Dedicated servers - by tasks / available uses
		Busyness
		Load? Busiest to least busy
	Sends request to server and receives a response
	Sends response back into the client

Redundancy


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