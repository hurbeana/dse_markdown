* TOC
{:toc}

## Motivation and Introduction

**Microservices**
* A few years ago, some of us were chatting about microservices being an
  interesting idea.
* The next thing you know it’s become the default architecture for hundreds of
  companies around the world […], and has everyone running to jump on a
  bandwagon that they are worried is about to disappear over the horizon.

## Chapter 1: Microservices

### The Software Monolith

* Big and complex - grown over decades
* Monolithical design - deployed at once
* Closed systems - no standard APIs
* Static interfaces - adaption ripples through system
* Frozen technologies - programmers shortage
* Vertical silos - no horizontal scaling
* Static planning and development
* Slow time-to-market -every 6 months e.g.
* Manual testing and deployment - maintenance window
* No requirements/design documentation existing
* High risk in any change of the system
* BUT: Ease of deployment, simple development workflows, simple end-to-end
  testing

*"Big ball of mud"*

### Types of Monoliths (MOnolithic Architecture)

1. Single Process Monolith
2. Modular Monolith
3. Modular Monolith w/ decomposed Database
-> *"Deployment Monolith"*

### Microservice Architecture (MSA)

* Microservice architecture (MSA) is emerging as the new standard for building
  applications.
    - This approach to software design breaks complex applications into small,
      nimble, independent components to speed up time to market, simplify
      maintenance, and enable continuous integration.

### Microservices: Split up the deployment monolith

Microservice -> deployed independetly

*"You build it, you run it"* (Devops principle)

### What are Microservices?

#### [Sam Newman15]

* “Microservices are small, autonomous services that work together.”

#### [Chris Richardson18]

* Microservices - also known as the microservice architecture - is an
  architectural style that structures an application as a collection of
  services that are
    - Highly maintainable and testable
    - Loosely coupled
    - Independently deployable
    - Organized around business capabilities
    - Owned by a small team
* The microservice architecture enables the rapid, frequent and reliable
  delivery of large, complex applications. It also enables an organization to
  evolve its technology stack.

#### [Sam Newman19]

* Microservices are independently deployable services modeled around a business
  domain.
* They communicate with each other via networks, and as an architecture choice
  offer many options for solving the problems you may face.
* It follows that a microservice architecture is based on multiple
  collaborating microservices.
* They are a type of service-oriented architecture (SOA), albeit one that is
  opinionated about how service boundaries should be drawn, and that
  independent deployability is key.
* Microservices also have the advantage of being technology agnostic.

#### [Ralf Westphal14]

* µServices sind Komponenten mit plattformneutralem Kontrakt.
* Der Zweck von µServices ist, die Wandelbarkeit von Software zu erhöhen.
    - “That´s it. Nicht mehr, nicht weniger. Vor allem: nur dies.”
    - focuses on the evolvability advantage that systems using microservices
      expose and does not recommend a use of microservices to increase other
      software qualities like e.g. scalability or resilience

### Service-Oriented Architecture (SOA)

A service has four properties according to one of many definitions of SOA:
1. It logically represents a business activity with a specified outcome.
2. It is self-contained.
3. It is a black box for its consumers, meaning the consumer does not have to
   be aware of the service's inner workings.
4. It may consist of other underlying services.

### About Microservices

#### Characteristics [Lewis/Fowler14]

* Componentization via Services
* Organized around Business Capabilities
* Products not Projects
* Smart endpoints and dumb pipes
* Decentralized Governance
* Decentralized Data Management
* Infrastructure Automation
* Design for Failure
* Evolutionary Design

#### Key Benefits [Sam Newman15]

* Technology Heterogeneity
* Resilience
* Scaling
* Ease of Deployment
* Organizational Alignment
* Composability
* Optimizing for Replaceability

#### “Competitors”

* Ancient
    - Shared Libraries (DLLs, Shared objects)
    - OSGi Bundles
    - SOA Services
* Future
    - Nanoservices?

#### Related Design Principles

* Coupling/Cohesion
* Single Responsibility Principle (SRP) [Bob Martin]
* Conways Law [Melvin Conway1968]
* Information Hiding [David Parnas1971]
* Bounded Context [Domain Driven Design, Eric Evans]
* Throw away version one [The mythical man month, Fred Brooks]
* Keep it stupid simple (KISS)
* You ain‘t gonna need it (YAGNI)
* Best tool for the job
* CQRS
* UI composition (e.g. Client-side UI composition)
* HATEOAS (Client/Server Interface decoupling)

