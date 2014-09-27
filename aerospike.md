## Aerospike

### Reading Code

- Edge Triggered Epoll, 根本不理EPOLLOUT，Write时是轮询，发布出去就usleep(1)
  (https://github.com/aerospike/aerospike-server/blob/master/as/src/base/proto.c#L786)
- EPOOLIN时先获取可读的数据量，如果不够就等下一轮一次读，`ioctl(fd, FIONREAD, &sz)`
- 多线程，连接到来时round-robin分发给某个thread
- 每个线程一个epoll_fd，一个事件循环
- 第一个线程accept新连接
- PhysicalNIC/PhysicalCPU pairing (http://highscalability.com/blog/2012/9/10/russ-10-ingredient-recipe-for-making-1-million-tps-on-5k-har.html)
- 一个请求，检查是否在内存里，如果在就直接处理，不在enqueue
- To avoid single core implementations and NUMA overhead, the balanced approach is to build a system that scales by grouping multiple threads per CPU socket instead of per core with a single threaded system. ?
- 同集群内是同步冗余，跨机房是异步冗余
- stack based allocator
- 文件夹
  - as server
  - cf 基础库
  - ai 索引


