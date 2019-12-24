<!-- Space: OP -->
<!-- Parent: Operational Readiness Review -->
<!-- Title: OPR - Metrics and Alerting -->

# Metrics and Alerting

## Metrics

- Watch cardinality
- Cardinality is a measure of all unique sets of possible labels on a metric. Unbounded cardinality is very bad as most time series data stores (Prometheus, for example) stores each unique set of labels as it's own time series.
- Some examples of unbounded cardinality:
-- email address, IP address, error message - all need to be considered carefully and CANNOT be used in long term storage.
- Good examples:
-- http error code as this is a fixed set
-- service type (hopefully don't have unbounded micro services!)
- Export informational metrics such as version number, important configuration values, build tag and time. These are fantastically useful for spotting configuration drive or change, for tracking versions of your deployed software and other things that can be incorporated into the dashboard. Simply emit the informational value as a label with a value of 1.
- Do not use sample-based metrics (e.g. Prometheus) for discrete events e.g. error logs. Use something like InfluxDB for this
- Free-form field metrics mean a metric does not exist until the first time an event related to it occurs. This means the first instance of an error is a counter going from null -> 1. This is not easily detectable in Prometheus in a way that also allows for identification of incrementation of said counter
- If your application has a queue it must be monitored
- Measure the current depth of a queue and alert on it
- Measure the maximum age of elements in the queue and alert on it
- If more sensitivity is required other alerts can be created
    - Queues that are low but non-zero or slowly rising for an extended period of time can indicate a small number of unprocessable elements
    - Queues rise quickly can be alerted on before they hit the maximum queue depth
- What to measure (here’s a few frameworks)
    - RED (Rate/Errors/Duration) https://www.weave.works/blog/the-red-method-key-metrics-for-microservices-architecture/
    - USE (Utilization/Saturation/Errors) http://www.brendangregg.com/usemethod.html
    - SRE Golden Signals https://landing.google.com/sre/sre-book/chapters/monitoring-distributed-systems/ #xref_monitoring_golden-signals
    - The first four things you measure (useful for services) https://www.honeycomb.io/blog/instrumentation-the-first-four-things-you-measure /

## Alerting

No discussion of alerting can be had without introducing SLOs. Every service should have Service Level Objectives that describe it's desired availability to the 
customer. Once we describe what key Service Level Indicators (SLIs) exist, we can start to monitor them.

Some good case studies of implementing SLOs:

- https://landing.google.com/sre/workbook/chapters/slo-engineering-case-studies/
