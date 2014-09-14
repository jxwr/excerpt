## ccan/io lib

io - simple library for asynchronous io handling.

io provides a mechanism to write I/O servers with multiple
connections.  Each callback indicates what I/O they plan next
(eg. read, write).  It is also possible to write custom I/O
plans.

### Core Loop

```
io_loop polling {
    io_ready()
    do_plan()
    plan->io()
    next_plan()
}
```

### Core Functions