#### Why Choose Microservices? [Sam Newman19]

* Improve Team Autonomy
* Reduce Time To Market
* Scale Cost-Effectively for Load
* Improve Robustness (Chaos Monkey, Simian Army, Chaos Mesh)
* Scale the Number of Developers
* Embrace New Technology
* But for each goal, Sam Newman names alternatives.

#### Pattern Languages

* A pattern is a reusable solution to a problem
* Selected microservices patterns following:
    - Database per Service Pattern (mandatory for the lab!)
    - Saga pattern (to compensate for absence of ACID)
    - Transactional outbox (insert into DB and publish message
      ‘all-or-nothing’)
    - Externalized configuration
    - API gateway (mandatory for the lab!)
    - Circuit Breaker
    - Client-side UI composition

#### Risks

* Distributed transactions / consistency / ACID?
* How to define optimal service boundaries?
* How to slice the monolithic UI?
* How to deploy thousands of services?
* How to do integration testing?
* How to enforce interface compatibility (compilation error)
* How to integrate the business experts?
* How to empower teams for taking service responsiblity?
* How to deal with a vast number of services in terms of
    - Management (e.g. API Versioning)
    - Monitoring / Logging
    - Elastic scalability
* How to deal with `n*(n-1)/2` communication channels?
    - Network load
    - Latency
    - Unpredictable network load and latency → indeterminism
    - Resilience (e.g. against fault propagation)
* Freedom of choice leads to unprecedented chaos
    - Dezentralized Governance
    - Rationales / Rules / Standards

### Coupling and Cohesion

* Even if you have nothing else in your design toolbox, merely by addressing
  coupling and cohesion properly you can already achieve a rather decent
  software system design
    - In software engineering, coupling is the degree of interdependence
      between software modules; a measure of how closely connected two routines
      or modules are; the strength of the relationships between modules.
    - In computer programming, cohesion refers to the degree to which the
      elements inside a module belong together. In one sense, it is a measure
      of the strength of relationship between the methods and data of a class
      and some unifying purpose or concept served by that class. In another
      sense, it is a measure of the strength of relationship between the
      class's methods and data themselves.

- “The code that changes together, stays together.”

*Constantine‘s Law: A structure is stable if cohesion is high, and
coupling is low. [Larry Constantine1968]*

#### Forms of Coupling

* **Implementation Coupling**
    - A is coupled to B in terms of how B is implemented — when the
      implementation of B changes, A also changes.
* **Domain Coupling**
    - E.g. between the Order Service and Recommendation Service
* **Temporal Coupling**
    - Synchronous RPC calls (vs. asynchronous message-oriented communication)
    - 2 Phase Commit (2PC) Transaction in a RDBMS
* **Deployment Coupling**
    - E.g. in a monolith: Static Web Content + WAR files + EAR files + Database

### Key Problem To Solve: Modularization

* There is no „silver bullet“ solution to reach reasonable modularization
    - Not object-orientation / information hiding
    - Not a specific programming language
    - Also: Not microservices!
    - (e.g. reuse domain model lib in every microservice → deployment
      monolith!)
* But
    - Domain Driven Design is considered best approach currently available
    - i.e. business analysis is equally important to technical solution
* Modularization yields Parallelization → [Amdahl‘s Law]

### Crucial Questions

#### Why not stick to SOA?

* Where is the Enterprise Service Bus (ESB)?
* Where is the business process layer/engine (BPM)?
* Where is the rule engine?
* Where are the `WS*` standards?
* Where is the tool support?
* Who takes the warranty?

#### How small is micro?

* No standardized/generally accepted definition!
* Some heuristical approaches available
    - „If a service is bigger than your head, than it is too big“ [James Lewis]
    - „Be able to rewrite it in two weeks (with your team)“ [Sam Newman15]
    - Two-Pizza Rule (team as big as two pizzas can feed) [Jeff Bezos]
    - 7±2 rule [Georg A. Miller1956]

#### How to design for distribution?

* Database
* GUI
* Security / SSO
* Communication / Integration
* Testing
* Deployment
* Monitoring


### Measuring Migration Success

