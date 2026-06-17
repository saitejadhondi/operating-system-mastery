# 🧵 Threads in Operating Systems

> A Thread is the smallest unit of CPU execution inside a process. Threads enable concurrent execution within the same process, improving responsiveness, resource utilization, and overall system performance. Understanding threads is essential for Operating Systems, Linux, Multithreading, RTOS, and Interview Preparation.

---

# 📌 Introduction

Consider a web browser.

While using Chrome:

```text
Loading Web Page

Playing YouTube Video

Downloading Files

Running JavaScript

Handling Mouse Clicks
```

Question:

```text
Does Chrome create a separate process for every task?
```

Not always.

Instead:

```text
One Process
    ↓
Multiple Threads
```

perform different tasks simultaneously.

---

# What is a Thread?

## Definition

A Thread is the smallest unit of CPU execution that can be scheduled independently by the Operating System.

---

# Simple Definition

```text
Process
-------
Container

Thread
------
Worker
```

---

# Process vs Thread

Imagine:

```text
Restaurant = Process

Employees = Threads
```

The restaurant provides:

```text
Building

Kitchen

Resources
```

Employees perform actual work.

---

# Visual Representation

```text
Process
│
├── Thread 1
├── Thread 2
├── Thread 3
└── Thread 4
```

---

# What Does a Thread Contain?

Each thread has its own:

```text
Program Counter (PC)

Registers

Stack

Thread State
```

---

# Shared Resources

Threads belonging to the same process share:

```text
Code Section

Data Section

Heap Memory

Open Files

Global Variables
```

---

# Thread Structure

```text
                Process
                     │
 ┌─────────────────────────────────┐
 │ Code Segment                    │
 │ Data Segment                    │
 │ Heap                            │
 └─────────────────────────────────┘
      │         │         │
      ▼         ▼         ▼

   Thread1   Thread2   Thread3

   Stack     Stack     Stack

   PC         PC        PC

   Registers Registers Registers
```

---

# Why Do We Need Threads?

Without threads:

```text
One Task At A Time
```

---

# Example

Single-threaded Browser:

```text
Download File
      ↓
UI Freezes
```

Bad user experience.

---

# With Threads

```text
Thread 1 → UI

Thread 2 → Download

Thread 3 → Rendering
```

Everything remains responsive.

---

# Benefits of Threads

### Better Responsiveness

Applications remain usable while background work continues.

---

### Resource Sharing

Threads share process resources.

---

### Faster Context Switching

Thread switch is cheaper than process switch.

---

### Improved CPU Utilization

Multiple threads can execute simultaneously.

---

# Single-Threaded Process

```text
Process
   │
   ▼
Thread
   │
   ▼
CPU
```

Only one task executes.

---

# Multi-Threaded Process

```text
Process
│
├── Thread 1
├── Thread 2
├── Thread 3
└── Thread 4
```

Multiple tasks execute concurrently.

---

# Example

Microsoft Word:

```text
Thread 1
---------
Typing

Thread 2
---------
Spell Check

Thread 3
---------
Auto Save

Thread 4
---------
Printing
```

---

# Thread States

A thread moves through various states.

---

# Thread State Diagram

```text
NEW
 │
 ▼
READY
 │
 ▼
RUNNING
 │
 ├─────────────► TERMINATED
 │
 ▼
WAITING
 │
 ▼
READY
```

---

# New State

Thread created.

Waiting for scheduling.

---

# Ready State

Ready to execute.

Waiting for CPU.

---

# Running State

Currently executing on CPU.

---

# Waiting State

Waiting for:

```text
I/O

Mutex

Semaphore

Event
```

---

# Terminated State

Execution completed.

---

# Thread Control Block (TCB)

Similar to PCB for processes.

---

# What is TCB?

Operating System data structure used to manage a thread.

---

# TCB Contains

```text
Thread ID

Thread State

Registers

Stack Pointer

Program Counter

Scheduling Information
```

---

# Thread Lifecycle

```text
Create Thread
      │
      ▼
Ready Queue
      │
      ▼
Running
      │
      ▼
Blocked
      │
      ▼
Ready
      │
      ▼
Exit
```

---

# Thread Creation

Linux Example:

```c
pthread_create()
```

---

# Example

```c
#include <pthread.h>

void* task(void* arg)
{
    return NULL;
}

int main()
{
    pthread_t tid;

    pthread_create(
        &tid,
        NULL,
        task,
        NULL
    );

    pthread_join(tid,NULL);

    return 0;
}
```

---

# Thread Termination

Linux:

```c
pthread_exit()
```

---

# Thread Synchronization

Multiple threads share memory.

Problem:

```text
Race Condition
```

may occur.

---

# Example

Two threads:

```text
Counter++
```

simultaneously.

Expected:

```text
2
```

Actual:

```text
1
```

possible.

---

# Solution

Use:

```text
Mutex

Semaphore

Spinlock

Condition Variable
```

---

# Thread Context Switching

Thread switch is cheaper than process switch.

---

# Why?

Threads share:

```text
Address Space

Files

Memory
```

Only:

```text
Registers

Stack

PC
```

