## System Design Task - Push Notifications

## Context

Engineering values to consider:

- Customer value and company value
- Speed (time-to-market, not solution performance)
- Simplicity

The company’s system architecture consists of 3 key components at a high-level:

1. A mobile app (Android & iOS) that employees of our clients use.
2. A backend service (Python + Flask & Celery) that can process requests both synchronously and asynchronously.
3. A relational database. (PostgreSQL)

The mobile app is currently available to 1 million employees in the UK and growing quickly.

## Problem description

The company have never sent push notifications to users. These will be used for a wide range of scenarios, for example:

1. To alert users that a new feature has launched.
2. To alert users of a promotion that is now available.
3. To alert users that their shift has been added, and that their earnings have increased by some amount.

Please outline the design of a subsystem that would allow us to send push notifications. Key areas to consider are:

1. Which components are impacted?
2. What data is required?
3. How will that data be stored?
4. What is the throughput of the system?
5. How are messages created to send to audiences?

## My proposed solution

1. [Description](my-proposed-solution.md)
2. [C4 Model Diagrams](diagrams/c4-model-diagrams.md)