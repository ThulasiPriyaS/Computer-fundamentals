# Computer-fundamentals

DBMS
Database - collection of organized data
Database Management System (DBMS) - a software that helps you store, retrieve and manage data
(eg): MySQL, PostgreSQL, MongoDB, Cassandra, etc

Types:
1. SQL - relational database (structured data) - RDBMS (data is fixed)
MySQL (strict normaliztion), PostgreSQL (sql model with nosql flexibility - allows json, array data also)
Vertical scaling - improving the performance of the machine that is already running on
2. NoSQL - unstructured data (document style, key value pair, graphs)
Mongodb - docs, Redis - key value pair, Neo4j - Graph, Cassandra - column based
Horizontal scaling - adding more machines to improve performance (like shrading )

sharding - the process of splitting a large database into smaller, faster, and more manageable parts. helps mainly in retieval of data. instead of searching through the entire database, since you are spliting it into smaller parts, searching is easy

ACID properties
  1. A - Atomicity (all or nothing mentality - either its fully successful or if it fails even at one stage we roll back to previous state)
  2. C - Consistency (when two or more databases are related, any change in a database A must be reflected and syncronized with all the other databases that are related to it)
  3. I - Isolation (every transaction must happen independently and in an order without interruptions- two operation that are related to each other shouldn't happen simultaenously)
  4. D - Durability (non repudiation basically - once a transaction is done, it cannot later be claimed that it didn't)

Primary key - a column of values that lets us uniquely indentify the row
Foreign key - when two or more tables are related, this column lets us identify the properties of both table, using the primary key that's common between them
Super key - set of column values that helps us uniquely identify a row (includes primary key along with alternative keys)
Candidate key - subset of super key (minimal set of attributes that are non redundant)

Normalization 
removing redundant data 
1NF - no row should have two values in a column (eliminating duplicates)
2NF - a non-key attribute must be fully dependent on a primary key, not just a part of it. (no partial dependency)
3NF - a non-key attribute must only be dependent on a primary key, not any other keys (transitive dependency)
Boyce-Codd Normal form (BCNF) - a set of values that helps us uniquely identify a row, must have super keys that helps us narrow it down. non existence of this super keys violates bcnf
Denormalization
Intentionally adding redudant data to the normalized database for better readability at the end point.

Transactions
Set of operations that perform as a single unit (must satisfy atomicity property)
Concurrency
Multiple operations trying to access the same database

Locking mechanisms to prevent concurrency
1. Table level locking - locking the database for a particular user, so no interrupts
(not very efficient or real-word use case)
2. Row level locking - locks only the row, instead of the whole table during the transaction
3. Page level locking - set of rows from a table or multiple tables is locked during a transaction
4. Pessimistic locking - locking a database at the start of a transaction and releasing it at the end of it
5. Optimistic locking - no locks. Commits each operations by stacking, even if one transaction fails, it rolls back to the previous state

Deadlocks
a situation where two or more transactions are blocked indefinitely, each waiting for a resource that is held by another transaction in the group

Necessary conditions of a deadlock
1. Mutex - only one transaction can hold a database at a time
2. Hold and wait - the transaction holding the resources may request request for other additional resources held by other transactions
3. No preemption - cannot forcibly take the resources from a transaction that is holding it
4. Circular wait - each transaction holds a resource held by another prohibiting any transactions from happpening

Ways to handle deadlock
1. Deadlock avoidance 
Methods:
Always follow a order in which the transactions happen
Use row level locking
Timeout - for a specified time if no transactions are made then fail all of it
2. Deadlock detection 
Wait for graph - (like bankers algorithm) creates a graph to check if the operation has any deadlocks, if so all operations are rejected
3. Deadlock prevention
1. Wait die scheme (non premptive) - SJF method (older transactions are meant to wait, while if any younger transaction requests a resource held by a older transaction, it is aborted)
2. Wound and wait (preemptive) - FCFS method (if the older transaction needs a resource held by the younger transaction, it aborts the younger transaction. if younger needs a resource held by older, then it waits.)

Indexing (not a linear search method)
this is data structure, that helps us calculate indices for the data from which we can easily retrieve data
Types
1. Clustered index - reorders the way records in the table are physically stored. Therefore table can have only one clustered index. The leaf nodes of a clustered index contain the data pages.
Basically a dictionary data structure
2. Non-Clustered index - pointer based. The leaf node indicates the row address intead of the data pages
Index implementation types
1. B-Tree index - Balanced (Binary trees). logn time to access data
2. Hashing based index - hashes the primary key of the record, and retrieves a memory address. based on this address we can simply access the data

CAP theorm
C - Consistency - All nodes see the same data at the same time
A - Availability - Every request receives a response, without the guarantee that it contains the most recent write. The system remains operational even if some nodes are down.
P - Partition tolerance - system can function even if there are network issues or a communication failure between nodes
Tradeoffs
CP - during a network crisis, the system priortizes data accuracy. may lead to unavailability of data
AP - prioritizes availability. may respond with an inaccurate data (not the mot recent write)
CA - works best when there are no network partitions (generally not used in real life scenarios)












