# 🧵 Multithreading Models

> Multithreading Models define the relationship between User-Level Threads and Kernel-Level Threads. They determine how threads created by applications are mapped to threads managed by the Operating System kernel. Understanding these models is essential for Linux, Operating Systems, Concurrent Programming, RTOS, and Interview Preparation.

---

# 📌 Introduction

When an application creates multiple threads:

```text
Browser Thread
Download Thread
Rendering Thread
Audio Thread
```

Question:

```text
How does the Operating System manage them?
```

Do all application threads directly become kernel threads?

```text
Not Always
```

This relationship is defined by:

```text
Multithreading Models
```

---

# Why Do We Need Multithreading Models?

Creating a Kernel Thread is expensive.

Reasons:

```text
Kernel Involvement

Memory Allocation

Scheduling Overhead

Context Switching Cost
```

To improve performance:

```text
User Threads
```

were introduced.

Now we need a mapping between:

```text
User Threads
        and
Kernel Threads
```

---

# Basic Terminology

## User-Level Thread (ULT)

Managed by:

```text
User Thread Library
```

Examples:

```text
POSIX Thread Libraries

Java Runtime

Green Threads
```

Kernel may not even know they exist.

---

## Kernel-Level Thread (KLT)

Managed directly by:

```text
Operating System Kernel
```

Examples:

```text
Linux Threads

Windows Threads
```

Kernel schedules them.

---

# Overview of Models

There are three major multithreading models:

```text
1. Many-to-One

2. One-to-One

3. Many-to-Many
```

---

# Visual Overview

```text
User Threads
      │
      ▼
Thread Model
      │
      ▼
Kernel Threads
```

---

# 1️⃣ Many-to-One Model

---

# Architecture

```text
User Threads

T1
T2
T3
T4

 │
 │
 ▼

Single Kernel Thread
```

---

# Mapping

```text
Many User Threads
          │
          ▼
One Kernel Thread
```

---

# Example

```text
T1
T2
T3
T4
```

All mapped to:

```text
Kernel Thread K1
```

---

# Diagram

```text
T1 ─┐
T2 ─┤
T3 ─┤────► K1
T4 ─┘
```

---

# Advantages

### Fast Thread Creation

No kernel involvement.

---

### Fast Context Switching

User-space operation.

---

### Low Memory Usage

Only one kernel thread.

---

### Simple Implementation

Easy to design.

---

# Disadvantages

### No Parallelism

Only one kernel thread exists.

Multiple CPUs cannot be utilized.

---

### Blocking Problem

If one thread performs:

```text
Blocking I/O
```

entire process blocks.

---

### Poor Scalability

Cannot benefit from multicore systems.

---

# Example

Suppose:

```text
T1 Reading File
```

gets blocked.

Result:

```text
T2
T3
T4
```

also stop.

---

# Historical Examples

```text
Green Threads

Early Java Implementations
```

---

# Summary

```text
Many User Threads
       ↓
One Kernel Thread
       ↓
Fast But Limited
```

---

# 2️⃣ One-to-One Model

---

# Architecture

```text
T1 ─► K1

T2 ─► K2

T3 ─► K3

T4 ─► K4
```

---

# Mapping

```text
One User Thread
        │
        ▼
One Kernel Thread
```

---

# Diagram

```text
T1 ─────► K1

T2 ─────► K2

T3 ─────► K3

T4 ─────► K4
```

---

# Advantages

### True Parallelism

Threads can run on different CPUs.

---

### Better Performance

On multicore systems.

---

### Blocking Isolation

If one thread blocks:

```text
Other Threads Continue
```

---

### Kernel Scheduling

OS has full visibility.

---

# Disadvantages

### Higher Overhead

Every user thread requires:

```text
Kernel Thread
```

---

### More Memory Usage

Each kernel thread requires resources.

---

### Thread Creation Cost

Higher than Many-to-One.

---

# Example

System:

```text
4 CPU Cores
```

Threads:

```text
T1
T2
T3
T4
```

All can run simultaneously.

---

# Linux Uses One-to-One

Linux implementation:

```c
pthread_create()
```

creates:

```text
User Thread
      ↓
Kernel Thread
```

---

# Windows Uses One-to-One

Modern Windows follows the same concept.

---

# Summary

```text
One User Thread
       ↓
One Kernel Thread
       ↓
True Parallelism
```

---

# 3️⃣ Many-to-Many Model

---

# Architecture

```text
User Threads

T1
T2
T3
T4
T5
T6

      │
      ▼

Kernel Threads

K1
K2
K3
```

---

# Mapping

```text
Many User Threads
          │
          ▼
Many Kernel Threads
```

---

# Diagram

```text
T1 ─┐
T2 ─┤
T3 ─┤
T4 ─┼────► K1
T5 ─┼────► K2
T6 ─┘────► K3
```

---

# Key Idea

Application may create:

```text
1000 User Threads
```

but OS manages:

```text
100 Kernel Threads
```

---

# Advantages

### Good Scalability

Supports large numbers of threads.

