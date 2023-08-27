---
status: In Progress
date: 2023-08-26
deciders: slee016
---

# DevOps Tools Onboarding Processor Component

## Context and Problem Statement

The DevOps Tools Onboarding service is a microservice tasked with receiving onboarding requests and processesing those requests aginsts the DevOps tools or capability API's.
This ADR explores the processor component within the microservice architecture that sits between the DebOps Tools Onboarding API and the capability API's. The processor design will lay the foundation on how these onboarding requests are processed asynchronously. The processor can either be event-driven (pub/sub) or task driven (queue).

## Decision Drivers

* Provide a Go library to help drive asynchronous events or tasks within each provisioning workflow
* Ability to make workflows idempotent (failure in one workflow will not impact other workflows)
* Reduce custom implementation or reproducing the wheel
* A Go library that's relatively easy to integrate into the microservice and has good documentation to help with the skill level of the engineering team
* Can eventually be integrated with the offered Cloud services*
* Persist state of tasks for audits, inquiries, or disaster recovery
* Reduce the number of managed technology (e.g. one database vs two databases)

### Requirements
This section explores some business requirements and evaulates how or if those requirements impact the architectural design

#### Criteria
1. Value/Risk: The requirement is directly associated with high business value (benefit vs. cost) or business risk.
2. Key Concern: The requirement is a concern of a particularly important stakeholder such as the project sponsor or an external compliance auditor.
3. Ext. Dep.: The requirement causes new or deals with one or more existing external dependencies that might have unpredictable, unreliable and/or uncontrollable behavior
4. X-Cutting: The requirement has a cross-cutting nature and therefore affects multiple parts of the system and their interactions; it may even have system-wide impact, short term and/or in the long run (examples: security, monitoring)
5. FOAK: The requirement has a First-of-a-Kind (FOAK) character: For instance, this team has never built a component or subsystem that satisfies this particular requirement before.

#### Miro table
Requirements are evaluated against the criteria defined in the [criteria](#Criteria) section. Ratings are based from 0 to 3 where:
0: not relevant
1: low importance
2: medium importance
3: high importance

| **Requirements**                                                          | **Value/Risk** | **Key Concern** | **Ext. Dep** | **X-Cutting** | **FOAK** | **Total** |
|---------------------------------------------------------------------------|----------------|-----------------|--------------|---------------|----------|-----------|
| Process tasks or workflows asynchronously                                 | 3              | 0               | 0            | 3             | 3        | 9         |
| Persist state of tasks for audits or inquiries                            | 3              | 3               | 0            | 0             | 3        | 9         |
| Recovery of tasks or queues in disasters                                  | 2              | 2               | 0            | 0             | 3        | 7         |
| Can be integrated with the offered services*                              | 2              | 0               | 0            | 1             | 3        | 6         |
| Can also be integrated and managed with on-prem Kubernetes                | 2              | 0               | 1            | 1             | 1        | 5         |
| Can be delivered quickly and not re-invent the wheel                      | 3              | 3               | 0            | 0             | 0        | 6         |
| Can be transferred, maintained and managed according to skill set of team | 2              | 0               | 0            | 0             | 3        | 5         |

\* offered services: Azure Redis Cache, Azure Cosmos DB, Google Pub/Sub, Google Cloud SQL


## Considered Options

1. Event driven library: [watermill](https://github.com/ThreeDotsLabs/watermill)
2. Task driven library: [asynq](https://github.com/hibiken/asynq)

## Decision Outcome

**IP** We decided on...

### Consequences
#### Watermill
##### Pros
##### Cons
#### Asynq
##### Pros
##### Cons

## More Information

* A link will be provided to the microservice diagram