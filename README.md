# Distributed KV

**Distributed KV** is a distributed key-value storage system designed to explore the fundamentals of distributed systems, including replication, fault tolerance, consensus, and horizontal scaling.

The project will progressively implement primary-backup replication, Paxos-based consensus, and dynamic sharding to maintain consistency and availability across multiple servers.

**Goal:** Develop a deep understanding of distributed systems by implementing core protocols from scratch, handling real-world failure scenarios, and exploring the architectural tradeoffs behind scalable, reliable infrastructure.

## What I am building

### 1. Primary-backup replication

Build a replicated key-value service with a primary server and a backup. A view service will track server liveness and coordinate role changes so the system can recover from server failures while preserving consistent state.

This stage explores failover, state synchronization, and network partitions, including the limitations of a view service that is itself a single point of failure.

**Components:** `viewservice/`, `pbservice/`

### 2. Paxos-based consensus

Implement Paxos from scratch and use it to agree on a shared sequence of key-value operations across replicas. This stage will remove the central view service and explore how a replicated service maintains consistency through failures and network partitions.

Progress will depend on a reachable majority of replicas, making the tradeoff between consistency and availability explicit.

**Components:** `paxos/`, `kvpaxos/`

### 3. Dynamic sharding

Partition the key space across replica groups, with each group using Paxos to replicate its state. Different groups will serve Get and Put operations in parallel, allowing the system to scale horizontally.

A replicated configuration service will manage shard ownership as groups join or leave. This stage will explore shard migration, reconfiguration, and preserving consistency while data moves between groups.

**Components:** `shardmaster/`, `shardkv/`, with consensus provided by `paxos/`
