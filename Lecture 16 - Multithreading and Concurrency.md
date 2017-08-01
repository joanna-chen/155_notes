# Multithreading
When not executing commands, CPU executes *NOP* commands
* some need to wait for TCT to complete which will leave the CPU *NOP*ing for ages.

### Process: An executable program:
   * Memory locations allocate for program and needed heap/stack
   * Program + Heap + Stack = Process Memory Sector
   * At least 1 thread
 
### Thread: Sequence of Commands:
   * scheduled to run on CPU
   * all threads created within same process memory sector
   * created and destroyed dynamically (heap)
   * communicate with each other through shared memory sector
   * Faster to create and destroy, less time to swtich between threads in same process
   * threads can easily communicate due to same process
   
If any thread encounters error, whole process halts.
Independent processes can keep going if a related one stops.

# Thread Scheduling
## States:
### Executing: thread occupies one CPU and is being executed
### Ready: Thread has all needed resources and is waiting to occupy CPU
### Blocked: Thread does not have all resources and cannot occupy CPU

## Co-operative Multithreading:
Each thread yields to CPU proactively whenever appropriate.
* Suitable for embedded systems that do not manage threads
* efficient if no greedy threads

## Pre-emptive Multithreading:
OS forces threads to switch at certain times
* implemented in most standard OS
* can critically impact system performance based on OS decisions

## Priority:
* Higher Priority to tasks with hard deadlines (safety features)
* Lower Priority to tasks with soft deadlines (battery life)
* Missed Hard Deadlines: switch to more optimzed RTOS or install CPU with more cores 

# Timer Coalescing
CPU cores forced to execute code at random times, unoptimal

OS Bundles interrupt handler calls by itroducing minor timing adjustments << time period such that all handlers can be called

### Efficiency: less thread swapping, more meaningful execution
### Heisenbug: may occur if handlers are designed with dependencies

# UML Sequece Diagram:
## Instance:
   * Objects involved in interaction sequence (thread, process, system)
## Lifeline:
   * Vertical, dashed, unitless time line (time axis)
   * creation and destruction of corresponding instance (Action Box) will be drawn on lifeline
## Action Box:
   * Indicating Life Time of instance (Rectangular box on lifeline)
## Gate: Starting point

## Basic Elements: Messages:
1. Synchronous message: instance waits for response of *solid arrow-headed line with method call*
2. Asynchronous message: instance does not wait for response of *dotted arrow-headed line labelled with field containing response*
3. Message Condition: condition befre message can be issued; [Guard] Action

