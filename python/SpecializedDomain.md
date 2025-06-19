# Specialized Domain Q\&A Guide

## 🟦 Real-Time Systems

### 1. How do you design systems for low-latency requirements?

* Use edge computing to reduce latency.
* Adopt event-driven architecture.
* Optimize data serialization formats (e.g., Protobuf).
* Use async/non-blocking I/O.
* Minimize network hops and I/O-bound bottlenecks.

### 2. What are the trade-offs between WebSockets, Server-Sent Events, and polling?

| Feature         | WebSockets | SSE      | Polling |
| --------------- | ---------- | -------- | ------- |
| Full Duplex     | ✅          | ❌        | ❌       |
| Browser Support | ✅          | Limited  | ✅       |
| Latency         | Low        | Moderate | High    |
| Complexity      | Medium     | Low      | Low     |

* WebSockets: ideal for bidirectional communication (chat, games).
* SSE: good for server push (live feeds, notifications).
* Polling: fallback method with highest latency.

### 3. How do you implement real-time collaboration features like Google Docs?

* Use Operational Transform (OT) or Conflict-Free Replicated Data Types (CRDTs).
* Implement WebSockets for continuous bidirectional sync.
* Maintain shared document state and versioning.
* Resolve concurrent edits via transformation algorithms.

### 4. What are the challenges of implementing real-time multiplayer games?

* Maintaining low latency and synchronization.
* Ensuring consistent state across players.
* Preventing cheating with authoritative server logic.
* Handling network jitter, lag, and disconnects.

### 5. How do you handle connection management in real-time applications?

* Use heartbeat signals for connection health.
* Implement reconnection strategies.
* Track session state in memory/Redis.
* Enforce auth tokens and timeout policies.

### 6. What is the CAP theorem and how does it apply to real-time systems?

* CAP: Consistency, Availability, Partition Tolerance.
* In real-time: often choose Availability + Partition Tolerance (AP).
* Example: collaborative apps tolerate eventual consistency for uptime.

### 7. How do you implement real-time monitoring and alerting systems?

* Use Prometheus for metrics collection.
* Grafana for visualization.
* Alertmanager or custom webhooks for notifications.
* Collect logs with Fluentd or Logstash.

### 8. What are the considerations for real-time data synchronization?

* Conflict resolution (timestamps or CRDTs).
* Delta sync vs full object sync.
* Efficient protocols (gRPC, MQTT).
* Bandwidth constraints and prioritization.

### 9. How do you handle offline scenarios in real-time applications?

* Cache changes in local storage or service workers.
* Implement retry and reconciliation logic.
* Notify users of sync state.
* Gracefully degrade features.

### 10. What are operational transforms and how do they work?

* OT allows concurrent edits to a shared document.
* Transforms operations (e.g., insert/delete) to preserve consistency.
* Maintains history to apply user actions in the correct order.

## 🟩 High-Performance Computing

### 1. How do you optimize Python code for CPU-intensive tasks?

* Use Cython or Numba to compile Python to C.
* Vectorize with NumPy.
* Offload to C/C++ extensions.
* Profile with `cProfile`, `line_profiler`.

### 2. What is the difference between threading, multiprocessing, and async in Python?

| Model           | Best For        | Limitation                      |
| --------------- | --------------- | ------------------------------- |
| Threading       | I/O-bound       | Limited by GIL                  |
| Multiprocessing | CPU-bound       | High memory, IPC overhead       |
| Async           | I/O concurrency | Requires async libraries/models |

### 3. How do you implement distributed computing with Celery at scale?

* Use multiple worker queues.
* Monitor with Flower.
* Configure autoscaling.
* Redis or RabbitMQ as brokers.

### 4. What are the considerations for memory-efficient data processing?

* Stream data with generators.
* Use chunked reads (e.g., `pandas.read_csv(chunksize=...)`).
* Avoid deep copies.
* Use compact formats like Parquet.

### 5. How do you implement caching strategies for high-performance applications?

* Use Redis for fast lookups.
* Apply `@lru_cache`, `@cache` for memoization.
* Layered caching (app, DB, CDN).
* Define TTLs and cache invalidation rules.

### 6. What is the role of CDNs in global application performance?

* Distribute static content close to users.
* Reduce latency and server load.
* Improve scalability and reliability.
* Enhance security with DDoS protection.

### 7. How do you optimize database queries for high-throughput systems?

* Use indexing and avoid N+1 problems.
* Apply connection pooling.
* Use denormalization and caching.
* Monitor with query analyzers.

### 8. What are the trade-offs between different serialization formats?

| Format      | Speed  | Size   | Human-readable |
| ----------- | ------ | ------ | -------------- |
| JSON        | Medium | Medium | ✅              |
| Protobuf    | High   | Small  | ❌              |
| Avro        | High   | Small  | ❌              |
| MessagePack | High   | Small  | ❌              |

### 9. How do you implement efficient pagination for large datasets?

* Offset pagination: simple, slower at scale.
* Keyset pagination: fast, uses indexed ID.
* Cursor pagination: good for APIs.

### 10. What are the considerations for handling large file uploads and downloads?

* Use chunked/multipart uploads.
* Stream files to avoid memory bloat.
* Store in object storage (e.g., S3).
* Validate file size/type.

## 🟨 Integration & Interoperability

### 1. How do you design APIs for third-party integrations?

* REST or GraphQL with clear contracts.
* OAuth2 or API key for authentication.
* Document via Swagger/OpenAPI.
* Provide versioning support.

### 2. What are the patterns for integrating with legacy systems?

* Wrap in a microservice.
* Use an anti-corruption layer.
* Use queues or change data capture for sync.

### 3. How do you implement event-driven integration patterns?

* Use Kafka or RabbitMQ for messaging.
* Design events as immutable facts.
* Use event sourcing when appropriate.

### 4. What are the challenges of API versioning in microservices?

* Keeping old versions supported.
* Coordinating deprecation.
* URI or header versioning.
* Managing schema evolution.

### 5. How do you handle data transformation between different systems?

* Use transformation pipelines (ETL).
* Use mapping libraries or APIs.
* Normalize formats with schema definitions (e.g., Avro).

### 6. What is enterprise service bus (ESB) and when would you use it?

* Middleware that routes, transforms, and manages messages.
* Use in large monolithic enterprises.
* Avoid in microservices — use lightweight queues.

### 7. How do you implement idempotent operations in distributed systems?

* Use unique operation/request IDs.
* Store processed requests to detect duplicates.
* Retry-safe with no side effects.

### 8. What are the patterns for handling distributed transactions?

* 2PC: strict but blocking.
* Sagas: compensating actions, eventual consistency.
* Use outbox patterns.

### 9. How do you implement circuit breakers for external service calls?

* Use libraries like Resilience4j.
* Monitor failure rates and trip circuit.
* Provide fallbacks or cached data.

### 10. What are the considerations for API rate limiting and throttling?

* Token bucket or leaky bucket algorithm.
* Per-user/IP limits.
* Return `429` with `Retry-After`.
* Implement sliding window quotas.
