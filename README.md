# Zero-to-Production

![Zero-to-Production](/assets/banner.png)

A curated, opinionated collection of resources to make anything production-grade
(APIs, backends, systems, infra, platforms, products)

> Production-grade ≠ fancy architecture

### Table of Contents

- [API](#api)
- [Backend](#backend)
- [Database](#database)
- [Deployment](#deployment)
- [Monitoring & Observability](#monitoring--observability)
- [Reliability](#reliability)
- [Security](#security)
- [Production Scaling](#production-scaling)
- [Infrastructure and DevOps](#infrastructure-and-devops)
- [Engineering Practices](#engineering-practices)

---

### API

#### **Design & Architecture**

#### REST & HTTP

- **[Zalando RESTful API Guidelines](https://opensource.zalando.com/restful-api-guidelines/)** - One of the most comprehensive guides on the internet. Covers naming, versioning, and JSON structure with extreme detail.
- **[Microsoft REST API Guidelines](https://github.com/microsoft/api-guidelines)** - The standard for durability and consistency.
- **[Google Cloud API Design Guide](https://cloud.google.com/apis/design)** - Focuses on resource-oriented design, valuable even if you aren't using gRPC.
- **[Idempotency Keys (Stripe)](https://stripe.com/blog/idempotency)** - Mandatory reading. How to handle network failures safely by preventing duplicate transactions.
- **[RFC 7807: Problem Details for HTTP APIs](https://tools.ietf.org/html/rfc7807)** - Stop inventing your own error formats. Use the standard.

#### GraphQL

- **[Production Ready GraphQL](https://book.productionreadygraphql.com/)** - (Book/Resources) The definitive guide on things like caching, rate limiting, and schema design in GraphQL.
- **[Designing GraphQL Schemas (Shopify)](https://github.com/Shopify/graphql-design-tutorial)** - Shopify runs one of the world's largest public GraphQL APIs. Their design tutorial is battle-tested.
- **[GraphQL at Scale (Twitter/X)](https://www.google.com/search?q=https://www.youtube.com/watch%3Fv%3DzVNxqhyfW1A)** - Lessons learned migrating a massive architecture to GraphQL.

#### gRPC & RPC

- **[Uber's switch to Google's Protocol Buffers](https://www.google.com/search?q=https://eng.uber.com/architecture-api-gateway/)** - Why JSON/REST wasn't enough for high-throughput internal services.
- **[Buf](https://buf.build/)** - Not just a tool, but their documentation and blog provide modern best practices for managing Protobuf files in production.

#### **Security**

- **[API Security Checklist](https://github.com/shieldfy/API-Security-Checklist)** - A concise list of counter-measures against common attacks.
- **[OWASP API Security Top 10](https://owasp.org/www-project-api-security/)** - The threat model you must design against (BOLA, Broken Auth, etc.).
- **[Phantom Token Pattern](https://curity.io/resources/learn/phantom-token-pattern/)** - How to use opaque tokens for public clients while utilizing JWTs internally for performance.
- **[RFC 6749: The OAuth 2.0 Authorization Framework](https://datatracker.ietf.org/doc/html/rfc6749)** - Dense, but necessary if you are implementing your own provider (which you generally shouldn't).

#### **Reliability & Scaling**

#### Rate Limiting & Load Shedding

- **[Scaling your API with Rate Limiters (Stripe)](https://stripe.com/blog/rate-limiters)** - Discusses different algorithms (Token Bucket, Leaky Bucket) and distributed counting.
- **[Google SRE Book: Handling Overload](https://sre.google/sre-book/handling-overload/)** - The concept of "Load Shedding" (dropping requests to save the service) is critical for Tier-1 APIs.
- **[Stop Rate Limiting! Capacity Management at Netflix](https://www.google.com/search?q=https://www.youtube.com/watch%3Fv%3DFqMoLkzp11g)** - A counter-intuitive approach to concurrency limits over simple rate limits.

#### Caching

- **[Caching Best Practices](https://jakearchibald.com/2016/caching-best-practices/)** - Deep dive into `Cache-Control`, `Etag`, and the `Vary` header.
- **[Things I Wish I Knew About Redis](https://www.google.com/search?q=https://hackernoon.com/3-things-i-wish-i-knew-about-redis-before-using-it-5e728469H)** - Practical operational advice for using Redis as a cache backing for APIs.

#### Observability & Evolution

- **[APIs as Infrastructure (Stripe)](https://stripe.com/blog/api-versioning)** - How to maintain years of backwards compatibility using a "version gates" middleware approach.
- **[The Golden Signals (Google)](https://sre.google/sre-book/monitoring-distributed-systems/)** - If you only measure four things on your API, measure Latency, Traffic, Errors, and Saturation.
- **[Spec-Driven Development](https://www.google.com/search?q=https://www.youtube.com/watch%3Fv%3D2Xl7V_FqVqo)** - Why you should write your OpenAPI (Swagger) spec _before_ you write code, and how to lint it automatically.

#### Reference Implementations & Tools

- **[Spectral](https://github.com/stoplightio/spectral)** - A flexible JSON/YAML linter for API specifications. Enforce style guides (camelCase, descriptions required) via CI/CD.
- **[OpenAPI Generator](https://github.com/OpenAPITools/openapi-generator)** - Generate clients/servers from specs. Don't write SDKs by hand.
- **[Prisma Examples](https://github.com/prisma/prisma-examples)** - While DB focused, their patterns for REST and GraphQL server setups are clean and production-oriented.

### **Backend**

#### Service Boundaries & Ownership

- **[Deconstructing the Monolith (Shopify)](https://engineering.shopify.com/blogs/engineering/deconstructing-monolith-designing-software-maximizes-developer-productivity)**
  How Shopify enforces modularity within a massive Ruby on Rails monolith to avoid the complexity tax of microservices while maintaining developer velocity.

- **[Domain-Oriented Microservice Architecture (Uber)](https://www.google.com/search?q=https://eng.uber.com/microservice-architecture/)**
  Uber's pivot away from "microservice sprawl" toward grouped domains. A critical look at the operational overhead of having too many services.

- **[Microservices (Martin Fowler)](https://martinfowler.com/articles/microservices.html)**
  The foundational text, but specifically the section on "Smart endpoints and dumb pipes" and the operational requirements pre-requisite to adoption.

- **[Context Mapping (Domain-Driven Design)](https://github.com/ddd-crew/context-mapping)**

#### Asynchronous Processing & Messaging

- **[The Log: What every software engineer should know about real-time data's unifying abstraction (LinkedIn)](https://www.google.com/search?q=https://engineering.linkedin.com/distributed-systems/log-what-every-software-engineer-should-know-about-real-time-datas-unifying-abstraction)**
  Jay Kreps (co-creator of Kafka) explains why the commit log is the heart of distributed backend systems, not just a database detail.

- **[What We Learned from Reading 120+ Postmortems (KubeCon)](https://www.google.com/search?q=https://www.youtube.com/watch%3Fv%3D0wWmDkP0UeU)**
  An analysis of failure patterns, highlighting how cascading failures often stem from synchronous dependencies that should have been asynchronous.

- **[Delivery Guarantees (Segment)](https://www.google.com/search?q=https://segment.com/blog/exactly-once-delivery/)**
  A realistic look at "exactly-once" delivery (and why it's mostly a myth), and how to architect for "at-least-once" with deduplication.

#### Background Jobs & Workers

- **[Scaling the Job Queue (Stripe)](https://www.google.com/search?q=https://stripe.com/blog/scaling-the-job-queue)**
  How Stripe manages rate limiting, fair consumption, and tenancy within their massive background job infrastructure.

- **[The Art of Sidekiq](https://github.com/mperham/sidekiq/wiki/Best-Practices)**
  While specific to Ruby, the principles here (idempotency, argument size limits, error handling) are universal for any worker-based system.

- **[Delay Queues (Amazon Builders' Library)](https://aws.amazon.com/builders-library/avoiding-insurmountable-queue-backlogs/)**
  Strategies for avoiding "insurmountable queue backlogs" during outages. Discusses load shedding and prioritizing traffic when workers are overwhelmed.

#### Idempotency & Distributed State

- **[Implementing Stripe-like Idempotency Keys](https://www.google.com/search?q=https://github.com/brandur/sorbets)**
  A reference implementation demonstrating how to lock, execute, and store responses to ensure safe retries in a distributed system.

- **[Starbucks Does Not Use Two-Phase Commit](https://www.enterpriseintegrationpatterns.com/ramblings/18_starbucks.html)**
  Gregor Hohpe explains eventual consistency using a real-world coffee shop analogy. It illustrates how to design systems that tolerate inconsistent state temporarily to maximize throughput.

- **[Distributed Locking (Redis)](https://www.google.com/search?q=https://redis.io/docs/manual/patterns/distributed-locks/)**
  The Redlock algorithm. Essential reading to understand the dangers of locking in distributed environments (clock drift, fencing tokens).

#### Resilience Patterns

- **[Circuit Breaker Pattern (Microsoft)](https://learn.microsoft.com/en-us/azure/architecture/patterns/circuit-breaker)**
  Technical implementation details of failing fast to preserve system resources during downstream outages.

- **[Making Retries Safe with Idempotent APIs (Amazon Builders' Library)](https://aws.amazon.com/builders-library/making-retries-safe-with-idempotent-APIs/)**
  Detailed guidance on retry storms, exponential backoff, and jitter. Explains why "retry immediately" is a production killer.

- **[The SRE Book: Addressing Cascading Failures (Google)](https://sre.google/sre-book/addressing-cascading-failures/)**
  A taxonomy of triggers for cascading failures (resource exhaustion, death spirals) and heuristics for preventing them.

### **Database**

- **[The SRE Book: Addressing Cascading Failures (Google)](https://sre.google/sre-book/addressing-cascading-failures/)**

#### Schema Migrations & Zero Downtime

- **[Online Schema Migrations at Scale (GitHub)](https://github.com/github/gh-ost)** `gh-ost` is GitHub's triggerless online schema migration tool for MySQL. The README and design docs explain why triggers are dangerous and how to migrate via binary logs.

- **[Safe Database Migrations Pattern (Stripe)](https://stripe.com/blog/online-migrations)** A masterclass in the "expand and contract" pattern. Explains how to dual-write to old and new columns to ensure backward compatibility during a rollout.

- **[PostgreSQL at Scale: Database Schema Changes Without Downtime](https://www.google.com/search?q=https://medium.com/paypal-tech/postgresql-at-scale-database-schema-changes-without-downtime-20d3749ed680)** PayPal's engineering team details lock contention issues in Postgres and how to use `SET LOCK_TIMEOUT` to prevent migration scripts from halting production traffic.

#### Performance & Indexing

- **[Use The Index, Luke](https://use-the-index-luke.com/)** The definitive guide to SQL indexing. Explains B-Trees, concantenated keys, and the performance impact of `OFFSET` pagination.

- **[Postgres Indexing: When to use what](https://www.google.com/search?q=https://www.youtube.com/watch%3Fv%3DclrteT8dYfk)** A deep dive into B-Tree vs. GIN vs. GiST indexes. Essential for understanding which data structure fits your access patterns (e.g., full-text search vs. standard lookups).

- **[Uber’s move from Postgres to MySQL (and back again)](https://www.google.com/search?q=https://eng.uber.com/postgres-to-mysql-migration/)** A controversial but educational piece on write amplification, buffer pool usage, and why architecture decisions depend heavily on the specific I/O patterns of the workload.

#### Connection Management & Saturation

- **[PgBouncer](https://www.pgbouncer.org/)** In production Postgres, you almost always need a connection pooler. The docs explain distinct pooling modes (Session vs. Transaction) which fundamentally change how your app behaves.

- **[The Life of a Database Transaction](https://www.google.com/search?q=https://www.cockroachlabs.com/blog/life-of-a-distributed-transaction/)** Visualizing the path of a query. Helps engineers understand where latency comes from (network RTTs, latch contention, disk I/O).

- **[Handling Overload: Queuing Theory in Practice](https://sre.google/sre-book/handling-overload/)** While general to SRE, this chapter is crucial for DBAs. It explains why adding more connections during a slowdown often makes the database slower (Little's Law).

#### Disaster Recovery & Integrity

- **[GitLab.com Database Incident Postmortem](https://about.gitlab.com/blog/2017/02/10/postmortem-of-database-outage-of-january-31/)** The most transparent database outage report in history. A tired engineer accidentally deleted the production DB, and _five_ different backup/replication mechanisms failed. A must-read for reality checks.

- **[Files are hard (SQLite)](https://sqlite.org/howtocorrupt.html)** An enlightening list of ways to corrupt a database file (e.g., file locking failures, disk sync lies). It highlights how much databases rely on the OS to tell the truth.

- **[Point-in-Time Recovery (PITR) Concepts](https://www.postgresql.org/docs/current/continuous-archiving.html)** Official docs explaining WAL (Write Ahead Log) archiving. You cannot claim to have a production database if you cannot replay logs to restore to a specific timestamp before a bad deployment.

### **Deployment**

#### Progressive Delivery (Canary & Blue/Green)

- **[Flagger: Progressive Delivery Operator](https://github.com/fluxcd/flagger)** A Kubernetes operator that automates the promotion of canary deployments using service mesh metrics (Istio, Linkerd). It demonstrates the pattern of "automated analysis" where software, not humans, decides if a release is safe.

- **[BlueGreenDeployment (Martin Fowler)](https://martinfowler.com/bliki/BlueGreenDeployment.html)** The definitive definition of Blue/Green. Key takeaway: Use this for instant rollbacks (switching the router) rather than just deployment safety.

- **[Six Strategies for Microservices Deployment](https://www.google.com/search?q=https://thenewstack.io/deployment-strategies-defined/)** A comparative analysis of Recreate, Ramped (Rolling), Blue/Green, Canary, and A/B testing. Essential for choosing the right strategy based on resource cost vs. safety needs.

#### Feature Flags & Decoupling

- **[Feature Toggles (aka Feature Flags)](https://martinfowler.com/articles/feature-toggles.html)** The comprehensive guide to Release Toggles, Ops Toggles, and Permission Toggles. It explains how to manage the complexity of "toggle debt" so your code doesn't become a graveyard of `if/else` statements.

- **[Dark Launching (Facebook/Meta)](https://www.google.com/search?q=https://engineering.fb.com/2012/06/15/core-data/under-the-hood-facebook-gradually-releasing-the-messenger-for-windows-desktop-app/)** How Facebook (and specifically the Gatekeeper system) releases code to production "dark" (inactive) to test infrastructure load before users ever see the feature.

- **[LaunchDarkly: The definitive guide to feature management](https://launchdarkly.com/blog/what-are-feature-flags/)** While a vendor blog, their explanation of using flags for "Kill Switches" and "Circuit Breakers" in production is industry standard.

#### The "Staging" Problem & Environment Parity

- **[Staging Is a Lie](https://www.google.com/search?q=https://medium.com/%40copyconstruct/testing-in-production-the-safe-way-18ca102d0bab)** Cindy Sridharan argues that since staging environments can never truly replicate production traffic or data volume, we must invest in "Testing in Production" (TiP) via observability, canarying, and feature flagging.

- **[The Google SRE Book: Release Engineering](https://sre.google/sre-book/release-engineering/)** How Google handles hermetic builds. If your build relies on external libraries that can change (e.g., `npm install` without a lockfile), your deployment is non-deterministic and dangerous.

#### Rollbacks & Failure Recovery

- **[The Knight Capital Group Deployment Error](https://dougseven.com/2014/04/17/knightmare-a-devops-cautionary-tale/)** The most expensive deployment error in history ($440 million lost in 45 minutes). Caused by a failed deployment where one server ran old code while others ran new code, repurposing a flag. A brutal lesson in configuration management and verifying deployment success.

- **[Why Rollbacks Are Hard](https://www.google.com/search?q=https://codeascraft.com/2010/05/20/code-deployment-at-etsy/)** Etsy explains why "rolling back" isn't always possible (e.g., after a database migration). Introduces the concept of "Rolling Forward" (fixing the bug) as often the safer, albeit scarier, option.

- **[Automating Safe Rollbacks (Netflix Spinnaker)](https://www.google.com/search?q=https://netflixtechblog.com/global-continuous-delivery-with-spinnaker-2a85e8a7861b)** How Netflix automates the "Red/Black" (their term for Blue/Green) deployment and rollback process. If health checks fail, the old ASG (Auto Scaling Group) is re-enabled automatically.

### **Monitoring & Observability**

#### Logging: Structured & Canonical

- **[Canonical Log Lines (Stripe)](https://stripe.com/blog/canonical-log-lines)** The single most impactful logging pattern. Instead of emitting 10 log lines per request, emit _one_ wide, structured event containing all context (duration, status, user_id, DB_time). This makes aggregation and debugging infinitely cheaper and faster.

- **[Logs are Streams (12-Factor App)](https://12factor.net/logs)** The foundational rule for modern deployment: apps should never manage log files. They should write to `stdout`/`stderr`, allowing the execution environment to capture and route the stream.

- **[Structured Logging (Uber)](https://www.google.com/search?q=https://eng.uber.com/logging/)** Uber's evolution from unstructured text to strongly typed, schema-backed logging. Essential for ensuring that a change in log format doesn't break your ingestion pipeline.

#### Metrics: The Golden Signals

- **[The Four Golden Signals (Google SRE Book)](https://www.google.com/search?q=https://sre.google/sre-book/monitoring-distributed-systems/%23xref_monitoring_golden-signals)** If you measure nothing else, measure Latency, Traffic, Errors, and Saturation. This is the industry standard for high-level service health.

- **[The RED Method (Weaveworks)](https://www.google.com/search?q=https://www.weave.works/blog/the-red-method-key-metrics-for-microservices-architecture/)** A derivative of Golden Signals specifically for microservices: Rate (requests/sec), Errors (failed requests/sec), and Duration (latency distribution).

- **[The USE Method (Brendan Gregg)](https://www.brendangregg.com/usemethod.html)** The counterpart to RED/Golden Signals. While those measure _service_ health, USE (Utilization, Saturation, Errors) measures _resource_ health (CPU, Disk, Memory). Essential for debugging infrastructure bottlenecks.

#### Distributed Tracing

- **[Dapper, a Large-Scale Distributed Systems Tracing Infrastructure (Google)](https://research.google/pubs/dapper-a-large-scale-distributed-systems-tracing-infrastructure/)** The paper that started it all. It explains the core concepts of Spans, Traces, and the necessity of _sampling_ (recording only 0.01% of requests) to keep overhead low in massive systems.

- **[Observability 3 Ways (Charity Majors)](https://www.google.com/search?q=https://www.honeycomb.io/blog/observability-3-ways-logging-metrics-tracing)** Charity Majors argues that metrics are insufficient for "unknown unknowns." Explains why high-cardinality data (e.g., grouping by `user_id` or `order_id`) is the only way to debug localized failures in production.

- **[OpenTelemetry Architecture](https://opentelemetry.io/docs/concepts/signals/traces/)** The current industry standard for instrumentation. Understanding Context Propagation (how a Trace ID hops from HTTP headers to gRPC metadata) is critical for implementing tracing correctly.

#### Alerting & Incident Response

- **[My Philosophy on Alerting (Rob Ewaschuk, Google)](https://docs.google.com/document/d/199PqyG3UsyXlwieHaqbGiWVa8eMWi8zzAn0YfcApr8Q/edit)** The manifesto on "Symptom-based Alerting." You should alert on "User is seeing errors," not "CPU is high." High CPU is a cause, not a symptom.

- **[On-Call Rotations and Alert Fatigue](https://www.google.com/search?q=https://increment.com/on-call/dealing-with-alert-fatigue/)** Practical strategies for grooming alerts. If an alert fires and no action is taken, it should be deleted.

- **[Runbooks (PagerDuty)](https://www.google.com/search?q=https://response.pagerduty.com/before/runbooks/)** Alerts must link to a runbook. This guide explains what a runbook needs: "What is happening?", "Impact?", and "Mitigation steps" (not just "fix steps," but how to stop the bleeding).

### **Reliability**

#### Timeouts & Latency Control

- **[Timeouts, Retries, and Backoff with Jitter (Amazon Builders' Library)](https://aws.amazon.com/builders-library/timeouts-retries-and-backoff-with-jitter/)** The definitive guide on why static timeouts are dangerous and how to implement "Jitter" (randomness) to prevent thundering herds.

- **[The Tail at Scale (Google)](https://research.google/pubs/the-tail-at-scale/)** Dean and Barroso explain why the 99th percentile latency matters more than the average. It introduces techniques like "Hedged Requests" (sending two requests, taking the fastest) to tame tail latency.

- **[Go net/http Timeouts](https://blog.cloudflare.com/the-complete-guide-to-golang-net-http-timeouts/)** A Cloudflare classic. Even if you don't write Go, the diagrams illustrating `ConnectTimeout` vs. `ReadTimeout` vs. `WriteTimeout` are universal concepts for any TCP-based service.

#### Retries & Storms

- **[Addressing Cascading Failures (Google SRE Book)](https://sre.google/sre-book/addressing-cascading-failures/)** A masterclass in failure modes. It explains "Positive Feedback Loops" where a service gets slow, clients retry, load increases, and the service dies completely.

- **[Preventing Retry Storms with Token Buckets (Uber)](https://www.google.com/search?q=https://eng.uber.com/reliability-retry-logic/)** How Uber implements a "Retry Budget." Services are only allowed to retry a certain percentage of traffic (e.g., 10%). If errors exceed that, retries are disabled to save the downstream system.

#### Circuit Breakers & Bulkheads

- **[Circuit Breaker Pattern (Microsoft Azure)](https://learn.microsoft.com/en-us/azure/architecture/patterns/circuit-breaker)** The standard reference for the Open/Closed/Half-Open state machine. Essential for understanding how to give a failing service time to recover.

- **[Hystrix: Defending Your App (Netflix)](https://github.com/Netflix/Hystrix/wiki)** While Hystrix is in maintenance mode, its Wiki remains the bible of reliability patterns. It defines "Bulkheading"—isolating thread pools so that a crash in the Image Service doesn't take down the User Service.

- **[Resilience4j](https://github.com/resilience4j/resilience4j)** The modern, lightweight successor to Hystrix models. Browse the documentation to see practical implementations of Rate Limiters and Circuit Breakers in functional programming styles.

#### SLIs, SLOs, & Error Budgets

- **[Service Level Objectives (Google SRE Book)](https://sre.google/sre-book/service-level-objectives/)** The framework that changed the industry. Defines the **SLI** (what you measure), the **SLO** (the target), and the **SLA** (the legal contract).

- **[The Error Budget (Atlassian)](https://www.atlassian.com/incident-management/kpis/error-budget)** A practical guide to using Error Budgets to resolve the "Dev vs. Ops" conflict. If you have budget left, you ship features. If you burned it all, you freeze deployments and fix stability.

#### Graceful Degradation

- **[Patterns for Resilient Architecture (InfoQ)](https://www.google.com/search?q=https://www.infoq.com/articles/patterns-resilient-architecture/)** Discusses "Fallback" strategies. If the Recommendation Engine is down, don't show a 500 error; show a static list of "Most Popular Items" instead.

- **[Failing Gracefully (Slack)](https://www.google.com/search?q=https://slack.engineering/failing-gracefully/)** How Slack handles outages in non-critical systems (like link previews) without impacting core messaging functionality.

### **Security**

#### Secrets Management

- **[Why you shouldn't use ENV variables for secrets](https://www.google.com/search?q=https://diogomonica.com/2017/03/27/why-you-shouldnt-use-env-variables-for-secret-data/)** Diogo Mónica (Docker security lead) explains why the 12-Factor App methodology is dangerous for secrets. Env vars leak into logs, child processes, and error dumps.

- **[GitLeaks](https://github.com/gitleaks/gitleaks)** The industry standard for pre-commit hooks and CI checks. If you don't automate the detection of AWS keys in your commits, you will eventually leak one.

- **[The Uber Data Breach (2022)](https://www.uber.com/newsroom/security-update/)** A classic case of hardcoded PowerShell credentials leading to total compromise. A reminder that PAM (Privileged Access Management) is useless if the keys to the castle are in a script on a file share.

#### Authentication & Authorization

- **[Stop using JWT for sessions](http://cryto.net/~joepie91/blog/2016/06/13/stop-using-jwt-for-sessions/)** The most cited article on why Stateless JWTs are often a security theater trap. It advocates for standard session cookies unless you have specific microservice scale needs.

- **[Google Zanzibar: consistent, global authorization system](https://research.google/pubs/zanzibar-googles-consistent-global-authorization-system/)** How Google handles "can User A view Document B" at a global scale. It introduces the concept of "Relation Tuples" which inspired open source tools like OpenFGA and SpiceDB.

- **[OAuth 2.0 Threat Model (RFC 6819)](https://datatracker.ietf.org/doc/html/rfc6819)** You cannot implement OAuth safely without understanding the attacks against it (Token bleeding, CSRF on redirect, open redirectors).

#### Supply Chain & Dependencies

- **[Dependency Confusion: How I Hacked Apple, Microsoft and Dozens of Other Companies](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610)** Alex Birsan's legendary exploit showing how public package repositories (npm, PyPI) can trick build systems into installing public malware instead of private internal packages.

- **[The Log4Shell Postmortem (FTC/CISA)](https://www.google.com/search?q=https://www.cisa.gov/news-events/news/log4j-vulnerability-guidance)** The "Chernobyl" of software vulnerabilities. It highlights the impossibility of manual patching and the absolute necessity of SBOMs (Software Bill of Materials) to know what is running in your fleet.

- **[Sigstore](https://www.sigstore.dev/)** The modern standard for signing software artifacts. It solves the "how do I trust this binary?" problem using OIDC and transparency logs, moving away from the pain of GPG keys.

#### Defensive Engineering & API Security

- **[Credential Stuffing: The unexpected cost of simple passwords](https://owasp.org/www-community/attacks/Credential_stuffing)** Why you need rate limiting and 2FA. Users reuse passwords; when LinkedIn gets breached, your API will be hammered with those credentials.

- **[Server-Side Request Forgery (SSRF) Bible](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Request%20Forgery)** A terrifying collection of ways to trick a server into making internal requests (e.g., hitting the AWS Metadata service `169.254.169.254` to steal IAM roles).

- **[Capital One Data Breach (SSRF)](https://krebsonsecurity.com/2019/08/what-we-can-learn-from-the-capital-one-hack/)** A direct application of the SSRF vulnerability mentioned above. A misconfigured WAF allowed an attacker to query the metadata service and drain S3 buckets.

### **Production Scaling**

#### The Philosophy: Don't Scale Yet

- **[Choose Boring Technology (Dan McKinley)](https://mcfunley.com/choose-boring-technology)** The most important scaling advice ever written. Innovation tokens are limited; spend them on your core product, not on running a custom distributed database you found on Hacker News.

- **[The Majestic Monolith (Signal v. Noise)](https://m.signalvnoise.com/the-majestic-monolith/)** DHH argues that the network latency and operational overhead of microservices often outweigh the scaling benefits for 99% of companies.

- **[You Are Not Google](https://blog.bradfieldcs.com/you-are-not-google-84912cf44afb)** A reality check. Solving problems you don't have (e.g., building for 100M users when you have 100) creates technical debt that kills velocity.

#### Caching: The Sharpest Double-Edged Sword

- **[Scaling Memcache at Facebook](https://www.google.com/search?q=https://www.usenix.org/system/files/conference/nsdi13/nsdi13-paper-nishtala.pdf)** The holy grail of caching papers. It covers the "Thundering Herd" problem, "Gutter" servers, and how to handle cache consistency when you have billions of requests per second.

- **[Cache Stampede Protection (Instagram)](https://instagram-engineering.com/thundering-herds-promises-82191c8af57d)** How Instagram prevents the DB from melting when a celebrity posts. Explains the "Promise" pattern (or "Request Coalescing") where only one backend request is made for thousands of concurrent cache misses.

- **[Why we stopped using a CDN (Segment)](https://segment.com/blog/the-million-dollar-eng-problem/)** A counter-intuitive story. Sometimes the cache (CDN) introduces enough cost and complexity that simply optimizing the origin server is the better scaling move.

#### Database Sharding & Partitioning

- **[Sharding Pinterest: How we scaled our MySQL fleet](https://www.google.com/search?q=https://medium.com/%40pinterest_engineering/sharding-pinterest-how-we-scaled-our-mysql-fleet-3f341e96ca6f)** A brutally practical guide to manual sharding. No magic middleware—just intelligent application-level routing. Their ID generation scheme (embedding the shard ID in the primary key) is a standard pattern.

- **[Foursquare Outage Postmortem (2010)](https://foursquare.com/about/)** A classic lesson in what happens when you hit the limit of vertical scaling (RAM exhaustion) before your sharding logic is ready.

- **[Consistent Hashing (Tom White)](https://tom-e-white.com/2007/11/consistent-hashing.html)** If you shard modulo N, resizing the cluster requires moving 100% of data. Consistent hashing allows you to add nodes while moving only `1/N` of the data.

#### Asynchrony & Backpressure

- **[Backpressure Explained (Jay Kreps)](https://www.google.com/search?q=https://engineering.linkedin.com/distributed-systems/log-what-every-software-engineer-should-know-about-real-time-datas-unifying-abstraction)** In the context of "The Log," Kreps explains that if the consumer is slower than the producer, you only have three options: drop data, buffer data (until you crash), or block the producer (backpressure).

- **[Scaling Event Sourcing at New York Times](https://open.nytimes.com/publishing-with-apache-kafka-at-the-new-york-times-7f0e3b7d2077)** How the NYT replaced a monolithic CMS with a log-based architecture, allowing different consumers (Search, Archive, Web) to scale independently by reading the same immutable stream.

- **[Little's Law](https://en.wikipedia.org/wiki/Little%27s_law)** The formula `L = λW`. It mathematically proves why adding more worker threads to a slow database connection pool just increases latency without increasing throughput.

### **Infrastructure and DevOps**

#### Infrastructure as Code (IaC) & GitOps

- **[Terraform Best Practices](https://github.com/antonbabenko/terraform-best-practices)** The de facto community standard for structuring Terraform projects. It covers directory layout, module usage, and the critical importance of keeping state files remote and locked.

- **[Painful Lessons Teaching Terraform](https://www.google.com/search?q=https://blog.gruntwork.io/5-lessons-learned-from-writing-over-300-000-lines-of-infrastructure-code-36ba7face60)** Gruntwork.io shares the realities of IaC at scale: why modules should be small, why `count` is dangerous, and why you should avoid "one big state file" at all costs.

- **[Atlantis: Pull Request Automation for Terraform](https://github.com/runatlantis/atlantis)** How teams do Terraform in production. It moves the `terraform apply` step to the Pull Request comment thread, ensuring that what is reviewed is exactly what is deployed (and locking the state during the process).

#### Cloud Economics (FinOps)

- **[The Duckbill Group: AWS Bills](https://www.lastweekinaws.com/blog/)** Corey Quinn’s writings are essential for understanding that "Cost" is often an architectural failure. Topics include the hidden costs of NAT Gateways and data transfer fees that bankrupt startups.

- **[How we reduced our AWS bill by $500k](https://segment.com/blog/the-million-dollar-eng-problem/)** A classic Segment post. It details how "micro-optimizations" rarely work, and how big wins come from architectural shifts (like removing a CDN or changing instance families).

- **[Kubecost](https://github.com/kubecost/cost-model)** In Kubernetes, costs are obscured by shared tenancy. This tool breaks down spend by namespace/pod, allowing you to chargeback teams for the resources they actually hoard.

#### Disaster Recovery & Extinction Events

- **[Code Spaces: The Company That Was Murdered](https://arstechnica.com/information-technology/2014/06/aws-console-breach-leads-to-demise-of-service-with-proven-backup-plan/)** The ultimate cautionary tale. An attacker gained access to their AWS console and deleted everything, including the backups. The company ceased to exist in 12 hours. Lesson: Backups must be in a separate, isolated account.

- **[Disaster Recovery of Workloads on AWS](https://docs.aws.amazon.com/whitepapers/latest/disaster-recovery-workloads-on-aws/disaster-recovery-workloads-on-aws.pdf)** Defines the standard recovery strategies: **Backup & Restore** (Cheapest, Slowest), **Pilot Light**, **Warm Standby**, and **Multi-Site Active/Active** (Most Expensive, Zero Downtime). You must pick one _before_ the disaster.

- **[Testing Backups](https://www.backblaze.com/blog/the-3-2-1-backup-strategy/)** The "3-2-1 Strategy" (3 copies, 2 media types, 1 offsite). But more importantly: **A backup is not a backup until you have successfully restored from it.**

#### Immutable Infrastructure & Drift

- **[Immutable Infrastructure (O'Reilly)](https://www.google.com/search?q=https://www.oreilly.com/radar/what-is-immutable-infrastructure/)** The philosophy that once a server is deployed, it is never modified. No SSH, no `apt-get update`. This eliminates "configuration drift" where staging works but production fails because someone manually tweaked a setting 6 months ago.

- **[Snowflake Servers (Martin Fowler)](https://martinfowler.com/bliki/SnowflakeServer.html)** Explains the danger of servers that are unique and cannot be reproduced automatically. If you are afraid to restart a server, you have a Snowflake, and it is a ticking time bomb.

### **Engineering Practices**

#### Code Review & Quality Standards

- **[Google Engineering Practices: Code Review](https://google.github.io/eng-practices/review/)** The industry gold standard. It separates "The Standard of Code Review" (what to look for) from "The CL Author's Guide" (how to write reviewable code). Key takeaway: "In general, reviewers should favor approving a CL once it is in a state that improves the overall code health of the system, even if the CL isn't perfect."

- **[Code Review Developer Guide (Palantir)](https://www.google.com/search?q=https://github.com/palantir/generated-code-reviewers-guide/blob/master/google-engineering-practices.md)** A concise, practical guide. It emphasizes that the cost of reviewing code is expensive, so reviews should focus on architectural correctness and logic, not formatting (which should be linted automatically).

- **[Unlearning Descriptive Comments](https://www.google.com/search?q=https://swizec.com/blog/code-comments-are-a-smell/)** A look at why "What" comments are code smells. Comments should explain "Why" (business logic, weird constraints) because the code itself explains "How."

#### Technical Debt & Legacy Systems

- **[Technical Debt Quadrant (Martin Fowler)](https://martinfowler.com/bliki/TechnicalDebtQuadrant.html)** Distinguishes between "Deliberate" debt (shipping fast to validate) and "Inadvertent" debt (lack of knowledge). Crucial for having adult conversations with product management about _why_ we need to refactor.

- **[Migrations: The only way is through (Stripe)](https://www.google.com/search?q=https://stripe.com/blog/migrations)** Will Larson details how to survive massive technical migrations. It introduces the concept that the hardest part of a migration is not the code, but the "political" capital required to get other teams to prioritize your deprecation.

- **[Rewrite vs. Refactor](https://www.joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/)** Joel Spolsky’s famous warning against the "Grand Rewrite." Rewriting code from scratch is the single worst strategic mistake a software company can make, as it throws away years of bug fixes and edge-case knowledge.

#### Documentation & Knowledge Management

- **[The Documentation System (Divio)](https://documentation.divio.com/)** The "Grand Unified Theory" of documentation. It argues that there are four distinct types of docs that must be kept separate: **Tutorials** (learning-oriented), **How-To Guides** (problem-oriented), **Reference** (information-oriented), and **Explanation** (understanding-oriented). Mixing these confuses the reader.

- **[Architecture Decision Records (ADR)](https://github.com/joelparkerhenderson/architecture-decision-record)** A git-based standard for recording _why_ a decision was made. Instead of a wiki page that rots, you commit a markdown file (`doc/adr/001-use-postgres.md`) explaining the context, options considered, and the decision.

- **[GitLab Handbook](https://about.gitlab.com/handbook/)** The most extreme example of "public by default." It shows that a remote-first culture requires obsessive documentation of processes, not just code.

#### On-Call & Sustainable Operations

- **[How to Roster (PagerDuty)](https://www.google.com/search?q=https://response.pagerduty.com/oncall/rostering/)** Practical advice on rotation lengths, handoffs, and "shadow" rotations. It argues that if your on-call engineer is waking up more than twice a week, your system is broken, and feature development must stop to fix it.

- **[Blameless PostMortems (Etsy)](https://www.etsy.com/codeascraft/blameless-postmortems/)** The post that defined "Just Culture" in tech. If an engineer pushes a button and breaks prod, the question is not "Why were they stupid?" but "Why did the system allow that button to be pushed?"

- **[HumanOps](https://www.humanops.com/)** A resource collection focused on the health of the operators. It covers topics like "Alert Fatigue," "Sleep Health," and the psychological impact of incident response.
