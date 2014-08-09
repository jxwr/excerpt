## Spanner: Google’s Globally-Distributed Database

Spanner is Google’s scalable, multi-version, globally distributed, and synchronously-replicated database. It is the first system to distribute data at global scale and support externally-consistent distributed transactions

- At the highest level of abstraction, it is a database that shards data across many sets of *Paxos state machines* in datacenters spread all over the world.
- clients automatically failover between replicas
- Many applications at Google have chosen to use Megastore [5] because of its semirelational data model and support for synchronous replication, despite its relatively poor write throughput
- It provides externally consistent reads and writes, and globally-consistent reads across the database at a timestamp. if a transaction T 1 commits before another transaction T 2 starts, then T 1 ’s commit timestamp is smaller than T 2 ’s
- A Spanner deployment is called a universe.
- Spanner is organized as a set of zones, a zone has one zonemaster and between one hundred and several thousand spanservers.
- Zonemaster assigns data to spanservers; the latter serve data to clients.
- To support replication, each spanserver implements a single Paxos state machine on top of each tablet.
- At every replica that is a leader, each spanserver implements a lock table to implement concurrency control(two-phase locking: it maps ranges of keys to lock states.)
- Each spanserver also implements a transaction manager to support distributed transactions.
- A directory(bucket) is the unit of data placement. All data in a directory has the same replication configuration. When data is moved between Paxos groups, it is moved directory by directory
- Movedir is the background task used to move directories between Paxos groups. Movedir actually moves fragments, and not whole directories, between groups.
- A directory is also the smallest unit whose geographic replication properties (or placement, for short) can be specified by an application.
- Administrators control two dimensions: the number and types of replicas, and the geographic placement of those replicas. (e.g. North America, replicated 5 ways with 1 witness)
- Spanner will shard a directory into multiple fragments if it grows too large. 也就是说，最小单位其实是fragment，Movedir以fragment粒度做数据迁移
- Spanner exposes: a data model based on schematized semi-relational tables, a query language, and general purpose transactions. -> applications
- Every table is required to have an ordered set of one or more primary-key columns. 半关系型
- The underlying time references used by TrueTime are GPS and atomic clocks.
- Ｗe have taken more than 5 years to iterate to the current design and implementation.