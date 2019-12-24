# Operational Readiness / Friendliness

## Foreword

This setup of documents outlines successive areas of review of a service, set of services, or feature for operational
best practice. These documents focus on delivering software-as-a-service in a robust, scalable, maintainable and 
transparent way.

Before getting started, these processes and areas of review work better and better the further you can inject them into
the engineering process. Doing so requires a lot of education and support of those engineering teams.

Usually, organisations implement these as a before-prodcution checklist. It is the easiest place to start but will inject
more friction into the split development / operations divide.

As such you quickly want to move the expertise from the SRE team into the engineering teams, getting them to use these review
areas during the development process. 

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
