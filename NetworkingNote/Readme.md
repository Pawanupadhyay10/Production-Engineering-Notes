
# Networking

There are two major models in networking namely
a) OSI Model
b) TCP/IP 5 layer model

<p align="center">
  <img src="images/network.jpg" />
</p>


### Terms that can be used in the future

Single collison domain: A domain in which network devices cannot transmit at the same time without causing a collison.

### Ethernet and MAC Layer

**CSMA/CD** : Carrier sense multiple access detects the channel for collision and if detected resends the message.

**MAC Address**: A globally unique identifier attached to an individual network interface.

It is a 48 bit number and the possibilities are 2^48 and that means it is possible to have globally unique identifiers for the mac addresses.

Now the mac address is split into 6 octets as shown below

<p align="center">
  <img src="images/MAC.png" />
</p>

The last three octets is upto the manufacturer.

### Unicast Multicast and broadcast

Unicast: In unicast there is only one receiver.

Broadcast: In broadcast the message is sent to all devices. This is accomplished by using a broadcast address. FF:FF:FF:FF:FF

Let us take a look at the ethernet frame

<p align="center">
  <img src="images/ethernet_frame.png" />
</p>

# Network Layer

### IP Addresses

It is a 32 bit number. These are described in 4 octets, and therefore can represent 0 to 255 numbers. This is known as dotted decimal notation

There are two types of addresses:

a) Dynamic IP Addresses

b) Static IP Addresses

<p align="center">
  <img src="images/ipdatagram.jpg" />
</p>

Version: Version number like IPV4

Header len: 20 bytes

Type of service : Quality of service details etc

Total Length field : This indicates the length of the datagram. It is 16bits

Flags: States whether the datagram is fragmented and the fragment offset is 

TTL : States how many hops the datagram will live before it dies out

upper layer: It defines the transport layer protocol to be used, the most common ones are TCP and UDP.


An IP address is split up into a network id and a host ID.

### Subnetting 

The IP Address space is divided into three major classes

Class A : NetworkID: 8 bits
Class B : NetworkID: 16 bits
Class C : NetworkID: 24 bits

Because an IP address is limited to indicating the network and the device address, IP addresses cannot be used to indicate which subnet an IP packet should go to. Routers within a network use something called a `subnet mask` to sort data into subnetworks.

For a real-world example, suppose an IP packet is addressed to the IP address 192.0.2.15. This IP address is a Class C network, so the network is identified by "192.0.2" (or to be technically precise, 192.0.2.0/24). Network routers forward the packet to a host on the network indicated by "192.0.2."

Once the packet arrives at that network, a router within the network consults its routing table. It does some binary mathematics using its subnet mask of 255.255.255.0, sees the device address "15" (the rest of the IP address indicates the network), and calculates which subnet the packet should go to. It forwards the packet to the router or switch responsible for delivering packets within that subnet, and the packet arrives at IP address 192.0.2.15 (learn more about routers and switches).

<p align="center">
  <img src="images/subnetting.png" />
</p>


### CIDR

<p align="center">
  <img src="images/CIDR.png" />
</p>


### VLAN

In essence, a VLAN is a collection of devices or network nodes that communicate with one another as if they made up a single LAN, when in reality they exist in one or several LAN segments. In a technical sense, a segment is separated from the rest of the LAN by a bridge, router, or switch, and is typically used for a particular department. This means that when a workstation broadcasts packets, they reach all other workstations on the VLAN but none outside it.


### DNS

DNS Servers resolve hostnames into IP addresses. There are 4 types of dns servers

a) DNS Recursor --> It is responsible for hunting down the IP address for the hostname. It searches for the authoritative nameserver and returns back the IP address. It caches the search results.

b) Root Nameserver
c) TLD Nameserver
d) Authoritative Nameserver --> It is the last in the foodchain of the dns lookups and will return the value for the hostname

The 8 steps in a DNS lookup:
* A user types ‘example.com’ into a web browser and the query travels into the Internet and is received by a DNS recursive resolver.
* The resolver then queries a DNS root nameserver (.).
* The root server then responds to the resolver with the address of a Top Level Domain (TLD) DNS server (such as .com or .net), which stores the information for its domains. When searching for example.com, our request is pointed toward the .com TLD.
* The resolver then makes a request to the .com TLD.
* The TLD server then responds with the IP address of the domain’s nameserver, example.com.
* Lastly, the recursive resolver sends a query to the domain’s nameserver.
* The IP address for example.com is then returned to the resolver from the nameserver.
* The DNS resolver then responds to the web browser with the IP address of the domain requested initially.
* Once the 8 steps of the DNS lookup have returned the IP address for example.com, the browser is able to make the request for the web page:


**3 types of DNS queries:**

* Recursive query - In a recursive query, a DNS client requires that a DNS server (typically a DNS recursive resolver) will respond to the client with either the requested resource record or an error message if the resolver can't find the record.
* Iterative query - in this situation the DNS client will allow a DNS server to return the best answer it can. If the queried DNS server does not have a match for the query name, it will return a referral to a DNS server authoritative for a lower level of the domain namespace. The DNS client will then make a query to the referral address. This process continues with additional DNS servers down the query chain until either an error or timeout occurs.
* Non-recursive query - typically this will occur when a DNS resolver client queries a DNS server for a record that it has access to either because it's authoritative for the record or the record exists inside of its cache. Typically, a DNS server will cache DNS records to prevent additional bandwidth consumption and load on upstream servers.

**What are the most common types of DNS record?**
* A record - The record that holds the IP address of a domain. Learn more about the A record.
* AAAA record - The record that contains the IPv6 address for a domain (as opposed to A records, which list the IPv4 address). Learn more about the AAAA record.
* CNAME record - Forwards one domain or subdomain to another domain, does NOT provide an IP address. Learn more about the CNAME record.
* MX record - Directs mail to an email server. Learn more about the MX record.
* TXT record - Lets an admin store text notes in the record. These records are often used for email security. Learn more about the TXT record.

