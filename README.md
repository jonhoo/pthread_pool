pthread_pool
============

A simple implementation of thread pooling for C/C++ using POSIX threads.

Each pool has a designated worker function, and expects to be given a number of
work items. Any thread in the pool can take a work item, and will pass the work
item to the pool's worker function. The work items are `void *`, and are passed
to the worker function exactly as they are given to `pool_enqueue`. The return
values of the worker functions are ignored.

Four functions of interest are provided:

  - `pool_start` will start a new pool. The worker function and number of
    threads in the pool need to be given as arguments.
  - `pool_enqueue` will add a new work item to the pool. The work item data
    pointer should be passed, as well as a flag specifying whether the work item
    should be free'd after the work item has been processed (or if the pool is
    terminated).
  - `pool_wait` will block until all queued work items have been processed.
  - `pool_end` should be called when the pool is no longer needed. This
    terminates the threads, deallocates the queue and the pool, as well as any
    freeable work items.

Further documentation is given in Doxygen format in `pthread_pool.h`.
