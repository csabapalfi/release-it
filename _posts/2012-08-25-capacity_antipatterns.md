---
layout: post
title: Capacity antipatterns
---

## Resource Pool Contention
* resource pool - necessary evil
* The bottleneck arises when there is contention for the resources. More threads require one of the resources than are available
* During "regular peak" operation, there should be no contention for resources.
* If possible, size resource pools to the request thread pool (witha grain of salt)
* Prevent vicious cycles -> slow transaction -> more resource contention
* Watch for Blocked Threads, use timeouts

## AJAX overkill
* Avoid needless requests (e.g only when input changes vs polling)
* Respect your session architecture
* Minimize the size of replies (JSON)
* Obviously increase the size of your web tier

## Overstaying Sessions
 * Keep sessions in memory for as short a time as reasonable
 * Remember that users don't understand sessions
 * Kepp keys not whole objects

## Wasting bandwith with bad UI practices
* HTML only for markup
* remove templating whitespace if any


## Reload button (really??)
* be careful
* make the Reload button irrelevant (fast site)

## Handcrafted SQL
* N+1 select, ORM collectioen members fetched one by one, one for the list then one for each member (N+1)
* Book says handcrafted SQL is unpredictable, use ORM
* DBA laugh test
* test your queries on real data set (maybe after PII removal)
* or write a data genrator

## Database Eutrophication
* data grows over time
* staging/QA vs prod -> indexes might only make a difference on bigger data
* schema should continously be adopted to support app func.
* table growt rates and churn -> partiotionaing tables
* multilevel storage, access time for historical data probably ok to suffer
* Don't mix transactions and reporting
* INDICES, PURGE OLD DATA, KEEP REPORTING OUT OF PROD

## Integration point latency
* A remote call takes at least 1,000 times as long as a local call.
* Expose yourself to latency as seldom as possible

## Cookie monsters
* serve small cookies
* use cookie-less domains whenever possible


