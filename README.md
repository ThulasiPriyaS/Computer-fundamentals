# Computer Fundamentals 


## DBMS

* **Database:** A collection of organized data.
* **Database Management System (DBMS):** Software that helps store, retrieve, and manage data.
  **Examples:** MySQL, PostgreSQL, MongoDB, Cassandra, etc.

---

## Types of Databases

### 1. SQL — Relational Database (Structured Data)

* Follows **RDBMS** model (data is fixed).
* **Examples:**

  * MySQL — strict normalization
  * PostgreSQL — SQL model with NoSQL flexibility (allows JSON, array data)
* **Scaling:** Vertical scaling — improving performance of the existing machine.

### 2. NoSQL — Unstructured Data

* Data stored in document style, key-value pairs, or graphs.
* **Examples:**

  * MongoDB — Document-based
  * Redis — Key-value pair
  * Neo4j — Graph-based
  * Cassandra — Column-based
* **Scaling:** Horizontal scaling — adding more machines to improve performance (via sharding).

---

## Sharding

The process of splitting a large database into smaller, faster, and more manageable parts.
It helps with data retrieval by reducing search space across smaller partitions.

---

## ACID Properties

| Property            | Meaning                  | Description                                                             |
| ------------------- | ------------------------ | ----------------------------------------------------------------------- |
| **A — Atomicity**   | All or nothing           | Either fully successful, or roll back to the previous state on failure. |
| **C — Consistency** | Data integrity           | Any change in one database must be reflected in related databases.      |
| **I — Isolation**   | Independent transactions | Each transaction must occur independently without interference.         |
| **D — Durability**  | Permanent results        | Once a transaction is complete, it remains recorded permanently.        |

---

## Keys in DBMS

| Key Type          | Description                                                                           |
| ----------------- | ------------------------------------------------------------------------------------- |
| **Primary Key**   | Uniquely identifies each row in a table.                                              |
| **Foreign Key**   | Links two or more tables using a common primary key.                                  |
| **Super Key**     | A set of attributes that uniquely identify a row (includes primary + alternate keys). |
| **Candidate Key** | Minimal subset of a super key, non-redundant.                                         |

---

## Normalization

**Goal:** Remove redundant data.

| Normal Form         | Description                                                                      |
| ------------------- | -------------------------------------------------------------------------------- |
| **1NF**             | No column should have multiple values (eliminate duplicates).                    |
| **2NF**             | Non-key attributes must depend on the whole primary key (no partial dependency). |
| **3NF**             | Non-key attributes depend only on the primary key (no transitive dependency).    |
| **BCNF**            | Every determinant must be a super key.                                           |
| **Denormalization** | Intentionally adding redundancy for readability and faster queries.              |

---

## Transactions

A **set of operations** performed as a single unit.
Must satisfy **atomicity** to ensure reliability.

---

## Concurrency

Occurs when multiple operations try to access the same database simultaneously.

### Locking Mechanisms

| Type                    | Description                                                     |
| ----------------------- | --------------------------------------------------------------- |
| **Table-level locking** | Locks the entire table (inefficient).                           |
| **Row-level locking**   | Locks only the specific row.                                    |
| **Page-level locking**  | Locks a set of rows or pages.                                   |
| **Pessimistic locking** | Locks resources at the start of a transaction until completion. |
| **Optimistic locking**  | No locks — commits all operations, rolling back if any fail.    |

---

## Deadlocks

A situation where two or more transactions are waiting for each other’s resources, causing indefinite blocking.

### Necessary Conditions

1. **Mutual Exclusion:** Only one transaction holds a resource at a time.
2. **Hold and Wait:** A transaction holds one resource while requesting others.
3. **No Preemption:** Resources cannot be forcibly taken from a transaction.
4. **Circular Wait:** Transactions form a circular chain of resource requests.

### Deadlock Handling

#### 1. Deadlock Avoidance

* Follow a strict transaction order.
* Use row-level locking.
* Apply timeouts for stalled transactions.

#### 2. Deadlock Detection

* Use a **Wait-for Graph** (like Banker's Algorithm) to detect cycles; abort operations if detected.

#### 3. Deadlock Prevention

* **Wait-Die (Non-Preemptive):** Older transactions wait; younger ones abort if needed.
* **Wound-Wait (Preemptive):** Older transactions abort younger ones holding required resources.

---

## Indexing

A **data structure** that improves data retrieval speed (not a linear search).

### Types

| Type                    | Description                                                                                     |
| ----------------------- | ----------------------------------------------------------------------------------------------- |
| **Clustered Index**     | Reorders how records are physically stored; only one per table. Leaf nodes contain actual data. |
| **Non-Clustered Index** | Uses pointers; leaf nodes contain row addresses, not data pages.                                |

### Index Implementations

* **B-Tree Index:** Balanced binary trees; logarithmic (O(log n)) access time.
* **Hash Index:** Hashes the primary key to retrieve the data’s memory address.

---

## CAP Theorem

| Property                    | Description                                                         |
| --------------------------- | ------------------------------------------------------------------- |
| **Consistency (C)**         | All nodes see the same data at the same time.                       |
| **Availability (A)**        | Every request gets a response, even if it’s not the latest version. |
| **Partition Tolerance (P)** | System functions despite network failures between nodes.            |

### Trade-offs

* **CP:** Prioritizes data accuracy (may become unavailable during partition).
* **AP:** Prioritizes availability (may serve slightly outdated data).
* **CA:** Works only when there are no network partitions (rare in real-world systems).

---