* NOT: Number of microservices created
* BUT
    - Reduced lead time
    - Increased deployment frequency
    - Reduced change failure rate
    - Improved “-ilities”
    - Maintainability
    - Testability
    - Deployability
    - Etc.

## Chapter 2

### Basic Design Approaches

* First Idea of a System
* Big Design Up Front (BDUF)
* Iterative Design/Architecture
* Top-down / Bottom-up
* X-Driven Design
    - Domain-/Test-/Feature-Driven
* Copy from Patterns
* Design by Contract
* Keep it simple, stupid (KISS)
* Divide et Impera (Divide & Conquer)
* Single Responsibility Principle (SRP)
* Separation of Concerns (SoC)
* Don‘t Repeat Yourself (DRY)
* Abstraction
* Modeling/Visualisation
* Information Hiding
* etc.

### Design Methods: The Big Ones

* Structured Design (SD)
    - Hierachical structured functional modules
    - Decomposition, structure, plumbing
    - Strictly divided view of data and functions
* Object-oriented Design (OOD)
    - Class hierarchies
    - Information hiding, inheritance, polymorphy
* Domain-driven Design (DDD)
    - Modeling around domains (e.g. Bounded Context)

### Clean Code Developer (CDD) Design Principles
* Separation of Concerns (SoC)
* Inversion of Control (IoC)
* Don‘t repeat yourself (DRY)
* Keep it simple, stupid (KISS)
* You Ain’t Gonna Need It (YAGNI)
* Favour Composition over Inheritance (FCoI)
* Single Level of Abstraction (SLA)
* Information Hiding (Coupling/Cohesion)

### Object-Oriented Design Principles
* *S*ingle Responsibility Principle (SRP)
* *O*pen Closed Principle (OCP)
* *L*iskov Substitution Principle (LSP)
* *I*nterface Segregation Principle (ISP)
* *D*ependency Inversion Principle (DIP)
* Acyclic Dependencies Principle (ADP)
* Common Reuse Principle (CRP)
* The Stable Dependencies Principle (SDP)
* Law of Demeter (LoD) etc.

*“SOLID”*

### Domain Driven Design

* Domain-Driven Design is an approach to the development of complex software in
  which we:
    - Focus on the core domain
    - Explore models in a creative collaboration of domain practitioners and
      software practitioners
    - Speak a ubiquitous language within an explicitly bounded context
* Domain
    - A sphere of knowledge, influence, or activity. The subject area to which
      the user applies a program is the domain of the software.
* Ubiquitous language
    - A language structured around the domain model and used by all team
      members within a bounded context to connect all the activities of the
      team with the software.
* Bounded Context
    - A description of a boundary  (typically a subsystem, or the work of a
      particular team) within which a particular model is defined and
      applicable.
* A Bounded Context defines the boundaries of the biggest services possible
    - Services that won’t have any conflicting models inside of them
    - Crossing the boundaries, conflicting models will result in big ball of
      mud
* Therefore, a Microservice is a Bounded Context, but not vice versa. Not every
  Bounded Context is a Microservice.

### Procedure Models: First-in-mind models

* Waterfall
* Iterative
    - Spiral model
    - RUP/OpenUP
    - V-Modell (XT) ...
* Agile
    - XP
    - Crystal
    - Scrum
    - Kanban
    - LESS
    - SAFE ...

### Software Engineering Circle

* Continuous Improvement (Kaizen)
* ‘Waterfall’ Phases
    - Requirements Elicitation
    - Architecture and Design
    - Development
    - Verification & Validation
    - Deployment & Maintenance
* Management Models
* Procedure Models
* Project-/Increment-Management
* Product/Lifecycle- Management
* Quality Management
* Methodologies
* Technologies
* Best Practices
* Tools

## Chapter 3

### How to apply the patterns

* Decision #1: Monolithic architecture or microservice architecture?
* Decision #2: How to decompose an application into services?
    - Monolithic architecture pattern
    - Microservice architecture pattern
    - Decompose by business capability
    - Decompose by subdomain
* Decision #3: How to maintain data consistency and perform queries?
    - Database per service pattern vs. Shared database pattern
    - Saga pattern
    - CQRS pattern

### ACID versus BASE: ACID

* ACID
    - Atomicity
    - Consistency
    - Isolation
    - Durability
