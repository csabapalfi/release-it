# General Design Issues

# Networking

## Multihomed servers

* a server having more than one NIC
* multilple prod + backup/admin network
* bonding= two NIc sharing the same IP (careful with routing loops)
* By default, an application that listens on a socket will listen for connection attempts on any interface
* conﬁgurable properties to deﬁne to which interfaces the server should
bind

## Routing

* with multiple interface it can get tricky
* keep track of destination name, address, desired route for each integration point

## Virtual IPs

* two meanings:
* Load balancers use virtual IPs to multiplex many services (each with its own IP address) onto a smaller number of physical interfaces
* Generally speaking, it means an IP address that is not strictly tied to an Ethernet MAC address

# Security

## The Principle of Least Privilege

* any app -> lowest level of privilege needed to accomplish its task
* webserver behind loadbalancer listening on port greater than 1024
* <1024 apache uses privilige separaten (gives up root once socket is open)

## Conﬁgured Passwords

* prod passwords separately.

# Availability

## Gathering Availability Requirements
* actual cost vs. avoided losses

## Documenting Availability Requirements
* SLAs in terms of speciﬁc features or functions of the system
* SLA can't be greater than the worst of the external dependencies involved in a feature
* SLA should deﬁne what device or devices will be monitoring the availability of the feature (e.g by executing synthetic transactions)
* checked how often?
* acceptable response time?
* from how many locations?
* how will it be recorded?

## Load balancing
* Load balancing is all about distributing requests across a pool or farm of servers to serve all requests correctly in the shortest feasible time

### DNS Round-Robin
* simply associates several IP addresses with the service name
* drawback: all the servers in the pool must be “routable". (their front-end IP addresses are visible and reachable from clients) -> security risks
* drawback2: putting too much control in the client’s hands -> no way to remove host from the cluster, can't guarantee even distribution
* has to bypass Java DNS caching if used for backend services

### Reverse proxy
* A normal proxy multiplexes many outgoing calls into a single source IP address.
* A reverse proxy server does the opposite: it demultiplexes calls coming in to a single IP address and fans them out to multiple addresses.
* does its magic at the application layer. As such, they are not transparent
* can be configured to cache static content.
* the biggest reverse proxy server “cluster” in the world is Akamai. (a large
number of servers located near the end users,)
* Because the reverse proxy server is involved in every request, it can
get burdened very quickly
* keep track of origin health
* X-Forwarded For header

### Hardware Load Balancer
* expensive


## Clustering

Load balancing does not require collaboration between the separate servers. When the servers are aware of each other and actively participate in distributing load, then they form a cluster. some communication overhead in heartbeats and state synchronization

* active/active - loadbalanced, all serving traffic
* active/passive - redundancy, in case of failure
* WebLogic, MSSQL has it built-in

# Administartion

* easy to administer, it will have good uptime
* users and devs - releases add value, ask admins/ops
* new release, new failure modes, old logs might disappear
* make your ops guys happy, DEVOPS

## "Does QA Match Production?"
* why the issue wasn’t discovered during testing?
* guaranteed to ﬁnd something different (hostnames and IPs at the very least)
* the expensive part is ﬁguring out which discrepancies are known, expected, and harmless and which are unexpected and risky
* tipcally confgiuration and topology differences
* Topology is the number and connectivity of the servers and applications
* sharing hosts that'll be different in prod. (solution: virtualize in QA)
* Zero, One, Many - if prod has twelve run at least two in QA

## Conﬁguration Files
* enterprise system: loads of configuration files
* config paramater names has to be unambigous
* internal config (bean wiring) vs application config (hostnames)
* put your shit in version control
* conﬁguration properties are part of the system’s user interface

## Start-up and Shutdown
* logged startup with logging errors
* start-up sequence must complete successfully before the application starts accepting work
* fail fast
* clean shutdown, waiting for in-flight transactions (with timeout) but not accepting new work

## Administrative Interfaces
* if GUI provide scriptable alternative
