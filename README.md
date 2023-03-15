# readers-writers-using-pthreads
## Problem Statement:
Reader-Writer Problem, pertains to any situation where a data structure, database, or file system is read and modified by concurrent threads. While the data structure is being written or modified it is often necessary to bar other threads from reading, in order to prevent a reader from interrupting a modification in progress and reading inconsistent or invalid data.The synchronization constraints are:
1. Any number of readers can be in the critical section simultaneously.
2. Writers must have exclusive access to the critical section.

In other words, a writer cannot enter the critical section while any other thread (reader or writer) is there, and while the writer is there, no other thread may enter.
## Solution:
1. Semaphore_mut(To make reader processes those which entered the queue after writer processes wait).
2. Semaphore_rd (Mututal exclusion for  readers count).
3. Semaphore_wrt (To make writer wait while reading).\
All these semaphores are intialized to 1 at the start.\
There is an integer variable(readerscount) intialized to 0 at the start.\
There is a integer type common_variable which is being read by reader() process and incremented by writer() process. common_variable is initialised to 0 at the start.

Consider the following threads to be created : 
rrrwwrrrrw (r- reader, w- writer).

>Let's assume that reader first enters critical section making the value of readerscount 1 and so makes semaphore_wrt to 0 so that writer   doesn't access the            critical section.\
>Multiple readers may enter critical section as semaphore_mut and semaphore_rd are set to 1 after incrementing readers_count.\
>When a writer thread arrives while reader is in critical section, writer cannot enter critical section as semaphore_wrt is set to 0 when the value of                    readerscount became 1.\
>When all the readers in critical section exit, value of readerscount is made to 0 and so semaphore_wrt is set to 1,so that writer can enter critical section.\
>when writer process is in critical section, the reader processes which come after the writer process will be stopped as semaphore_mut is set to 0 by the writer    thread.This ensures the code to be starve free.\
>When writer is in critical section then remaining readers and writers have equal chance to enter the critical section when the writer exits from the critical section.\
>If we start with writer in critical section first,it will be executed from the state mentioned in point 5.
