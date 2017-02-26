## Spinning vs Queueing
Defines how a thread should wait when it has to wait. It can wait by polling, if the waiting time is expected to be short. It may also be suspended and put into a wait queue, and wakened up when it's signaled.

## Hardware vs Software
Mutex can be implemented with hardware compare-and-swap. It can also be implemented in software by Peterson's algorithm.

## Models
Mutex and cooperation are two types of interaction between threads. 

Sometimes they are both called synchronization and sometimes only coopration is called synchronization.

- Condition variables
- Mutex
  - guarantees only one thread executes a critical region at a given time
  - used when 
- Cooperation 
  - guarantees things happen in a specific order. 
