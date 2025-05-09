# Partitioning and Sharding Design

## Overview

This document outlines the partitioning and sharding strategy for the system's data storage. Partitioning and sharding are critical for distributing large datasets efficiently across multiple servers, improving performance, scalability, and availability.

<img width="293" alt="image" src="https://github.com/user-attachments/assets/e98fe0e6-6c1b-4512-909f-5ed29f217656" />
<img width="218" alt="image" src="https://github.com/user-attachments/assets/39a88ee8-2b8c-4927-b19f-3d562fd9a0f7" />


## 1. Partitioning

Partitioning refers to dividing a database into smaller, more manageable pieces, called partitions. Each partition contains a subset of data, which helps to distribute the load and makes data more accessible.

### 1.1. Types of Partitioning

#### 1.1.1. Horizontal Partitioning (Sharding)

- **Definition**: Splitting data into rows, where each partition contains a subset of rows from the same table.
- **Use Case**: Useful for large datasets where certain rows (based on a key) can be accessed independently.

#### 1.1.2. Vertical Partitioning

- **Definition**: Splitting a table into smaller tables where each partition contains a subset of columns.
- **Use Case**: Often used when certain columns are frequently accessed together, improving performance by reducing I/O.

### 1.2. Benefits of Partitioning

- **Improved Query Performance**: Smaller partitions lead to faster query execution.
- **Manageability**: Easier to maintain and back up smaller partitions.
- **Scalability**: Allows horizontal or vertical scaling to handle large datasets.
- **Data Isolation**: Partitioning ensures that specific data subsets are isolated for more efficient access.

## 2. Sharding

Sharding is a specific type of partitioning where data is distributed across multiple servers, or "shards," to ensure that no single server is overloaded. Sharding helps improve performance, redundancy, and scalability by breaking data into smaller, distributed units.

### 2.1. Sharding Strategies

#### 2.1.1. Range-Based Sharding

- **Definition**: Data is partitioned based on a range of values from a given column (e.g., date, numeric ID).
- **Example**: If we shard a users table by `user_id`, users with IDs 1–1000 go to shard 1, IDs 1001–2000 go to shard 2, and so on.
- **Pros**: Easy to implement; good for queries that need range scans.
- **Cons**: May result in uneven data distribution (e.g., large gaps between values).

#### 2.1.2. Hash-Based Sharding

- **Definition**: A hash function is applied to a key (e.g., `user_id`) to distribute rows across shards uniformly.
- **Example**: If we hash `user_id` using a modulus operation (`user_id % number_of_shards`), the user with `user_id = 1057` may be placed on shard 3.
- **Pros**: Provides uniform distribution; reduces the risk of hot spots.
- **Cons**: Harder to manage when adding or removing shards (requires rehashing).

#### 2.1.3. Directory-Based Sharding

- **Definition**: A central directory or lookup table maps records to specific shards based on certain attributes or rules.
- **Example**: A directory table contains mappings like `user_id 1-1000 → shard_1, user_id 1001-2000 → shard_2`.
- **Pros**: Flexible and easy to adjust.
- **Cons**: The directory becomes a potential bottleneck and single point of failure.

### 2.2. Shard Key Selection

The shard key is the attribute of the data that determines how it will be partitioned across the shards. Choosing the right shard key is critical to avoid issues like data skew or hotspots.

- **High Cardinality Keys**: A good shard key has high cardinality to ensure even distribution (e.g., `user_id` or `order_id`).
- **Access Patterns**: Select a shard key based on query access patterns to minimize cross-shard queries.
- **Avoid Hotspots**: Choose a shard key that evenly distributes the data. For example, sharding by a timestamp may result in uneven distribution if the majority of traffic is time-based.

### 2.3. Handling Cross-Shard Queries

Cross-shard queries occur when data from multiple shards needs to be accessed at the same time. These queries can introduce complexity and overhead.

- **Solution 1**: Use **replicas** for high availability and quicker access to frequently queried data.
- **Solution 2**: Implement **distributed joins** using middleware that can access data from multiple shards simultaneously.
- **Solution 3**: Avoid cross-shard queries when possible by designing the data model to keep related data on the same shard.

## 3. Benefits of Sharding

- **Improved Performance**: Distributes the load across multiple servers, improving query performance.
- **Increased Scalability**: Can scale horizontally by adding more shards.
- **Fault Tolerance**: Each shard can be replicated for fault tolerance.
- **Flexibility**: Allows systems to store large amounts of data without overloading any single database.

## 4. Challenges of Sharding

- **Complexity**: Sharding introduces complexity in data management, query execution, and system maintenance.
- **Data Rebalancing**: When adding new shards, data may need to be redistributed, which can be resource-intensive.
- **Cross-Shard Joins**: These can be slower and more complex to implement efficiently.

## 5. Monitoring and Maintenance

- **Shard Health Monitoring**: Regularly monitor the health and performance of each shard (e.g., CPU, memory, disk usage).
- **Rebalancing**: Implement periodic checks to ensure even data distribution and initiate rebalancing when necessary.
- **Replication**: Ensure that data in each shard is replicated to other shards or nodes to maintain high availability and durability.

## 6. Conclusion

Partitioning and sharding are critical strategies for managing large-scale systems. By choosing the right partitioning and sharding strategies, selecting appropriate shard keys, and monitoring the system closely, we can ensure optimal scalability, performance, and fault tolerance.

