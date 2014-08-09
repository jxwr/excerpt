## Cockroach

A scalable, transactional, geo-replicated database

https://docs.google.com/document/d/11k2EmhLGSbViBvi6_zFEiKzuXxYF49ZuuDJLe6O8gBU

http://www.cs.cornell.edu/~ie53/publications/DC-col51-Sep13.pdf

- Implements a single, monolithic sorted map from key to value where both keys and values are byte strings (not unicode).
- Data stored in RocksDB
- Raft consensus algorithm. All consensus state is stored in RocksDB.
- A single logical mutation may affect multiple key/value pairs. Logical mutations have ACID transactional semantics. If all keys affected by a logical mutation fall within the same range, atomicity and consistency are guaranteed by Raft; this is the fast commit path. Otherwise, a non-locking distributed commit protocol is employed between affected ranges. 一次业务逻辑修改可能影响多个kv对，如果这些改动在一个range中，Raft来保证一致性，否则使用非阻塞分布式提交协议来搞
- Snapshot isolation is a guarantee that all reads made in a transaction will see a consistent snapshot of the database (in practice it reads the last committed values that existed at the time it started), and the transaction itself will successfully commit only if no updates it has made conflict with any concurrent updates made since that snapshot. 事务
- Cockroach allows configuration of arbitrary zones of data. This allows replication factor, storage device type, and/or datacenter location to be chosen to optimize performance and/or availability. 数据分布
- Each physical node exports a RoachNode service. Each RoachNode exports one or more key ranges. RoachNodes are symmetric. Each has the same binary and assumes identical roles. 节点是同质的
- Up to F failures can be tolerated, where the total number of replicas N = 2F + 1 (e.g. with 3x replication, one failure can be tolerated; with 5x replication, two failures, and so on). 根据需要选择3倍还是5倍冗余，Spanner是5倍，避免两个数据中心同时挂了第三个也不能用了。
- Cockroach maintains historical versions of values by storing them with associated commit timestamps. 实现是通过修改RocksDB，加入timestamp和gc
- Provides distributed transactions without locks. 支持SI和SSI，SSI是默认的，SI性能好一点，但是会有write skew
- Timestamp choosing use retries, could also potentially use a global clock (Google did this with Pinax) 没有Spanner的原子钟问题麻烦多了
- Both inboxes and outboxes are assigned to keys; messages can be sent or received on behalf of any key. Messages can be deliverable, or executable.  
- Cockroach accepts writes at any replica, 从将写转发给主
- RoachNodes split or merge ranges based on whether they exceed maximum or minimum thresholds for capacity or load.
- Node Allocation via Gossip
- Complete accounting for each node is also stored to a central location 汇报
