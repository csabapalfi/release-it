# Stability

## Define: transaction, system, resilience

* a transaction is an abstract unit of work processed by the system.
* a system is a collection of hosts, applications, network segments, power supplies... that process transactions from end to end
* a resilient system keeps processing transactions, even when there are 
    * transient impulses (getting Slahdotted)
    * persistent stresses (slow payment processing response)
    * or component failures disrupting normal processing

## Failure modes

* failure mode: how system/components behave when they encounter a failure
* safe failure modes that contain the damage and protect the rest of the system
* resilient systems have designed failure modes

## Cracks propagate

* upstream errors can propage to downstream systems if they're not protected
* example
    * database exception because of failure -> 
    * exhausts database connection pool -> 
    * request handling threads become blocked waiting on connection ->
    * whole system is down

## Chain of Failure

* the more tightly coupled the architecture, the greater the chance that this coding error can propagate
* high levels of complexity provide more directions for the cracks to propagate in
* tight coupling accelerates cracks

