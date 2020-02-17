<!-- Space: OP -->
<!-- Title: Operational Readiness Review -->

# Operational Readiness / Friendliness

## Foreword

This set of documents outlines successive areas of review of a service, set of services, or feature for operational
best practice. These documents focus on delivering software-as-a-service in a robust, scalable, maintainable and 
transparent way.

Before getting started, these processes and areas of review work better and better the further you can inject them into
the engineering process. Doing so requires a lot of education and support of those engineering teams.

Usually, organisations initially implement these as a before-production checklist. Though this is the easiest place to start 
the trade off will be more friction between development and operations which long term is detrimental.

As such you quickly want to move the expertise from the SRE team into the engineering teams, getting them to use these review
areas during the development process, and review them before submitting a service for production deployment. 

This is not an easy thing and takes dedication, passion for reliability engineering and lots of support!

## Beginning the conversation

Any review should start with the customer and the promises you are implicitly making by developing this service or feature in
the first place.

Some places to start before framing the discussion around the review areas:

- What does this feature or service provide to it's customers? 
- What promises are you making as to the availability and scalability of this service?
- What impact can this service have to the rest of the services provided to the customer?
- What constitutes success for this service or feature, to it's customers? Is it uptime? Is it uptake of the feature?

The next questions are around how you are going to measure these success criteria, and as engineers, what are indicators
of both sucess and failure (SLIs)?

## Service Maturity Scale

This set of documents is an attempt to assess the operational maturity of a service. It starts with the basics like documentation
and logging and works it's way up the levels. If a service passes each section of review it advances along the maturity scale.

It has been our experience that the most robust, easy to troubleshoot, resilient services we have worked with had most of the areas
that this document covers addressed.

This is our attempt to come up with a maturity score out of 10 for service deployments!

### Maturity Level - Documentation

Level -1: No documentation exists!
Level  0: Engineering documentation exists, design pages, no dedicated operational docs.
Level  1: Operational docs exist, does not contain one of: inputs, dependencies, outputs, or API.
Level  2: Operational page exists, contains inputs, dependencies, outputs, and any APIs.
Level  3: Level 2 docs exist, have been reviewed, include additionally failure modes tested with example diagnostics, dashboard links, SLOs, example logs.
Bonus: docs are served by the service, and include API examples in an easy to use manner for testing!

### Maturity Level - Logging

Level -1: No logging at all
Level  0: Logging, but unstructured and incomplete.
Level  1: Structured logging, in JSON please.
Level  2: Structured logging with events and decisions, no warnings are emitted.
Level  3: Level 2 logging with error zero, logging is reviewed with common failure cases.
Anti-Bonus: go to -2 if you multi-line log!
Anti-Bonus: go to -2 if you log to a file in a container!

### Maturity Level - Configuration

### Maturity Level - Metrics & Dashboarding

Level -1: No metrics at all
Level  0: Basic metrics provided, likely provided by an included base library.
Level  1: Service metrics that are specific to this service are provided.
Level  2: Service metrics and dependency metrics are provided.
Level  3: Metrics are provided along with dashboard showing service health.

### Maturity Level - Health Checking

Level -1: No health checks - hopefully we are not here if we are deploying to k8s.
Level  0: Health check returns just a status code.
Level  1: Health check endpoint exists and emits data about the service.
Level  2: Health check endpoint exists and emits data on the serivce and all dependencies.
Level  3: Health check has the ability to list both breaking and non-breaking dependencies.

### Maturity Level - Monitoring and Alerting

operational alerts
team alerts
slo alerts

### Maturity Level - SLOs / SLIs

### Maturity Level (Options) - Circuit Breakers & Tracing

### Maturity Level - Continuous Deployment

Level -1: Basic continuous integration
Level  0: Continuous integration 

