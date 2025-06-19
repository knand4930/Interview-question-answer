### Advanced Code Examples & Whiteboard Challenges

---

## ✅ Algorithm & Data Structure Problems

### 1. Implement a LRU cache with O(1) operations

Use a combination of a **hash map** for constant-time lookups and a **doubly linked list** for constant-time insertions/removals.

```python
from collections import OrderedDict

class LRUCache:
    def __init__(self, capacity):
        self.cache = OrderedDict()
        self.capacity = capacity

    def get(self, key):
        if key not in self.cache:
            return -1
        self.cache.move_to_end(key)
        return self.cache[key]

    def put(self, key, value):
        if key in self.cache:
            self.cache.move_to_end(key)
        self.cache[key] = value
        if len(self.cache) > self.capacity:
            self.cache.popitem(last=False)
```

---

### 2. Design a URL shortener with collision handling

Use a hash function and check for collision in a dictionary.

```python
import hashlib, random, string

class URLShortener:
    def __init__(self):
        self.db = {}

    def shorten(self, url):
        short = ''.join(random.choices(string.ascii_letters + string.digits, k=6))
        while short in self.db:
            short = ''.join(random.choices(string.ascii_letters + string.digits, k=6))
        self.db[short] = url
        return short

    def expand(self, short):
        return self.db.get(short, None)
```

---

### 3. Implement a distributed rate limiter

Use a sliding window counter stored in Redis sorted sets to limit requests across distributed systems.

```python
import time
import redis

class DistributedRateLimiter:
    def __init__(self, redis_client, key_prefix='rate:', window_seconds=60, limit=100):
        self.client = redis_client
        self.window = window_seconds
        self.limit = limit
        self.key_prefix = key_prefix

    def allow_request(self, user_id):
        key = f"{self.key_prefix}{user_id}"
        now = int(time.time() * 1000)  # current time in ms
        window_start = now - self.window * 1000

        pipe = self.client.pipeline()
        pipe.zremrangebyscore(key, 0, window_start)
        pipe.zadd(key, {str(now): now})
        pipe.zcard(key)
        pipe.expire(key, self.window)
        _, _, request_count, _ = pipe.execute()

        return request_count <= self.limit

# Usage example:
# redis_client = redis.StrictRedis(host='localhost', port=6379, db=0)
# limiter = DistributedRateLimiter(redis_client)
# if limiter.allow_request("user123"):
#     print("Request allowed")
# else:
#     print("Rate limit exceeded")
```

---

### 4. Design a consistent hashing algorithm

Use a hash ring with virtual nodes.

```python
import hashlib

class ConsistentHash:
    def __init__(self, nodes, vnodes=3):
        self.ring = dict()
        self.sorted_keys = []
        for node in nodes:
            for i in range(vnodes):
                key = self.hash(f"{node}-{i}")
                self.ring[key] = node
                self.sorted_keys.append(key)
        self.sorted_keys.sort()

    def hash(self, key):
        return int(hashlib.md5(key.encode()).hexdigest(), 16)

    def get_node(self, key):
        h = self.hash(key)
        for k in self.sorted_keys:
            if h <= k:
                return self.ring[k]
        return self.ring[self.sorted_keys[0]]
```

---

### 5. Implement a bloom filter for duplicate detection

Use bit array and multiple hash functions.

```python
import hashlib

class BloomFilter:
    def __init__(self, size=1000, hash_count=3):
        self.size = size
        self.hash_count = hash_count
        self.bit_array = [0] * size

    def _hashes(self, item):
        return [int(hashlib.md5((item + str(i)).encode()).hexdigest(), 16) % self.size for i in range(self.hash_count)]

    def add(self, item):
        for hash_ in self._hashes(item):
            self.bit_array[hash_] = 1

    def check(self, item):
        return all(self.bit_array[hash_] for hash_ in self._hashes(item))
```

---

### 6. Design a time-series database structure

Store data in chunks (e.g., by day/hour). Use timestamp-based keys and write-ahead logs for durability.

```sql
CREATE TABLE sensor_data (
    sensor_id UUID,
    timestamp TIMESTAMPTZ,
    value DOUBLE PRECISION,
    PRIMARY KEY (sensor_id, timestamp)
);
-- Use TimescaleDB for automatic partitioning and compression.
```

---

### 7. Implement a priority queue with custom priority functions

```python
import heapq

class CustomPriorityQueue:
    def __init__(self, func):
        self.heap = []
        self.func = func

    def push(self, item):
        heapq.heappush(self.heap, (self.func(item), item))

    def pop(self):
        return heapq.heappop(self.heap)[1]
```

---

### 8. Design a distributed lock mechanism

Use Redis with `SET NX PX` or Redlock algorithm.

```python
# Using redis-py
import redis, uuid

class DistributedLock:
    def __init__(self, client):
        self.client = client

    def acquire(self, key, ttl=5000):
        self.lock_id = str(uuid.uuid4())
        return self.client.set(key, self.lock_id, nx=True, px=ttl)

    def release(self, key):
        script = """
        if redis.call("get", KEYS[1]) == ARGV[1] then
            return redis.call("del", KEYS[1])
        else
            return 0
        end
        """
        return self.client.eval(script, 1, key, self.lock_id)
```

