### **HTTP**

Based on [Lecture 0 - HTTP](https://www.youtube.com/watch?v=8KuO4r5CHjM) of the series _Building Dynamic Websites_ by David J. Malan

What happens when you enter a website?

IP address - identifies a server or computer on the internet. A number of the following form:  w.x.y.z (numbers from 0-255). 32 bits
version 4 to 6. 128 bits u.v.w.x.y.z
what are the other rules?

How do they know which address it is?
Domain name lookup -
Domain Name System - converts domain / host names into addresses and vice versa
helping routing of email, validation of ownership

Hierarchy of DNS systems - 
Root servers - spread across continents. Tell you who knows the relevant server

ISP - An ISP, or Internet Service Provider, is a company that provides individuals and businesses with access to the internet

HTTP - Protocol / schema
Packet
Requests
Headers

defaultgateway /  router - they know how to get from A to B or who to pass it to

language html, rendersit


why the www, :// and all that on the url
URL components: Protocol://hostname.domain name.Top Level Domain (TLD)/ path - specifies path / folder to access
how to configure it to work without missing some parts?

Need a server to host the website
public vs private 
how do routers work
cable or DSM modem

Private ip addresses - 192.168.x.x Addresses that are never given out that aren't given to the public
172.16.y.y
class A - 10.z.z.z
they aren't uniquely identifiers. Can't use them to get the website out in the world


Web server - apache

Port forwarding - 
TCPIP - Transmission Control Protocol (Standard that servers use to move data around) Internet Protocol (set of conventions that governs how numeric addresses relate to computers)
govern how data can be transmited
transport layer, ip layer, application layer,

port numbers -
80 for HTTP service
traffic comes in in ports, need ways to identify what to do with the data
firewall?
443 for HTTPS

security mechanism and how ports help

it's hard to set up on your home set up and it comes with many drawbacks, such as you always need to have it plugged in, weird host name, many IPS do not allow it, and such

domain name registrars to buy domain names

how to use the domain name? - tell the registrar the IP address of the DNS server. Convention is to have a primary and secondary
Web hosting companies can help for this
- hard drive - storage
- connections to the internet
- pool of IP addresses
- RAM
- server and everything necessary to keep it alive

NS Record -
database with key-value pairs of domain name - ip address
can also be
	A record domain name - ip address
	CName: Canonical name, uses an alias domain name - to domain name
	Mx: Mail exchange record - mail server - ip address. Can have many and that go by priorities 
	
	

**Topics**
DNS
Private IP Address
TCP IP
Port 80
URLs
Port numbers
Where do you purchase domains
Namecheap
DNS Records
Cnames
Prerequisites
Lecture Structure
PHP
XML
Scalability

Projects
DreamHost
Virtual Hosting
Virtual Private Servers


