## Terms
Mutex can both mean mutual exclusion(ME), which is a result, or mutex lock, which is a method to guarantee mutual exclusion. Mutual exclusion can also be lock-free when it uses atomic compare-and-swap. Lock-free in this context means high-level lock free, since machine locks are needed for atomicity.

## Atomicity
Atomicity means not interruptible(no process switch) and thus ensures mutual exclusion on a single processor machine. Although by itself atomic instruction does not provide mutual exclusion on a multiprocessor machine, since two processes could execute the atomic operation at the same time, memory(or cache) often provides memory lock to guarantee mutual exclusion in such case. See below. In this sense, atomicity always implies mutual exclusion. 
[ref](http://www.cs.nott.ac.uk/~psznza/G52CON/lecture4.pdf)

Low level atomicity is accomplished by hardware lock. At a high level, critical section's ME can be guaranteed by a mutex lock, or a semaphore, or some other lock-free approaches such as compare-and-swap.

In some context, atomic opration implies lock-free. For example, in HotSpot VM's context, the lightweight lock is called "aquired by atomic operation" sometimes.

## Hardware Atomicity
Low level ME can be provided by memory or CPU, because once at a really low level, two accesses to the same memory location cannot really happen "at the same time". High level ME is built upon low level ME. A cpu can use its own machanism to ensure atomicity of an instruction, it may also uses supports from RAM, such as dual-port RAM. A DPRAM set an internal flag when CPU1 issuses an atomic operation. If CPU2 issues an operation to the same location, DPRAM issues a BUSY interrupt. 
[test-and-set hardware imeplementation](https://en.wikipedia.org/wiki/Test-and-set)

## Models
Mutex and cooperation are two types of interaction between threads. 
- Mutex
  - guarantees only one thread executes a critical region at a given time
  - used when accessing a shared resource
- Cooperation
  - guarantees things happen in a specific order

Sometimes they are both called synchronization and sometimes only coopration is called synchronization.
- Condition variables
  - cv = a mutex + notify system
  - cv has to be used together with a mutex and in such a pattern as below
  - [cond_wait unlocks and locks the mutex](https://stackoverflow.com/questions/14924469/does-pthread-cond-waitcond-t-mutex-unlock-and-then-lock-the-mutex)
  - [another good discussion](http://stackoverflow.com/questions/2763714/why-do-pthreads-condition-variable-functions-require-a-mutex)

- Monitor
  - as a general concept: condition variables + a mutex
  - in Java means a lock and a wait set
  
- Semaphore
  - use as a mutex: guard the critical section with sem.wait() and sem.post()
  - use as a condition variable
    - by incrementng and decrementing the semaphore, a sem == 0 condition is implied as wait condition
    - in a Monitor, a wait condition and a cv are two variables. The two are combined in semaphore
    
## Implementation
- Mutex
  - hardware: atomically set a flag. Other threads busy wait or sleep.
  - software: Peterson's algorithm, etc

Other models can be built upon mutex, or implemented using similar hardware atomic operations. 

## Spinning vs Switching
Defines how a thread should wait when it has to wait. It can wait by polling, if the waiting time is expected to be short. It may also be suspended and put into a wait queue, and try again later or wait for a signal.