---

### 9. Implement a sliding window rate limiter

```python
from collections import deque
import time

class SlidingWindowRateLimiter:
    def __init__(self, max_requests, window_seconds):
        self.max_requests = max_requests
        self.window = window_seconds
        self.requests = deque()

    def allow(self):
        current = time.time()
        while self.requests and self.requests[0] < current - self.window:
            self.requests.popleft()
        if len(self.requests) < self.max_requests:
            self.requests.append(current)
            return True
        return False
```

---

### 10. Design a recommendation algorithm with collaborative filtering

```python
import numpy as np
from sklearn.metrics.pairwise import cosine_similarity

# Sample user-item matrix
# Rows = users, Columns = items
ratings = np.array([
    [5, 3, 0, 1],
    [4, 0, 0, 1],
    [1, 1, 0, 5],
    [0, 0, 5, 4],
    [0, 0, 4, 0],
])

# Step 1: Compute similarity matrix between users
user_similarity = cosine_similarity(ratings)

# Step 2: Predict missing ratings using weighted sum of similarities
# Predict rating for user 0, item 2
user_index = 0
item_index = 2

# Get all other users' ratings for this item
item_ratings = ratings[:, item_index]
similarities = user_similarity[user_index]

# Exclude self-rating and users who haven't rated the item
mask = (item_ratings != 0) & (np.arange(len(ratings)) != user_index)

if np.any(mask):
    weighted_sum = np.dot(similarities[mask], item_ratings[mask])
    similarity_sum = np.sum(similarities[mask])
    predicted_rating = weighted_sum / similarity_sum
else:
    predicted_rating = 0  # fallback

print(f"Predicted rating for user {user_index} on item {item_index}: {predicted_rating:.2f}")

# Step 3: Recommend top-N items with highest predicted ratings
# Iterate over all unrated items and compute predictions
```

---

## ✅ System Design Whiteboard Exercises

### 1. Design Instagram/Twitter feed system

* Components: Post service, User graph, Feed generator
* Write fanout for celebrities, read fanout for normal users
* Cache feeds in Redis, use background workers

### 2. Design Uber/Lyft ride-sharing system

* Real-time location tracking
* Matching engine (geo-hashing)
* ETA prediction (ML models), surge pricing

### 3. Design Netflix video streaming platform

* Video encoder, CDN, DRM, player analytics
* Store metadata in Postgres, videos in S3, serve via CDN

### 4. Design WhatsApp messaging system

* Use message queues (Kafka)
* Store messages in distributed DB
* Delivery receipts, end-to-end encryption (Signal protocol)

### 5. Design Dropbox file storage system

* Chunk large files, deduplicate
* Use metadata DB and object store like S3
* Background sync clients

### 6. Design Stack Overflow Q\&A platform

* PostgreSQL for relational data
* ElasticSearch for search
* Tables: Questions, Answers, Votes, Tags, Users

### 7. Design Ticketmaster event booking system

* Use seat-lock service with Redis
* Support atomic booking, concurrency control
* Eventually consistent inventory updates

### 8. Design YouTube video upload and streaming

* Video ingestion pipeline
* Transcode to multiple resolutions
* Store in CDN

### 9. Design Amazon product search system

* Full-text search engine
* Ranking, recommendations
* Filters and faceted search

### 10. Design Slack team communication platform

* WebSocket gateway
* Event store and timeline service
* Archive and permission model

---

## ✅ Database Design Challenges

### 1. Design schema for multi-tenant SaaS application

* Global tenant table
* All tables have tenant\_id as FK
* Optional: schema/database per tenant

### 2. Design schema for e-commerce platform with complex pricing

* Products, Variants, Prices, Discounts, Coupons
* Tiered pricing, time-based rules

### 3. Design time-series data storage for IoT sensors

* Use TimescaleDB or InfluxDB
* Partition by time
* Schema: device\_id, ts, metric\_name, value

### 4. Design schema for social media platform with feeds

* Users, Posts, Follows, Likes, Comments
* Store feeds separately (cached/precomputed)

### 5. Design database for financial trading system

* ACID-compliant engine
* Order books, transactions, balances
* Use append-only logs and audit trails

### 6. Design schema for content management system

* Pages, Sections, Blocks
* JSON fields for flexibility
* Versioning and rollback support

### 7. Design database for real-time analytics dashboard

* Materialized views
* Streaming ETL using Kafka/Flink
* Columnar DB (ClickHouse)

### 8. Design schema for logistics and supply chain management

* Products, Shipments, Warehouses, Routes
* Real-time tracking and audit history

### 9. Design database for healthcare management system

* Patients, Doctors, Visits, Prescriptions
* Role-based access, encrypted records
* Support regulatory compliance (HIPAA)

### 10. Design schema for online learning platform

* Courses, Lessons, Enrollments
* Progress tracking, quizzes, certificates
* Discussion forum and peer grading

---
