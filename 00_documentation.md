# Documentation

- Documentation should live with the micro service.
- When the operational unit is made up of several micro services a service catalog page should be created.
- Documentation is like code - it should have a QA process. In particular, searching. When you search for any service, is the service catalog page the first result? If you search for a micro service, does the catalog page or pages where this is used appear in the first search results?
- Service catalog page should include:
-- link back to user feature or product documentation - ie what does this do for the customer as a whole, along with a summary 
-- all child micro services
-- all dependencies of this service
-- all configuration options that are relevant to deployment (see below configuration section)
-- estimates on service load, logging load, database load, etc.
-- dashboard links
-- logging links (either central, or how to get to local logs)
-- logging examples - when things are working well what you see, when things are failing what you would see
-- key service metrics
-- SLOs (Service Level Objectives)
-- SLIs (Service Level Indicators)
-- alerting required (along with links to alert catalog page or pages)
