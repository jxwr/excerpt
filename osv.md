## osv

OSv—Optimizing the Operating System for Virtual Machines

- includes an ELF dynamic linker for Linux ABI
- has simple ramfs, devfs, procfs
- libc: musl, vfs: prex, zfs: freebsd, ACPI: ACPICA
- network channels-based network stack
- implement the mutex itself without using a spinlock
- most work in the kernel, including interrupt handling, these can use lock-based algorithms. they use mutex, not a spin-lock
- network channel的问题在于，应用程序使用send/recv收发数据，以及网卡驱动接受输入传递给应用程序，这两个过程共享数据结构，在压力大的时候，会产生很多锁和竞争
- tick-less, on virtual machines where interrupts are signiﬁcantly slower than on physical machines, as they involve exits to the hypervisor
- make use of the fact that most reschedules are voluntary, osv can skip saving
the FPU state for voluntary context switches
- can use zero-copy api where the kernel and user space share the buffers
- netmap-like api, 4x memcached
- shrinker api make an application uses all the memory which OSv doesn’t need
