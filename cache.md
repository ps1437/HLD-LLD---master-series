# Caching in Distributed Systems

## 🧠 What is Caching?
Caching is the process of storing frequently accessed data in a temporary storage (cache) to reduce the time and cost of fetching data from the original source (e.g., database, remote API).

---

## 🔖 Types of Cache

### 1. **In-Memory Cache**
- Stored in local memory of the application (e.g., Java `ConcurrentHashMap`, Guava Cache).
- Fastest but not shared between instances.
- Example: `LocalCache.get(key)`

### 2. **Distributed Cache**
- Shared across multiple application instances.
- Resilient and scalable.
- Examples: Redis, Memcached, Hazelcast, Apache Ignite.

### 3. **Persistent Cache**
- Cache stored on disk to survive restarts.
- Slower than in-memory but useful for large data sets.
- Example: Ehcache with disk persistence.

### 4. **Write-Through Cache**
- Every cache update writes to the database.
- Ensures consistency.
- Example: `cache.put(key, value)` also writes to DB.

### 5. **Write-Behind (Write-Back) Cache**
- Writes are delayed and written to DB asynchronously.
- Improves write performance but risks data loss on crash.

### 6. **Read-Through Cache**
- Cache fetches data from the database if not present.
- Example: `cache.get(key)` → if miss → load from DB → store in cache.

### 7. **Refresh-Ahead Cache**
- Periodically refreshes entries before they expire to avoid cache misses.

---

## ⚙️ Distributed Cache Examples

| Tool        | Description                              |
|-------------|------------------------------------------|
| **Redis**   | In-memory data store with pub-sub & persistence |
| **Hazelcast**| Java-native, supports distributed data structures |
| **Memcached**| Simple key-value store, fast but no persistence |
| **Apache Ignite** | In-memory + disk storage with SQL support |

---

## 🧩 Cache Design Considerations

- **Eviction Policy**: LRU (Least Recently Used), LFU, FIFO
- **TTL (Time-To-Live)**: Expiry time for cache entries
- **Consistency**: Strong (always accurate) vs Eventual (may be stale)
- **Cache Size**: Limited memory → need eviction
- **Preloading / Warm-Up**: Load frequently used data at startup
- **Partitioning/Sharding**: Spread data across nodes

---

## ❗ Common Issues with Cache

| Issue                       | Description                                                                 |
|----------------------------|-----------------------------------------------------------------------------|
| **Cache Inconsistency**    | Cache and DB out of sync due to delayed or failed updates                   |
| **Cache Stampede**         | Multiple threads query the DB on cache miss (solution: mutex/semaphore)     |
| **Cache Avalanche**        | Many keys expire at once → DB overload (solution: randomized TTL)           |
| **Cache Penetration**      | Repeated requests for non-existent data (solution: cache nulls)             |
| **Hot Keys**               | Uneven traffic on certain keys (solution: key partitioning or rate limiting)|
| **Serialization Overhead**| Time taken to serialize/deserialize complex objects                         |
| **Stale Data**             | Data becomes outdated if not updated promptly                               |

---

## ✅ Best Practices

- Use consistent hashing for distributed cache keys.
- Compress large data objects.
- Monitor cache hit/miss ratios.
- Version your cache keys (`user:123:v2`) for schema changes.
- Use fallback logic in case of cache failure.

---

## 📌 Sample Cache Key Strategy

Use clear namespaces and consistent patterns.

---

## 🔄 Cache Invalidation Strategies

- **Manual Invalidation**: On data change, explicitly remove/update cache.
- **Time-Based Expiry**: Set TTLs to auto-expire stale data.
- **Event-Based Invalidation**: Use message brokers (e.g., Kafka, Redis pub-sub) to notify changes.

---

<img width="234" alt="image" src="https://github.com/user-attachments/assets/0011fa8f-584d-4459-8355-0d8ccce5a9b0" />

