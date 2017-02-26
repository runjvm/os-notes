## Atomicity
Atomicity means not interruptible(no process switch) and thus ensures mutex on a single processor machine. Although by itself atomic instruction does not provide mutex on a multiprocessor machine, since two processes could execute the atomic operation at the same time, memory(or cache) often provides memory lock to guarantee mutex in such case. See below. In this sense, atomicity always implies mutual exclusion. 
[ref](http://www.cs.nott.ac.uk/~psznza/G52CON/lecture4.pdf)

## Hardware vs Software
Low level mutex can be provided by RAM or CPU, because once at a really low level, two accesses to the same memory location cannot really happen "at the same time". High level mutex is built upon low level mutex. Although atomicity means not interruptible(no process switch), it also means mutual exclusive. A cpu can use its own machanism to ensure atomicity of an instruction, it may also uses supports from RAM, such as dual-port RAM. A DPRAM set an internal flag when CPU1 issuses an atomic operation. If CPU2 issues an operation to the same location, DPRAM issues a BUSY interrupt. 
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
  - cv has to be used together with a mutex and in such a pattern as below
  - [cond_wait unlocks and locks the mutex](https://stackoverflow.com/questions/14924469/does-pthread-cond-waitcond-t-mutex-unlock-and-then-lock-the-mutex)
  - [another good discussion](http://stackoverflow.com/questions/2763714/why-do-pthreads-condition-variable-functions-require-a-mutex)
  
## Implementation
- Mutex
  - hardware: atomically set a flag
  - software: Peterson's algorithm, etc

Other models can be built upon mutex, or implemented using similar ideas. 

## Spinning vs Switching
Defines how a thread should wait when it has to wait. It can wait by polling, if the waiting time is expected to be short. It may also be suspended and put into a wait queue, and try again later or wait for a signal.

## Atomicity
An atomic opeation can be one machine instruction, such as Intel's CMPXCHG. Such atomic opeations can be used to implement a mutex by atomically setting a memory location as a flag. When other threads see the flag is set, they either busy wait or release the cpu. The hadeware implementation of such atomic instruction can be complicated and need cache coherence protocol. 

Compare-and-swap is a generalization of an atomic instruction. A function can be written in a CAS fashion to ensure atomicity(compute the new value and do an instruction-level CAS at the end). Such functions provide wait-free mutex.
