---
layout: post
title: Stability patterns
---

## Use Timeouts
* Apply to Integration Points, Blocked Threads, and Slow Responses
* Apply to recover from unexpected failures and keep moving
* Consider delayed retries

## Circuit Breaker
* Don't do it if it hurts - prevenet calls when external system is unavailible
* call failed multiple times -> trip open, always return error
* Expose, track, and report state changes


## Bulkheads
* Save part of the ship
* might result in less efficient use of resources
* granularity: thread pools inside an application, CPUs in a server, or servers in a cluster
* Very important with shared services models

##Steady state
* Avoid ﬁddling - Human intervention leads to problem - run continously at least between deployments
* Purge data with application logic
* Limit caching
* Roll the logs

## Fail fast
* Avoid Slow Responses and Fail Fast
* Reserve resources, verify Integration Points early (e.g check circuit breakers)
* basic input validation early on

## Handshaking
* Create cooperative demand control -(most app level protocols don't do handshaking)
* Consider health checks - app level workaround instead of handshaking
* Build Handshaking into your own low-level protocols

## Test harness
* Emulate out-of-spec failures - real world failure modes
* Stress the caller - slow response, no response, grabage response
* Leverage shared harnesses for common failures
* Supplement, don't replace, other testing methods

## Decoupling middleware
* Decide at the last responsible moment
* Avoid many failure modes through total decoupling
* Learn many architectures, and choose among them