* Prevalent design approach in ‘classical’ / low-scale distributed systems
  using (clustered) relational databases
    - Key Feature: Two-Phase Commit Distributed Transactions offering ‘strong’
      consistency

### CAP Theorem

* CAP
    - *C*onsistency
    - *A*vailablility
    - *P*artition Tolerance
* CAP: „You cannot have all 3“

### ACID versus BASE: BASE

* BASE
    - *B*asically *A*vailable
    - *S*oft state
    - *E*ventually consistent

* Prevalent design approach in highly scalable distributed systems
    - Key Feature: Horizontal Scalability supporting nearly unlimited
      transactions per second (but ‘weak’ consistency)
    - Used by globally acting service providers such as Social Media Services,
      Streaming Services etc.

### Decomposition: Decompose by business capability

* A business capability is a concept from business architecture modeling. It is
  something that a business does in order to generate value.

### Decomposition: Decompose by subdomain

* Define services corresponding to Domain-Driven Design (DDD) subdomains. DDD
  refers to the application’s problem space - the business as the domain. A
  domain consists of multiple subdomains. Each subdomain corresponds to a
  different part of the business.

### Decomposition: Service per team

* Each service is owned by a team, which has sole responsibility for making
  changes. Ideally each team has only one service.

### Data management: Database per Service

* Keep each microservice’s persistent data private to that service and
  accessible only via its API. A service’s transactions only involve its
  database.

### Data management: Shared database

* Solution: Use a (single) database that is shared by multiple services. Each
  service freely accesses data owned by other services using local ACID
  transactions.
* The drawbacks of this pattern are:
    - *Development time coupling* - a developer working on, for example, the
      OrderService will need to coordinate schema changes with the developers
      of other services that access the same tables. This coupling and
      additional coordination will slow down development.
    - *Runtime coupling* - because all services access the same database they can
      potentially interfere with one another. For example, if long running
      CustomerService transaction holds a lock on the ORDER table then the
      OrderService will be blocked.
    - Single database might not satisfy the data storage and access
      requirements of all services.

### Data management: Saga

Implement each business transaction that spans multiple services as a saga.

* A saga is a sequence of local transactions. Each local transaction updates
  the database and publishes a message or event to trigger the next local
  transaction in the saga.  If a local transaction fails because it violates a
  business rule then the saga executes a series of compensating transactions
  that undo the changes that were made by the preceding local transactions.

### Transactions: Transactional Outbox

* Problem: A service command typically needs to update the database and send
  messages/events.
* For example, a service that participates in a saga needs to atomically update
  the database and send messages/events.
* Similarly, a service that publishes a domain event must atomically update an
  aggregate and publish an event. The database update and sending of the
  message must be atomic in order to avoid data inconsistencies and bugs.
* However, it is not viable to use a distributed transaction that spans the
  database and the message broker to atomically update the database and publish
  messages/events.

### Transactions: Transactional Outbox

* *Solution:* A service that uses a relational database inserts messages/events
  into an outbox table as part of the local transaction. A separate Message
  Relay process publishes the events inserted into database to a message
  broker.
* *Problems of the solution:* The Message Relay might publish a message more than
  once (hence there is no “exactly once semantics”).
* It might, for example, crash after publishing a message but before recording
  the fact that it has done so.
* When it restarts, it will then publish the message again. As a result, a
  message consumer must be idempotent, perhaps by tracking the IDs of the
  messages that it has already processed.  Fortunately, since Message Consumers
  usually need to be idempotent (because a message broker can deliver messages
  more than once) this is typically not a problem.

### Cross cutting concerns: Microservices Chassis

* *Problem:* When you start the development of an application you often spend a
  significant amount of time putting in place the mechanisms to handle
  cross-cutting concerns. Examples of cross-cutting concerns include:
    - *Externalized configuration* - includes credentials and network locations
      of external services such as databases and message brokers
    - *Logging* - configuring of a logging framework such as log4j or logback
    - *Health checks* - a URL that a monitoring service can “ping” to determine
      the health of the application
    - *Metrics* - measurements that provide insight into what the application
      is doing and how it is performing
    - *Distributed tracing* - instrument services with code that assigns each
      external request a unique identifier that is passed between services.

### Cross cutting concerns: Microservices Chassis

