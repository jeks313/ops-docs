# Operational Readiness / Friendliness

## Foreword

This setup of documents outlines successive areas of review of a service, set of services, or feature for operational
best practice. These documents focus on delivering software-as-a-service in a robust, scalable, maintainable and 
transparent way.

Before getting started, these processes and areas of review work better and better the further you can inject them into
the engineering process. Doing so requires a lot of education and support of those engineering teams.

Usually, organisations initially implement these as a before-prodcution checklist. It is the easiest place to start but will inject
more friction into the split development / operations divide. 

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

So, this is our attempt to come up with a maturity score out of 10 for service deployments!
