## Spinning vs Switching
Defines how a thread should wait when it has to wait. It can wait by polling, if the waiting time is expected to be short. It may also be suspended and put into a wait queue, and try again later or wait for a signal.

## Hardware vs Software
Mutex can be implemented with hardware compare-and-swap. It can also be implemented in software by Peterson's algorithm.

## Models
Mutex and cooperation are two types of interaction between threads. 
- Mutex
  - guarantees only one thread executes a critical region at a given time
  - used when accessing a shared resource

- Cooperation
  - guarantees things happen in a specific order.

Sometimes they are both called synchronization and sometimes only coopration is called synchronization.

- Condition variables
  - cv has to be used together with a mutex and in such a pattern as below
  - [cond_wait unlocks and locks the mutex](https://stackoverflow.com/questions/14924469/does-pthread-cond-waitcond-t-mutex-unlock-and-then-lock-the-mutex)
  - [another good discussion](http://stackoverflow.com/questions/2763714/why-do-pthreads-condition-variable-functions-require-a-mutex)
  
- Mutex

## Atomicity
An atomic opeation can be one machine instruction, such as Intel's CMPXCHG. Such atomic opeations can be used to implement a mutex by atomically setting a memory location as a flag. When other threads see the flag is set, they either busy wait or release the cpu. The hadeware implementation of such atomic instruction can be complicated and need cache coherence protocol. 

Compare-and-swap is a generalization of an atomic instruction. A function can be written in a CAS fashion to ensure atomicity(compute the new value and do an instruction-level CAS at the end). Such functions provide wait-free mutex.
