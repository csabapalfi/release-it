---
layout: post
title: Operations
---

* Jumphost: a single machine, very tightly secured, that is allowed to connect via SSH to the production servers.
* ATG - ecommerce platform, DRP-Dynamo Request Protocol (similar to AJP)
* The ability to restart components, instead of entire servers, is a key concept of recovery-oriented computing
* http://roc.cs.berkeley.edu/
* Failures are inevitable and not all of them can be predicted. Human action is a major source of system failures.
* improve survivability in the face of failures: damage containment, automatic fault detection, and component-level restartability

# Transparency

* systems has to expose their internal state somehow

## Perspectives

* historical trending
* future predictions
* present status (dashboard, what has happened)
* instantaneous behavior (JMX inspection, threaddumps)

## Designing for transparency

Accross all applications to avoid ineffective local optimixations
Be careful with coupling and keep monitoring etc. separate as an exoskeleton

## Enabling technologies

* black-box: external monitoring, can be added after e.g. by ops team
* white-box: runs within: e.g. exposing custom stuff via JMX

## Log files

* still the best
* location not good - tiplically symlinks as workaround
* log levels - no debug logs in prod, ideally you have env-spec config anyway
* Error codes in logs -unambigous communicstion between ops and dev
* Human readable
* SessionId, userid, guid in logs (MDC)

## Monitoring systems

* tipically an agent has to be running on the monitored host
* detecting patterns in logfiles, syslog, system metrics, JMX
* agent goes down when a complete host is lost
* monitoring traffic should not cross VLANs that carry public trafﬁc
* gaps in commercial systems: not aware of business features, server might be all ok but customer experience still bad because of other issues (cookier, etc)
* tealeaf -> focusing on customer experience
* usually monitoring systems are already in place when desinging a new application/system
* monitoring standards: SNMP, CIM, JMX

## Operations Database

* collect operation data from logs and monitoring in a DB
* logs database - Splunk
* maybe also implement an API so apps can add data to the opsDB (probably better off with async/decoupled writes)

## Supporting processes

* An effective feedback process can be described as "acting responsively to meaningful data."
* Plan-Do-Check-Act or Observe-Orient-Decide-Act

# Adaptation

* The true birth of a system is when it gets to prod. This is a beginning, not an end. And above all the system must change to adapt.
* form follows function is false. form follows failure.
* Any action to change the system has a cost: design, development, and testing effort, plus the cost of release
* If the cost of making these changes exceeds the value returned by ﬁlling a gap or removing a bump, then the rational choice is to not make the change

from this onwards some things are a bit outdated

## Adaptable Software Design

* dependency injection
* good OO desgin
* design patterns
* refactoring, unit testing, TDD
* agile databases

## Adaptable Enterprise Architecture

* top-down architecture from one architect or group - tipically no good
* use biological or ecological methaphor instead of mechanic one
* Real enterprises are always messier than the enterprise architecture would ever admit.
* most useful criterion for evaluating architectures is this: "Does it make IT better at responding to its users' needs?"
* dependecies within the system - loose cluster
* Dependencies Between Systems: Protocols, versioning, database int. (no)

## Releases Shouldn't Hurt

* if it's painful do it more often and get good at it
* faster feedback loop
* timing releases: Don't risk customers for an arbitrary release date
* Zero Downtime Deployments: expansion (new versions of deps), rollout, cleanup
