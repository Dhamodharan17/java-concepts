### Multithreading :
**ability of a program to execute multiple threads simultaneosuly within a single process.**

Multithreading refers to the ability of a program to execute multiple threads simultaneously within a single process. Each thread runs independently of the other threads and can perform its own set of tasks. Multithreading can help improve the responsiveness of a program by allowing it to continue running while performing other tasks in the background.

### Concurrency :
**ability of multiple threads to access shared resoueces simultaneosuly.**
Concurrency, on the other hand, refers to the ability of multiple threads to access shared resources simultaneously. 
In a concurrent program, multiple threads can access the same piece of data or code at the same time, 
which can result in conflicts and synchronization issues if not handled properly.

- both can be supported in java through threads and synchornization mechanism such as locks, semaphores and monitors.

  **Thread Creation**
  - By extending Thread class - override run method
  - By implementing Runnable interface - implement run method

 **Synchronization**
 - using **synchronized** keyword which allow only one thread at a time to any shared resource.
- Java also provides other synchronization mechanisms such as semaphores and monitors, which can be used to coordinate
access to shared resources in more complex scenarios.

**Atomic Operations**
- these operation are executed atomically they cannot be interrupted by other threads.

**Deadlock Prevention**
- 2 threads waiting forever for each other to complete.
- to prevent deadlocks ensure locks are acquired and released in consistent order.
  
Another important consideration in Java concurrency is deadlock prevention. Deadlocks occur when two or more threads are waiting
for each other to release a lock, resulting in a deadlock situation where none of the threads can proceed. To prevent deadlocks,
it is important to ensure that locks are acquired and released in a consistent order, and to avoid holding onto locks for long periods of time.

## Multitasking 
- **multitasking allows several activities to run concurrently on the computer.**

  **Types**
  1. Process based multitasking - running notepad and music player
  2. Thread based - video player ( one thread handle video and another audio)

**Thread** 
- independent sequential path of execution within a program
- threads indpending and don't share memory
**Process**
  - instance of program that being executed
    

  