* *Problem:* Cross cutting concerns code use is manifold in a service
* *Solution:* Build your microservices using a microservice chassis framework,
  which handles cross-cutting concerns.
* Examples of microservice chassis frameworks
    - Java
        - Spring Boot and Spring Cloud
        - Dropwizard
    - Go
        - Gizmo
        - Micro
        - Go kit

### Sidecar Pattern

* Solution: Co-locate a cohesive set of tasks with the primary application, but
  place them inside their own process or container, providing a homogeneous
  interface for platform services across languages.

### Communication style: Remote Procedure Invocation

* *Problem:* How do services in a microservice architecture communicate?
* *Solution:* Use RPI for inter-service communication. The client uses a
  request/reply-based protocol to make requests to a service.
There are numerous examples of RPI technologies:
    * REST
    * gRPC
    * Apache Thrift

### Service discovery: Client-side discovery

* Use of a Service Registry
    - Compare e.g. to the Java RMI Registry
* Single Point of Failure has to be tackled via High Availability Deployment
* Examples:
    - Apache Zookeeper
    - Consul
    - Etcd
    - Netflix Eureka

### Service discovery: Server-side discovery

* When making a request to a service, the client makes a request via a router
  (aka load balancer) that runs at a well-known location.
* The router queries a service registry, which might be built into the router,
  and forwards the request to an available service instance.
* An AWS Elastic Load Balancer (ELB) is an example of a server-side discovery
  router.

### Reliability: Curcuit Breaker

* *Problem:* How to prevent a network or service failure from cascading to other
  services?
* *Solution:* When the number of consecutive failures crosses a threshold, the
  circuit breaker trips, and for the duration of a timeout period all attempts
  to invoke the remote service will fail immediately.
    - Example: Netflix Hystrix

### Reliability: Curcuit Breaker

* The Curcuit Breaker has different configurable reactions to a client. Instead
  of routing the request to the overloaded resource, the curcuit breaker
  immediately
    - Returns an error
    - Returns a pre-defined default value
    - Returns the last value returned form the service
* Curcuit breakers
    - decrease latency
    - stop cascading failure
    - enable resilience where failure is inevitable

### Security: Access Token

* *Problem:* How to communicate the identity of the requestor to the services
  that handle the request?
* *Solution:* The API Gateway authenticates the request and passes an access
  token (e.g. JSON Web Token) that securely identifies the requestor in each
  request to the services. A service can include the access token in requests
  it makes to other services.
* *Example:* See JSON Web Token for usage examples and supporting libraries.

## Chapter 4

* Service Meshes: linkerd and istio

### What is a service mesh?

* In software architecture, a service mesh is a
    - dedicated infrastructure layer
    - for facilitating service-to-service communications between microservices
    - often using a sidecar proxy
* Implementations
    - Consul
    - Istio
    - Kuma
    - Linkerd
    - Maesh
    - Grey Matter
* Related Patterns
    - Proxy
    - Reverse Proxy
    - Interceptor
    - Decorator
    - Sidecar
* *Data Plane:* The proxies form the data plane
    - Proxies are Layer 7-aware TCP proxies, such as haproxy or NGINX
* *Control Plane:* Management processes controlling/using data plane

### What is linkerd?

* “Ultralight, security-first service mesh for Kubernetes”
* Data Plane
    - Uses proxies written in Rust: ‘linkerd-proxy’
        - Proxies act as proxy and reverse-proxy
    - Implement a feature set that focuses on the calls between services, not
    to the outside world as API gateways or ingress proxies
* Control Plane
    - Focuses on service discovery, TLS certificate issuing, metrics
    aggregation, etc.
* Microservice and proxy run in the same pod, proxy as a sidecar

### Why using a service mesh?

* Linkerd, like most meshes, has a Layer 7 feature set focused primarily on
HTTP calls, including HTTP/2 and gRPC.
* The feature set can be divided into three classes:
    - Reliability features. Request retries, timeouts, canaries (traffic
      splitting/shifting), etc.
    - Observability features. Aggregation of success rates, latencies, and
      request volumes for each service, or individual routes; drawing of
      service topology maps; etc.
    - Security features. Mutual TLS, access control, etc.
* Many of these features operate at the request level (hence the “L7 proxy”).

### Why using a service mesh?