---

### True Parallelism

Multiple kernel threads execute simultaneously.

---

### Lower Overhead

Compared to One-to-One.

---

### Flexible Resource Usage

Efficient thread management.

---

# Disadvantages

### Complex Implementation

Mapping is difficult.

---

### Scheduling Complexity

Thread assignment becomes challenging.

---

### Rarely Used Today

Most modern OS use One-to-One.

---

# Summary

```text
Many User Threads
       ↓
Many Kernel Threads
       ↓
Balanced Approach
```

---

# Comparison Table

| Feature           | Many-to-One | One-to-One | Many-to-Many |
| ----------------- | ----------- | ---------- | ------------ |
| Parallelism       | No          | Yes        | Yes          |
| Blocking Issue    | Yes         | No         | No           |
| Complexity        | Low         | Medium     | High         |
| Memory Usage      | Low         | High       | Medium       |
| Scalability       | Poor        | Good       | Excellent    |
| Kernel Visibility | No          | Yes        | Partial      |

---

# Visual Comparison

## Many-to-One

```text
T1
T2
T3
T4
 │
 ▼
K1
```

---

## One-to-One

```text
T1 → K1
T2 → K2
T3 → K3
T4 → K4
```

---

## Many-to-Many

```text
T1
T2
T3
T4
 │
 ▼
K1 K2 K3
```

---

# Which Model Does Linux Use?

Linux uses:

```text
One-to-One Model
```

---

# Why?

Benefits:

```text
True Parallelism

Simple Scheduling

Multicore Support
```

---

# Linux Example

Create threads:

```c
pthread_create()
```

Observe threads:

```bash
ps -eLf
```

---

# RTOS Perspective

RTOS generally uses:

```text
One-to-One
```

style scheduling.

Each task is directly managed by scheduler.

---

# Example

FreeRTOS:

```text
Task A

Task B

Task C
```

Scheduler sees every task.

---

# AUTOSAR Perspective

AUTOSAR OS does not use traditional thread models.

Instead it manages:

```text
Basic Tasks

Extended Tasks

ISRs
```

directly.

Conceptually similar to:

```text
One-to-One
```

management.

---

# Multicore Perspective

Suppose:

```text
8 CPU Cores
```

---

# Many-to-One

```text
Only One Core Used
```

---

# One-to-One

```text
Multiple Cores Used
```

---

# Many-to-Many

```text
Multiple Cores Used
Efficiently
```

---

# Real World Analogy

Restaurant Example

---

# Many-to-One

```text
10 Waiters

1 Chef
```

Bottleneck occurs.

---

# One-to-One

```text
10 Waiters

10 Chefs
```

Maximum performance.

---

# Many-to-Many

```text
10 Waiters

4 Chefs
```

Balanced approach.

---

# Interview Questions

## Q1. What are multithreading models?

Relationship between User Threads and Kernel Threads.

---

## Q2. What are the three models?

```text
Many-to-One

One-to-One

Many-to-Many
```

---

## Q3. Which model does Linux use?

```text
One-to-One
```

---

## Q4. Which model provides true parallelism?

```text
One-to-One

Many-to-Many
```

---

## Q5. Biggest problem with Many-to-One?

```text
Blocking

No Parallelism
```

---

## Q6. Which model is easiest to implement?

```text
Many-to-One
```

---

## Q7. Which model is most widely used today?

```text
One-to-One
```

---

## Q8. Why is Many-to-Many considered efficient?

Because many user threads share a smaller set of kernel threads.

---

# ⚠️ Common Interview Trap

Question:

```text
Does creating 100 threads mean 100 kernel threads?
```

Answer:

```text
Depends On Thread Model
```

---

# Many-to-One

```text
100 User Threads

1 Kernel Thread
```

---

# One-to-One

```text
100 User Threads

100 Kernel Threads
```

---

# Many-to-Many

```text
100 User Threads

N Kernel Threads
```

---

# 📝 Quick Revision

```text
Many-to-One
------------
Many User Threads
One Kernel Thread

Pros:
Fast

Cons:
No Parallelism

--------------------------------

One-to-One
-----------
One User Thread
One Kernel Thread

Pros:
Parallelism

Linux Uses This

Cons:
Higher Overhead

--------------------------------

Many-to-Many
------------
Many User Threads
Many Kernel Threads

Pros:
Balanced

Cons:
Complex

Linux
-----
One-to-One

Interview Keywords
------------------
ULT
KLT
Parallelism
Blocking
Thread Mapping
```

---

# 🎯 Key Takeaway

Multithreading Models define how user threads are mapped to kernel threads.

```text
Many-to-One
------------
Fast but Limited

One-to-One
-----------
True Parallelism
Used by Linux

Many-to-Many
------------
Flexible and Scalable
```

Understanding these models is critical before learning:

* Thread Synchronization
* Mutexes
* Semaphores
* Race Conditions
* Deadlocks
* Condition Variables
* Linux Pthreads
* Concurrent Programming
* RTOS Task Scheduling