need updating.

---

# Process vs Thread Context Switch

## Process Switch

```text
PCB Switch

Memory Mapping

TLB Effects

Cache Effects
```

Expensive.

---

## Thread Switch

```text
Registers

Stack

Program Counter
```

Cheaper.

---

# User-Level Threads

Managed by:

```text
User Library
```

instead of kernel.

---

# Examples

```text
Green Threads

Language Runtimes
```

---

# Advantages

```text
Very Fast
```

---

# Disadvantages

```text
Kernel Unaware
```

Blocking thread may block entire process.

---

# Kernel-Level Threads

Managed by:

```text
Operating System Kernel
```

---

# Examples

Linux:

```text
POSIX Threads (Pthreads)
```

---

# Advantages

```text
True Parallelism

Kernel Scheduling
```

---

# Disadvantages

```text
More Overhead
```

than user-level threads.

---

# User Thread vs Kernel Thread

| Feature            | User Thread    | Kernel Thread    |
| ------------------ | -------------- | ---------------- |
| Managed By         | User Library   | Kernel           |
| Speed              | Faster         | Slower           |
| Context Switch     | Cheap          | More Expensive   |
| Parallel Execution | Limited        | True Parallelism |
| Blocking           | Entire Process | Single Thread    |

---

# Multithreading Models

---

# Many-to-One

```text
Multiple User Threads
          │
          ▼
One Kernel Thread
```

---

# One-to-One

```text
One User Thread
       │
       ▼
One Kernel Thread
```

Used by Linux.

---

# Many-to-Many

```text
Many User Threads
         │
         ▼
Many Kernel Threads
```

---

# Comparison

| Model        | Parallelism | Complexity |
| ------------ | ----------- | ---------- |
| Many-to-One  | No          | Low        |
| One-to-One   | Yes         | Medium     |
| Many-to-Many | Yes         | High       |

---

# Linux Perspective

Linux uses:

```text
One-to-One Thread Model
```

---

# Thread Creation

```c
pthread_create()
```

---

# Wait for Thread

```c
pthread_join()
```

---

# View Threads

```bash
ps -eLf
```

---

# RTOS Perspective

RTOS generally calls threads:

```text
Tasks
```

---

# Example

FreeRTOS:

```text
Task A

Task B

Task C
```

executing concurrently.

---

# AUTOSAR Perspective

AUTOSAR OS uses:

```text
Basic Tasks

Extended Tasks
```

similar to threads.

---

# Embedded Systems Perspective

Threads are used for:

```text
Sensor Reading

Communication

Display Updates

Control Logic
```

running simultaneously.

---

# Real World Analogy

Restaurant Example

```text
Restaurant
----------
Process

Waiter
------
Thread

Chef
----
Thread

Cashier
-------
Thread
```

All workers share:

```text
Kitchen

Tables

Resources
```

but perform different tasks.

---

# Advantages of Threads

✅ Faster than processes

✅ Resource sharing

✅ Better responsiveness

✅ Improved concurrency

✅ Lower memory usage

---

# Disadvantages of Threads

❌ Synchronization issues

❌ Race conditions

❌ Deadlocks

❌ Debugging complexity

❌ Shared memory risks

---

# Interview Questions

## Q1. What is a Thread?

Smallest unit of CPU execution.

---

## Q2. Difference Between Process and Thread?

Process owns resources.

Thread executes work.

---

## Q3. What resources are shared between threads?

```text
Code

Data

Heap

Files
```

---

## Q4. What resources are private to each thread?

```text
Stack

Registers

Program Counter
```

---

## Q5. Why are threads faster than processes?

Because threads share address space and resources.

---

## Q6. What is TCB?

Thread Control Block.

Stores thread information.

---

## Q7. What is the thread model used by Linux?

```text
One-to-One
```

---

## Q8. What problems occur in multithreading?

```text
Race Conditions

Deadlocks

Synchronization Issues
```

---

# ⚠️ Common Interview Trap

Question:

```text
Do threads have separate heap memory?
```

Answer:

```text
No.
```

Threads share:

```text
Heap

Code

Data
```

but have separate:

```text
Stack

Registers

Program Counter
```

---

# 📝 Quick Revision

```text
Thread
------
Smallest Unit Of Execution

Shares
-------
Code
Data
Heap
Files

Owns
----
Stack
Registers
Program Counter

Thread States
-------------
New
Ready
Running
Waiting
Terminated

Models
------
Many-to-One
One-to-One
Many-to-Many

Linux
-----
pthread_create()
pthread_join()

Advantages
----------
Fast
Responsive
Shared Resources

Disadvantages
-------------
Race Conditions
Deadlocks
Synchronization Issues
```

---

# 🎯 Key Takeaway

Threads are lightweight execution units within a process. They share process resources while maintaining their own execution context, making them faster and more efficient than processes.

Understanding threads is essential before learning:

* Multithreading Models
* Thread Synchronization
* Mutexes
* Semaphores
* Race Conditions
* Deadlocks
* Linux Pthreads
* RTOS Tasks
* AUTOSAR Task Scheduling
* Concurrent Programming