* Service meshes tackle specific challanges of highly distributed systems
* Instead of in-process calls in monoliths causing high coupling and low
exchangeability microservice-based systems use remote procedure calls between
loosely-coupled self-deployed services
* Different feature layers

|              | Observability                              | Reliability                                          | Security                                          |
|:-------------|:-------------------------------------------|:-----------------------------------------------------|:--------------------------------------------------|
| Service Mesh | Service success rates                      | Request retries                                      | Mutual TLS between all services                   |
| Platform     | Log aggregation                            | Multiple replicas of dataset                         | Ecryption of data at rest                         |
| Application  | Instrumentation of internal features usage | Handling of failure when an entire component is down | Ensuring users only have access to their own data |

### What is istio?

* ‘Connect, secure, control, and observe services.’
* Main features
    - Traffic management
    - Security
    - Observablity
    - Extensibility

### Differences: linkerd vs. istio

* Istio uses Envoy as proxies, linkerd linkerd-proxy
    - Envoy is written in C++, linkerd-proxy in Rust
* Linkerd is bound to be used on Kubernetes, istio not
* Linkerd has a admin dashboard, istio not
* Istio has built-in tracing capabilites, linkerd not
* Istio has more features

### Summary: Why service meshes?

* Automatic load balancing
* Fine-grained control of traffic behavior with routing rules, retries,
  failovers etc.
* Pluggable policy layer
* Configuration API supporting access controls, rate limits and quotas
* Service discovery
* Service monitoring with automatic metrics, logs and traces for all traffic
* Secure service to service communication

### Service mesh: Key use cases

* Service discovery
    - A service mesh provides service-level visibility and telemetry, which
      supports service inventory information and dependency analysis.
* Operation reliability
    - Metrics data from service mesh allows you to see how your services are
      performing. For example, how long did it take it to respond to service
      requests and how much resource it is using. This data is useful to detect
      issues and correct them.
* Traffic governance
    - With service meshes you can configure the mesh network to perform
      fine-grained traffic management policies without going back and changing
      the application. This includes all ingress and egress traffic to and from
      the mesh.
* Access control
    - With service meshes you can assign policies that a service request can be
      granted only based on the location where the request came and can only
      succeed if the requester passes the health check.
* Secure service-to-service communications
    - You can enforce mutual TLS for service-to-service communications for all
      your service in mesh. Also you can enforce service-level authentication
      using either TLS or JSON web tokens.

### Ingress vs. Egress

* Ingress
    - Incoming traffic to a pod
    - An API object that manages external access to the services in a cluster,
      typically HTTP.
    - Ingress may provide load balancing, SSL termination and name-based
      virtual hosting.
* Egress
    - Outgoing traffic from a pod

## Chapter 5

### What are Micro Frontends?

* The term Micro Frontends first came up in ThoughtWorks Technology Radar at
  the end of 2016
* It extends the concepts of micro services to the frontend world
* The idea behind Micro Frontends is to think about a website or web app as a
  composition of features which are owned by independent teams
* Each team has a distinct area of business or mission it cares about and
  specializes in
* A team is cross functional and develops its features end-to-end, from
  database to user interface

### Micro Frontends: Monolith vs. Microservices

Monolithic Frontend Team seemed long time to limit potential of microservices

### Conway‘s Law and fighting it

* Conway’s law says that the interface structure of a software system will
  reflect the social structure of the organization that produced it.
* Inverse conway manoeuvre recommends evolving your team and organizational
  structure to promote your desired architecture. Ideally your technology
  architecture will display isomorphism with your business architecture.

### Core Ideas behind Micro Frontends

* Be Technology Agnostic
    - Each team should be able to choose and upgrade their stack without having
      to coordinate with other teams. Custom Elements are a great way to hide
      implementation details while providing a neutral interface to others.
* Isolate Team Code
    - Don’t share a runtime, even if all teams use the same framework. Build
      independent apps that are self contained. Don’t rely on shared state or
      global variables.
* Establish Team Prefixes
    - Agree on naming conventions where isolation is not possible yet.
      Namespace CSS, Events, Local Storage and Cookies to avoid collisions and
      clarify ownership.
* Favor Native Browser Features over Custom APIs
    - Use Browser Events for communication instead of building a global PubSub
      system. If you really have to build a cross team API, try keeping it as
      simple as possible.
