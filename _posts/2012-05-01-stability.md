---
layout: post
title: Stability
---

## Definitons

* A transaction is an abstract unit of work processed by the system.
* I use system when I mean a collection of hosts, applications, network segments, power supplies, and so on, that process transactions from end to end
* A resilient system keeps processing transactions, even when there are transient impulses (getting Slahdotted), persistent stresses (slow payment prcessing response), or component failures disrupting normal processing.

## Failure modes

* longevity tests
* failure mode: how system behaves when shit hits the fan
* safe failure modes that contain the damage and protect the rest of the system.
* crack stoppers
* designed failure modes

## Cracks propagate

* SQLException because of failover -> exhausts conn pool -> brings down down the shole system
* create more connections if the pool was exhausted
* requesting threads block indefinitely -> no timeout
* RMI client without a timeout -> set a timeout on the RMI sockets (custom socket factory)
* queues
* The more tightly coupled the architecture, the greater the chance that this coding error can propagate

## Chain of Failure

* High levels of complexity provide more directions
for the cracks to propagate in
* Tight coupling accelerates cracks

