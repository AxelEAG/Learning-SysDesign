
Resource: [Linux Journey](https://linuxjourney.com/)

### Linux History

The **kernel** is the core component of an operating system: it connects hardware with software and manages system resources.


#### Lab: ["Getting started with Linux"](https://labex.io/labs/linux-getting-started-with-linux-446315)
"-" represents parameters to define
**Commands**
	- **echo** - outputs whatever's inputted  
	- **date** - outputs the current date and time
	- **cal** - outputs the calendar
	- **expr** - outputs the evaluation of inputted expression
	- **figlet** - outputs ASCII art out of input 
	- **man** - shows manual
	- **clear** (or **ctr + L**) - cleans terminal

#### Lab: ["Your First Linux Lab"](https://labex.io/labs/linux-your-first-linux-lab-270253)

Linux is case-sensitive on the commands

In Linux, users are organized into groups that determine rights and permissions
	uid - user id
	gid - primary group id
	root is the superuser.
	
In Linux, you typically install software using a package manager.
	**apt** for Debian-based (like Ubuntu)

**Commands**
	- **whoami** - tells you the current username 
	- **id** - gets additional information on user (uid, gid, and groups user is part of)
	- **sudo** (SuperUser DO) - allows to execute commands with administrator privileges
	- **apt** (Advanced Package Tool) - package manager to install apps (ex: *sudo apt install "app"* )
	- **htop** (Hisham' Table of Processes) -  shows 
		- CPU, memory usage and uptime (how long machine has been running)
		- A list of processes (running programs)
		- Options for interacting with it
	