* Build a Resilient Site
    - Your feature should be useful, even if JavaScript failed or hasn’t
      executed yet. Use Universal Rendering and Progressive Enhancement to
      improve perceived performance.

### Custom Elements

* Are the interoperability aspect from the Web Components Spec
* Are a good primitive for integration in the browser
* Each team builds their component using their web technology of choice and
  wraps it inside a Custom Element
    - e.g. `<order-minicart></order-minicart>`
* The DOM specification of this particular element (tag-name, attributes &
  events) acts as the contract or public API for other teams.
* The advantage is that they can use the component and its functionality
  without having to know the implementation.
* They just have to be able to interact with the DOM

### Client-Side Integration using Custom Elements

Buy button: Team Product includes the button by simply adding `<blue-buy
sku="t_porsche"></blue-buy>` to the desired position in the markup.  For this
to work, Team Checkout has to register the element blue-buy on the page.

### Serverside Rendering using Server Side Includes

```html
<blue-buy sku="t_porsche">
    <!--#include virtual="/blue-buy?sku=t_porsche" -->
</blue-buy>
```

* The #include comment is part of Server Side Includes (SSI), which is a
  feature that is available in most web servers
* There are also a few alternative techniques like ESI, nodesi, compoxure and
  tailor, but SSI is recommended by Michael Geers
* The #include comment is replaced with the response of
  `/blue-buy?sku=t_porsche` before the web server sends the complete page to
  the browser.

Works with JavaScripts disabled!

## Chapter 6

### Testing: Testing in Production

* A/B Testing (split testing)
    - User Group A uses Service A
    - User Group B uses Service B
    - A comparator service analyzes which service performs better
* Canary testing
    - A small group of users is routed to the new service
    - If the tests succeed, all the users are switched over to the new service
* Both approaches are facilitated by a microservices architecture

### Tools: Helm - the package manager for Kubernetes

* A Chart is a Helm package
    - Contains all of the resource definitions necessary to run an application,
      tool, or service inside a Kubernetes cluster. Think of it like the
      Kubernetes equivalent of a Homebrew formula, an Apt dpkg, or a Yum RPM
      file.
* A Repository is the place where charts can be collected and shared
    - Like Perl's CPAN archive or the Fedora Package Database, but for
      Kubernetes packages.
* A Release is an instance of a chart running in a Kubernetes cluster
    - One chart can often be installed many times into the same cluster. And
      each time it is installed, a new release is created.
    - Consider a MySQL chart: if you want two databases running in your
      cluster, you can install that chart twice. Each one will have its own
      release, which will in turn have its own release name.

Helm installs charts into Kubernetes, creating a new release for each
installation.  To find new charts, you can search Helm chart repositories.

### Immutable Infrastructure Principle

* Immutable infrastructure principle often used with microservices
    - “if you need to add or rewrite some of the code in a deployed
      microservice that’s working well, the best approach is usually to create
      a new microservice for the new or changed code, leaving the existing
      microservice in place”
    - New/changed code always results in a new microservice version (e.g. in a
      new container instance)
        - → a once deployed a microservice is immutable
    - If a microservice grows too big → split it up

### Tools: Why Helm?

* Manage complexity
* Easy Updates
* Simple sharing
* Defined rollbacks
* Enables - together with other tools like Terraform - infrastructure as code
  (IAC) on Kubernetes
    - Helm focuses more on software deployment
    - Terraform focuses more on infrastructure deployment

## Chapter 7

### Architectural Style Wrap-Up:

MOA, SOA, MSA

* Monolithic Architecture (MOA)
* Service-Oriented Architecture (SOA)
* Microservices Architecture (MSA)

### MSA versus SOA

* ‘1 service owns 1 database’ versus ‘n services access a small number of
  enterprise databases’
* Simpler ‘JSON via REST’ versus more complex ‘WS*’ inter-service communication
* BASE-like versus ACID-like
* ‘Reactive fail-fast’ versus ‘wait for timeout’
* Horizontal scalability versus vertical scalability
* Scalability via functional decomposition* in addition to horizontal
  scalability
* Evolution by revolution (recreation) versus modification (refactoring)
    - Immutability versus volatility

### The Art of Scalability

Functional decomposition into microservices
