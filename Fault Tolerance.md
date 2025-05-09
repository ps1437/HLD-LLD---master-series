# Fault Tolerance

## What is Fault Tolerance?

Fault tolerance is the ability of a system to **keep working even if some parts fail**. It ensures that a failure in one component does **not cause the whole system to stop**.

---

## Key Ideas

- **No Single Point of Failure**: The system is built so that if one part fails, others take over.
- **Automatic Recovery**: The system detects failure and responds without manual help.
- **Continuous Service**: Users often don’t even notice something broke.

---

## Fault Tolerance vs High Availability

| Aspect               | Fault Tolerance                                  | High Availability                                  |
|----------------------|--------------------------------------------------|---------------------------------------------------|
| **Goal**             | Keep system working even if a part fails         | Minimize downtime and ensure system is usually available |
| **Failure Handling** | Continues running even during a failure          | May need to switch to a backup or wait for recovery |
| **Example**          | A server crashes, but the system still responds  | If a server crashes, another one takes over quickly |

---

## Techniques to Achieve Fault Tolerance

1. **Redundancy**  
   - Multiple components (e.g., servers, disks) ready to replace failed ones.

2. **Replication**  
   - Data or services copied across different machines or regions.

3. **Failover Systems**  
   - Automatic switching to backup components when one fails.

4. **Error Detection and Recovery**  
   - Detect and correct software/hardware issues on the fly.

5. **Retry Mechanisms**  
   - Re-attempt failed operations (e.g., network retries).

6. **Distributed Architecture**  
   - Systems like microservices or distributed databases reduce impact of individual failures.

7. **Circuit Breakers** (in software)
   - Prevent cascading failures by stopping calls to failing services.

---

# Title of Your Document

## Design Patterns

### 1. Circuit Breaker
- **Purpose**: Prevents repeated failures by halting calls to a service after a threshold is reached.
- **Implementation**: Briefly describe how it's implemented.

### 2. Retry
- **Purpose**: Retries failed operations to handle transient issues.
- **Implementation**: Describe the retry logic in use.

### 3. Fallback
- **Purpose**: Provides an alternative action when the primary service fails.
- **Implementation**: Outline how the fallback mechanism works.

### 4. Bulkhead
- **Purpose**: Isolates failures to prevent them from affecting other system components.
- **Implementation**: Explain how critical components are isolated.

### 5. Timeout
- **Purpose**: Prevents operations from hanging indefinitely.
- **Implementation**: Describe timeout settings and usage.

## Section 3: Conclusion
Summarize the importance of failure tolerance and how it helps the system stay resilient.

---

## Real-World Example

- A payment system uses multiple servers and databases.
- If one database fails, the system automatically switches to another without affecting users.
- That’s fault tolerance in action.

