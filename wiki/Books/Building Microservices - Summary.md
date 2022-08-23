## Summary

[![Figure 1: "Building Microservices (2nd edition)"" along my notes](https://res.cloudinary.com/practicaldev/image/fetch/s--f6os3Zoq--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://blog.dornea.nu/posts/img/2022/building-microservices-2nd-edition/microservices-book-cover.jpg)](https://res.cloudinary.com/practicaldev/image/fetch/s--f6os3Zoq--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://blog.dornea.nu/posts/img/2022/building-microservices-2nd-edition/microservices-book-cover.jpg)

During my overall IT carreer I came across different architectural design patterns where oppinions differ on the question if they’re the right ones for the problems/challanges teams are dealing with. Before reading this book I was familiar with _some_ of the microservices concepts but it was some article (on modern architectures) that rouse my attention and introduced me to Sam Newman. At the same time I was surprised to read about the similarities between [Hexagonal Architecture](https://brainfck.org/#Hexagonal%20Architecture) and _microservices_. But also topics like [DDD](https://brainfck.org/#DDD), [CD](https://brainfck.org/#Continuous%20Delivery%20(CD)),[CI](https://brainfck.org/#Continuous%20Integration%20(CI)) are bound together in way that you need to take a hollistic approach to (building) microservices.

I recommend this book to anyone willing to spend some time (book has ca. 500 pages) learning about [Information hiding](https://brainfck.org/#Information%20hiding), [communication between microservices](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#ch-dot-4-communication-styles), [proper teams setup](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#stream-aligned-teams), role of (IT) [architects](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#ch-dot-16-the-evolutionary-architect) and much more. Fair enough the author emphasizes multiple time the _complexity_ of decoupling existing services (monoliths) into smaller, independent ones (microservices). The book recommendations in each chapter also give a great hint where you can enlarge upon a specific topic.

What follows next is an [ORG mode](https://orgmode.org/) / outline style collection of notes, thoughts and quotes from the book.

## [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#ch-1-what-are-microservices)Ch. 1: What are Microservices?

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#definition)Definition

> Microservices are independently releasable services that are modeled around a business domain. A service encapsulates functionality and makes it accessible to other services via networks.

-   [Microservices](https://brainfck.org/#Microservices) are a type of [SOA](https://brainfck.org/#SOA) architecture
    -   service boundaries are important
    -   independent deployability is key
-   [Microservices](https://brainfck.org/#Microservices) embrace the concept of [Information hiding](https://brainfck.org/#Information%20hiding)

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#key-concepts)Key Concepts

-   Independent deployability
-   Modeled around a business domain
-   Owning their own state
-   Size
-   Flexibility
-   Alignment of architecture and organization

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#advantages)Advantages

-   Technology Heterogeneity

[![image](https://res.cloudinary.com/practicaldev/image/fetch/s--2DsdIHbi--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://blog.dornea.nu/posts/img/2022/building-microservices-2nd-edition/microservices_07-02-2022_12.35_4.jpg)  
Technology heterogenity  
](https://blog.dornea.nu/posts/img/2022/building-microservices-2nd-edition/microservices_07-02-2022_12.35_4.jpg)

-   Robustness
-   Scaling
-   Ease of Deployment
-   Organizational alignment
-   Composability

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#pain-points)Pain Points

-   Developer Experience
-   Technology overload
-   Costs
-   Reporting
-   Monitoring and troubleshooting
-   Security
-   Latency
-   Data consistency

## [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#ch-2-how-to-model-microservices)Ch. 2: How to model microservices

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#information-hiding)[Information hiding](https://brainfck.org/#Information%20hiding)

-   hide as many details as possible behind a module / microservice boundary
-   Parnas identified following benefits:
    -   improved development time
    -   comprehensibility
    -   each module is isolated and therefore better to understand
    -   flexibility

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#cohesion)Cohesion

-   code that changes together, stays together
-   strong cohesion
    -   ensure related behavior is at one place
-   weak cohesion
    -   related functionality is spread across the system

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#coupling)Coupling

-   loosely coupled
    -   change to one service should not require a change to another
-   a loosely coupled services knows as little as it needs about the services it communicates with
    -   limitation of number of different types of calls is important

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#interplay-of-coupling-and-cohesion)Interplay of coupling and cohesion

> A structure is stable if cohesion is strong and coupling is low.

-   cohesion applies to the relationship between things **inside** a boundary
-   coupling describes relationship **between things across** a boundary
-   still: there is no best way how to organize code

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#types-of-coupling)[Types of coupling](https://brainfck.org/#Types%20of%20coupling)

#### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#domain-coupling)Domain coupling

-   one microservice interacts with another microservice because it needs the functionality the other microservice provides

[![image](https://res.cloudinary.com/practicaldev/image/fetch/s--7rCyQweP--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://blog.dornea.nu/posts/img/2022/building-microservices-2nd-edition/microservices_07-02-2022_12.35_5.jpg)  
Domain coupling  
](https://posts/img/2022/building-microservices-2nd-edition/microservices_07-02-2022_12.35_5.jpg)

-   considered as a _loose_ form of coupling
-   again, information hiding: Share only what you absolutely have to, and send only the absolute minimum amount of data that you need

#### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#passthrough-coupling)Pass-through coupling

-   one microservice passes data to some other microservice because data is needed by another microservice

[![image](https://res.cloudinary.com/practicaldev/image/fetch/s--pOSCPdFY--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://blog.dornea.nu/posts/img/2022/building-microservices-2nd-edition/microservices_07-02-2022_12.35_6.jpg)  
Pass-through coupling  
](https://posts/img/2022/building-microservices-2nd-edition/microservices_07-02-2022_12.35_6.jpg)

#### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#common-coupling)Common coupling

-   when 1 or 2 microservices make use of a **common** set of data
    -   use of shared DB
    -   use of shared memory/filesystem
-   problem: changes to data can impact multiple microservices at once
-   better solution would be to implement [CRUD](https://brainfck.org/#CRUD) operations and let only 1 microservice handle shared DB operations

#### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#content-coupling)Content coupling

[![image](https://res.cloudinary.com/practicaldev/image/fetch/s--JvtyQuq_--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://blog.dornea.nu/posts/img/2022/building-microservices-2nd-edition/microservices_07-02-2022_12.35_7.jpg)  
Content coupling  
](https://blog.dornea.nu/posts/img/2022/building-microservices-2nd-edition/microservices_07-02-2022_12.35_7.jpg)

-   when an upstream service reaches into internals of a downstream service anc changes its internal state

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#ddd)DDD

[DDD](https://brainfck.org/#DDD) stands for Domain-Driven Design.

#### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#concepts)Concepts

-   Ubiquitous language
-   Aggregates
-   Bounded context

#### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#event-storming)Event Storming

-   collaborative brainstorming exercise designed to help design a domain model
-   invented by [Alberto Brandolini](https://www.eventstorming.com/)

#### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#boundaries-between-microservices)Boundaries between microservices

There are some factors when defining clear boundaries between microservice

-   volatility
-   data
    -   also with concern to security
-   technology
-   organizational
    -   Layering Inside vs Layering Outside

## [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#ch-3-split-the-monolith)Ch. 3: Split the monolith

[![image](https://res.cloudinary.com/practicaldev/image/fetch/s--L9_Ksevh--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://blog.dornea.nu/posts/img/2022/building-microservices-2nd-edition/microservices_07-02-2022_12.35_2.jpg)  
Monolith types  
](https://blog.dornea.nu/posts/img/2022/building-microservices-2nd-edition/microservices_07-02-2022_12.35_2.jpg)

[![image](https://res.cloudinary.com/practicaldev/image/fetch/s--mfcelNOn--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://blog.dornea.nu/posts/img/2022/building-microservices-2nd-edition/microservices_07-02-2022_12.35_3.jpg)  
Monolith types  
](https://blog.dornea.nu/posts/img/2022/building-microservices-2nd-edition/microservices_07-02-2022_12.35_3.jpg)

-   you need to have a **goal** before moving to microservices
    
    -   should be a conscious decision
    -   without clear understanding of what you want to achieve, you could fall into the trap of **confusing activity with outcome**

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#decomposition-patterns)Decomposition patterns

-   Strangler fig pattern
-   Parallel run
-   Feature toggles

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#data-decomposition-concerns)Data Decomposition concerns

-   performance
-   data integrity
-   transactions
-   Tooling
-   Reporting DB

## [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#ch-4-communication-styles)Ch. 4: Communication styles

[![image](https://res.cloudinary.com/practicaldev/image/fetch/s--iQ_OWNt_--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://blog.dornea.nu/posts/img/2022/building-microservices-2nd-edition/microservices_07-02-2022_12.35_10.jpg)  
Communication styles  
](https://blog.dornea.nu/posts/img/2022/building-microservices-2nd-edition/microservices_07-02-2022_12.35_10.jpg)

-   styles for IPC communications
    -   synchronous blocking
    -   asynchronous blocking
    -   request-response
    -   [Event-Driven Architecture](https://brainfck.org/#Event-Driven%20Architecture)
    -   Common data

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#eda)EDA

-   events vs messages
    -   **event** : is a fact
    -   **message** : is a thing
    -   a message contains an event

## [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#ch-5-implementing-communication)Ch. 5: Implementing communication

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#criterias-for-ideal-technology)Criterias for ideal technology

-   backward compatibility
-   make your interface(s) explicit
-   keep your APIs technology-agnostic
-   make your service simple for the consumers
-   hide internal implementation details

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#technology-choices)Technology choices

-   [RPC](https://brainfck.org/#RPC)
-   REST
-   GraphQL
-   Message brokers

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#api-gateway)API Gateway

-   built on top on existing HTTP proxy products
-   main function: reverse proxy
    -   but also authentication, logging, rate limiting
-   Examples:
    -   [AWS API Gateway](https://aws.amazon.com/api-gateway/)
    -   [GCP API Gateway](https://cloud.google.com/api-gateway)

[![image](https://res.cloudinary.com/practicaldev/image/fetch/s--3quR0o9V--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://blog.dornea.nu/posts/img/2022/building-microservices-2nd-edition/microservices_07-02-2022_12.35_11.jpg)  
API Gateway  
](https://blog.dornea.nu/posts/img/2022/building-microservices-2nd-edition/microservices_07-02-2022_12.35_11.jpg)

## [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#ch-6-workflow)Ch. 6: Workflow

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#distributed-transactions)Distributed Transactions

#### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#twophase-commits-2pc)Two-phase Commits (2PC)

-   a commit algorithm to make transactional changes in a distributed system, where multiple separate parts need to be updated

#### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#sagas)Sagas

-   coordinate multiple changes in state
-   but without locking resources for a long period
-   involves
    -   backward recovery
    -   forward recovery
-   allows to recover from _business_ failures not technical ones
-   when rollback is involved, maybe a compensating transaction is needed

#### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#books)Books

-   [Enterprise Integration Patterns: Designing, Building, and Deploying Messaging Solutions](https://www.goodreads.com/book/show/85012.Enterprise_Integration_Patterns)
-   [Practical Process Automation](https://www.goodreads.com/en/book/show/55362275-practical-process-automation)

## [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#ch-7-build)Ch. 7: Build

-   on [Continuous Integration (CI)](https://brainfck.org/#Continuous%20Integration%20(CI))
-   how to organize artifacts
    -   monorepo
    -   multirepo

## [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#ch-8-deployment)Ch. 8: Deployment

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#principles-of-microservices-deployment)[Principles of Microservices Deployment](https://brainfck.org/#Microservices/Deployment)

-   isolated execution
-   focus on automation
-   Infrastructure as a Code
-   zero-downtime deployment
-   desired state management
-   progressive delivery

## [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#ch-10-from-monitoring-to-obersavability)Ch. 10: From monitoring to obersavability

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#the-observability-of-a-system)The observability of a system

-   is the extenct to which you can understand the internal state of the system from external output
-   **monitoring** is something we _do_
-   **observability**
-   pillars of observability

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#alert-fatigue)Alert fatigue

> Alert fatigue—also known as alarm fatigue—is when an overwhelming number of alerts desensitizes the people tasked with responding to them, leading to missed or ignored alerts or delayed responses – [Source](https://www.atlassian.com/incident-management/on-call/alert-fatigue)

#### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#what-makes-a-good-alert)What makes a good alert

An alert has to be:

-   relevant
-   unique
-   timely
-   prioritized
    -   give enough information to decide in which order alerts should be dealth with
-   understandable
    -   information has to be clear and readable
-   diagnostic
    -   it needs to be clear what is wrong
-   advisory
    -   help the operator understand what actions need to taken
-   focussed
    -   draw attention to the most important issues

#### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#on-the-importance-of-testing-quote)On the importance of testing quote

> “Not testing in production is like not practitioning with the full orchestra because your solo sounded fine at home”

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#semantic-monitoring)Semantic monitoring

-   compare against normal conditions
-   you could use synthetic transactions
-   other options
    -   A/B testing
    -   canary releases
    -   [Chaos engineering](https://brainfck.org/#Chaos%20engineering)
    -   parallel runs
    -   smoke tests

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#tools)Tools

-   [opentelemetry.io](https://opentelemetry.io/)

## [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#ch-11-security)Ch. 11: Security

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#lifecycle-of-secrets)Lifecycle of secrets

-   Creation
    -   How we create the secret
-   Distribution
    -   How do we make sure the secrets get to the right place?
-   Storage
    -   Is the secret stored in a way only authorized parties can access it?
-   Monitoring
    -   Do we know how secret is used?
-   Rotations
    -   Are we able to change the secret without causing problems?

## [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#ch-12-resiliency)Ch. 12: Resiliency

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#resiliency)Resiliency

-   defined by David D. Woods
-   aspects

## [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#ch-14-user-interfaces)Ch. 14: User interfaces

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#streamaligned-teams)Stream-aligned teams

-   topologies how to build organizations, teams
-   aka “full-stack teams”
-   a team aligned to a single, valuable stream of work
-   the team is empowered to build and deliver customer or user value as quickly and independently as possible, without requiring hand-offs to other teams to perform parts of the work

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#microfrontends)Microfrontends

-   architectural style where independently deliverable frontend applications are composed into a greater whole
-   possible implementations

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#scs)SCS

-   stands for Self-Contained Systems
-   highlights

## [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#ch-15-organizational-structures)Ch. 15: Organizational structures

-   [Stream-aligned teams](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#stream-aligned-teams)
    -   concept aligns with loosely-coupled organizations (as in [Accelerate](https://brainfck.org/#Accelerate))

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#conways-law)Conways Law

> “Any organization that designs a system will inevitably produce a design whose structure is a copy of the organizations communication structure” - Melvin Conway

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#all-about-people)All about people

> “Whatever industry you operate in, it is all about your people, and catching them doing things right, and providing them with the confidence, the motivation, the freedom and desire to achieve their true potential” - John Timpson

## [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#ch-16-the-evolutionary-architect)Ch. 16: The evolutionary architect

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#role-of-architects)Role of architects

-   We should think of the role of IT architects more as **town planners** than architects for the built environment

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#buildings-and-software)Buildings and software

> The comparison with software should be obvious. As our users use our software, we need to react and change. We cannot foresee everything that will happen, and so rather than plan for any eventuality, we should plan to allow for change by avoiding the urge to overspecify every last thing. Our city (the system) needs to be a good, happy place for everyone who uses it. One thing that people often forget is that our system doesn’t just accommodate users; it also accommodates developers and operations people who also have to work there, and who have the job of making sure it can change as required.

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#governance)Governance

> Governance ensures that enterprise objectives are achieved by evaluating stakeholder needs, conditions and options; setting direction through prioritisation and decision making; and monitoring performance, compliance and progress against agreed-on direction and objectives. – Cobit 5

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#responsibilities-of-the-evolutionary-architect)Responsibilities of the evolutionary architect

-   Vision
    -   clearly communicated technical vision for the system that will help meet requirements of customers and organization
-   Empathy
    -   understand impact of decissions on customers and colleagues
-   Collaboration
    -   engage with as many of your pears and colleagues as possible to help define, refine and execute the vision
-   Adaptability
    -   tech vision changes as required by customers/organization
-   Autonomy
    -   balance between standardizing and enabling autonomy for your teams
-   Governance
    -   system being implemented fits the tech vision
    -   make sure it’s easy for people to do the right thing

### [](https://dev.to/dorneanu/book-summary-building-microservices-2nd-edition-2bm0#book-recommendations)Book recommendations

-   [Building evolutionary architectures](https://www.goodreads.com/en/book/show/35755822-building-evolutionary-architectures)
-   [The software architect elevator](https://www.goodreads.com/book/show/49828197-the-software-architect-elevator)