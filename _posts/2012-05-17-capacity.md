# Capacity


## Deﬁning Capacity
*  Performance measures how fast the system processes a single transaction
* Throughput describes the number of transactions the system can process in a given time span
* Scalability: 1. how throughput changes under varying loads. 2. modes of scaling supported by a system (adding capacity)
* the maximum throughput a system can sustain, for a given workload, while maintaining an acceptable response time for each individual transaction is its capacity
* session count vs user count

## Constraints
* Difficult to understand nonlinear effects
* In every system, exactly one constraint determines the system’s capacity. -> bottleneck
* Understanding the capacity of any system requires systems thinking, as described by Peter Senge in The Fifth Discipline [Sen90]—
* driving variables (e.g req/sec) 
* Following variables move in response to driving variables (CPU usage)
* Load testing, stress testing, observations of production systems how following variables correlated to each driving variable
* For example, database I/O drives application server response time, which drives web server memory usage
* constraint in your system will be a limit in one of the following variables.
* knee in load-testing charts

##Scalability

* A horizontally scalable system can grow by adding more servers. A vertically scalable system requires upgrades to the existing servers. These are sometimes described as “getting wide” or “getting big.”
* shared-nothing -> easy to scale horizontally

## Summary

* CPU, Storage and bandwidth is NOT cheap
* look for the multiplier effects
* Understand the effects that one layer has on another
* Improving nonconstraint metrics will not improve capacity.
* Place safety limits on everything: timeouts, maximum memory consumption, maximum number of connections, and so on
* Monitor capacity continuously