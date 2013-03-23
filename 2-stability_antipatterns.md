# Stability antipatterns

## Integration points
* Every integration point will eventually fail in some way, and youneed to be prepared for that failure.
* Integration point failures take several forms e.g protocol violation, slow response, or outright hang.
* Debugging integration point failures usually requires peeling back a layer of abstraction - packet sniffers
* Failures propagate quickly when your code isn't defensive enough.
* Apply patterns to avert Integration Points problems
* Solution: Defensive programming via Circuit Breaker, Timeouts, Decoupling Middleware, and Handshaking

### Socket base protocols
* pretty much everything -> exposed to socket layer failures
* simplest: conection refused
* SYN, SYN/ACK, ACK
* TCP/IP Guide or TCP/IP Illustrated
* Idle Connection Dropped by Firewall
* firewall drops packets on the floor

### HTTP
* main source of problem: client libraries
* connect and read timeout

## Chain reaction
* One server down jeopardizes the rest
* The death of one server adds increased load on the others making them more likely to fail
* the rest of the servers will go down even faster if they have the same problem (e.g. probability of deadlock or resource leak)
* resource leaks are the most likely cause of this
* solution: Bulkheads, Cicruit breaker

## Cascading failures
* cracks jump from one system or layer to another, usually because of insufﬁciently paranoid integration points
* exhausted resource pool -> e.g no timeouts
* aggressive retry policy (optimized for transient errors) -> hammering lower layer -> us curcuit breaker instead
* Solution timeouts, circuit breaker

## Users
* each users consumes some memory but some are expensive to serve
* Load test for coversion rate
* unwanted - non converting robots, scrapers, badly configured proxies
* malicious - DDoS - protection on the network equip. level

## Blocked threads
* hanging
* Blocked Threads antipattern usually happens around resource pools
* use proven primitives, rolling your own concurrent stuff can be really hard
* You cannot prove that your code has no deadlocks in it, but you can make sure that no deadlock lasts forever using timeouts
* always use wait(timeout)
* Beware the code you cannot see - test thirdparty libraries

## Attacks of self-denial

* Keep the lines of communication open - know about marketing stuff which can kill your site
* Protect shared resources (or even better: havea share-nothing architecture)
* There’s no such thing as limited distribution (think coupon codes)

## Scaling Effects
* scaling point-to-point connections
* examine production versus QA environments to spot Scaling Effects
* Watch out for point-to-point communication (scales badly, since the number of connections increases as the square of the number of participants) -> tens of servers -> think about alternatives
* Watch out for shared resources (bottleneck, a capacity constraint, and a threat to stability.)

## Unbalanced capacities
* Examine server and thread counts (prod vs qa, frontend vs backend)
* Stress both sides of the interface
* backend should slow down and recover instead of failing
* frontend should deal with it

## Slow Responses
* worse than failing quickly as ties down resources
* can trigger Cascading Failures
* your system t should track its own responsiveness.
* Consider sending an immediate error when the average response time exceeds the system’s allowed time (caller should also have a timeout)
* Hunt for memory leaks or resource contention

## SLA inversion
* This is the IT equivalent of the Second Law of Thermodynamics: service levels only go down
* Don't make empty promises: service level that you can achieve only through luck
* Examine every dependency - SLAs everywhere
* Decouple your SLAs - Be sure you can maintain service even when your dependencies go down

## Unbounded Result Sets
* Use realistic data volumes - production size test data
* Don't rely on the data producers (e.g. that they create a limited amount of data)
* Put limits into other application-level protocols
