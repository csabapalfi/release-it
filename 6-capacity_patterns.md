# Capacity patterns

## Pool connections

* basic
* timeout for connection checkout
* monitor waiting times
* undersized pool -> contention

##  Use Caching Carefully

* limit cache sizes (memory usage)
* monitor hit rates
* consider generation time before caching
* when possible pre-compute instead
* consider risk of stale data (TTLs, flushing) and access and change frequency

## Precompute content

* Precompute content that changes infrequently

## Tune the Garbage Collector
* tune it and revise for each release
* don't pool objects