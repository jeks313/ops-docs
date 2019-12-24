<!-- Space: OP -->
<!-- Parent: Operational Readiness Review -->
<!-- Title: OPR - Health Check -->

# Health Check

- Check all external dependencies
- Do not report full health check output of a dependency in your health check. This leads to deep JSON nesting and health checks that are effectively no longer human-readable.
- Health checks should not run every time the HTTP endpoint is called. Health checks should be periodically run and the results cached. This prevents additional LBs, service discovery systems, etc. from impacting performance substantially
- Do not allow circular dependencies in health checks. If one occurs it is an architectural mistake
- Carefully consider which dependencies are required for your service to work at all, and which are only necessary for some feature or for performance.
- If your health check is used by service discovery or a load balancer, then a shared dependency going offline will deregister the entire cluster for that service. Do not do this if your application can still serve some traffic without a given dependency
- Non-critical dependencies are still useful in the JSON output of a health check, but must be marked as non-critical or informational so that incident responders do not waste time looking at unrelated problems
