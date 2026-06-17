# 🏢 Multilevel Queue (MLQ) Scheduling

> Multilevel Queue (MLQ) Scheduling is an advanced CPU scheduling algorithm where the Ready Queue is divided into multiple separate queues based on process type, priority, or characteristics. Each queue can have its own scheduling algorithm and priority level.

---

# 📌 Introduction

In previous scheduling algorithms:

```text
FCFS
SJF
SRTF
RR
Priority
```

All processes existed in a:

```text
Single Ready Queue
```

Problem:

Not all processes are equal.

Example:

```text
System Processes

Interactive Processes

Background Processes

Batch Processes
```

Should all be treated the same?

```text
No
```

This led to:

```text
Multilevel Queue Scheduling
```

---

# 🏛️ What is Multilevel Queue Scheduling?

## Definition

Multilevel Queue Scheduling divides the Ready Queue into multiple independent queues.

Each queue:

```text
Has Its Own Priority

Has Its Own Scheduling Algorithm
```

---

# Basic Idea

Instead of:

```text
Ready Queue
------------
P1 P2 P3 P4 P5
```

we create:

```text
System Queue

Interactive Queue

Batch Queue
```

---

# Architecture

```text
                    CPU
                     ▲
                     │
     ┌──────────────────────────┐
     │     Scheduler Chooses    │
     └──────────────────────────┘
                     ▲
                     │

 ┌─────────────┐
 │ System Queue│
 └─────────────┘

 ┌─────────────┐
 │ Interactive │
 └─────────────┘

 ┌─────────────┐
 │ Batch Queue │
 └─────────────┘
```

---

# Why MLQ?

Different process categories have different requirements.

---

# Example

## System Process

```text
OS Services

Interrupt Handlers

Kernel Tasks
```

Need:

```text
Very Fast Response
```

---

# Interactive Process

```text
Browser

Terminal

VS Code
```

Need:

```text
Good User Experience
```

---

# Batch Process

```text
Backup Jobs

Data Analysis

Reports
```

Can wait longer.

---

# Queue Separation

Typical MLQ System:

```text
Queue 1
System Processes

Queue 2
Interactive Processes

Queue 3
Batch Processes
```

---

# Example Structure

```text
Highest Priority
----------------
System Queue

Medium Priority
---------------
Interactive Queue

Lowest Priority
---------------
Batch Queue
```

---

# Scheduling Inside Each Queue

Each queue may use a different scheduling algorithm.

---

# Example

```text
System Queue
Priority Scheduling

Interactive Queue
Round Robin

Batch Queue
FCFS
```

---

# Visual Example

```text
System Queue
------------
Priority

Interactive Queue
-----------------
Round Robin

Batch Queue
-----------
FCFS
```

---

# Queue Scheduling Methods

Two major approaches exist.

---

# 1️⃣ Fixed Priority Scheduling

Higher-priority queues always execute first.

---

# Example

```text
Queue 1
System

Queue 2
Interactive

Queue 3
Batch
```

If Queue 1 contains processes:

```text
Queue 2 And Queue 3 Wait
```

---

# Visual

```text
System Queue
     │
     ▼
CPU

Interactive Waits

Batch Waits
```

---

# Problem

Can cause:

```text
Starvation
```

---

# Example

System queue continuously receives tasks.

Then:

```text
Batch Queue
Never Executes
```

---

# 2️⃣ Time Slice Between Queues

CPU time divided among queues.

---

# Example

```text
System Queue
50%

Interactive Queue
30%

Batch Queue
20%
```

---

# Visual

```text
CPU Time

50% System

30% Interactive

20% Batch
```

---

# Advantage

Every queue gets CPU time.

---

# Example 1

Three Queues:

```text
Q1 = System

Q2 = Interactive

Q3 = Batch
```

Scheduling:

```text
Q1 → Priority

Q2 → RR

Q3 → FCFS
```

---

# Processes

```text
System Queue
-------------
S1
S2

Interactive
------------
I1
I2

Batch
-------
B1
```

---

# Fixed Priority Execution

Order:

```text
S1

S2

I1

I2

B1
```

---

# Example 2

CPU Distribution:

```text
System
50%

Interactive
30%

Batch
20%
```

Execution:

```text
System Tasks
5 ms

Interactive Tasks
3 ms

Batch Tasks
2 ms
```

Cycle repeats.

---

# Advantages

### Process Classification

Processes grouped by behavior.

---

### Better Response Time

Interactive tasks receive faster service.

---

### Flexible

Different algorithms for different queues.

---

### Useful For Multi-User Systems

Supports diverse workloads.

---

# Disadvantages

### Starvation

Low-priority queues may suffer.

---

### Static Assignment

Process permanently belongs to one queue.

---

### Poor Flexibility

Cannot adapt to workload changes.

---

### Complex Configuration

Need to decide:

```text
Number Of Queues

Queue Priorities

Scheduling Policies
```

---

# Biggest Limitation

Processes cannot move between queues.

---

# Example

Suppose:

```text
Batch Process
```

becomes highly interactive.

Still:

```text
Remains In Batch Queue
```

---

# This Problem Leads To...

```text
Multilevel Feedback Queue
(MLFQ)
```

which allows:

```text
Queue Migration
```

---

# Starvation Problem

Most important interview topic.

---

# Example

```text
System Queue
Always Busy
```

Interactive Queue:

```text
Waiting
```

Batch Queue:

```text
Waiting
```

forever.

---

# Solution

Use:

```text
Time Slicing Between Queues
```

or

```text
Aging
```

---

# Comparison With Priority Scheduling

Priority Scheduling:

```text
Priority Per Process
```

---

# MLQ Scheduling:

```text
Priority Per Queue
```

---

# Comparison

| Feature              | Priority | MLQ      |
| -------------------- | -------- | -------- |
| Priority Applied To  | Process  | Queue    |
| Multiple Queues      | No       | Yes      |
| Different Algorithms | No       | Yes      |
| Starvation           | Possible | Possible |

---

# Comparison With Round Robin

| Feature          | RR  | MLQ |
| ---------------- | --- | --- |
| Single Queue     | Yes | No  |
| Multiple Classes | No  | Yes |
| Queue Priorities | No  | Yes |

---

# Real Operating System Example

Classic UNIX systems used queue-based scheduling concepts.

Example:

```text
Foreground Jobs

Background Jobs
```

received different treatment.

---

# Linux Perspective

Linux does not use pure MLQ.

Modern Linux uses:

```text
CFS
Completely Fair Scheduler
```

However:

```text
Real-Time

Normal

Idle
```

scheduling classes resemble MLQ concepts.

---

# Linux Scheduling Classes

```text
Real-Time Class

Normal Class

Idle Class
```

Higher classes execute first.

---

# RTOS Perspective

RTOS generally uses:

```text
Priority Scheduling
```

instead of MLQ.

But conceptually:

```text
Critical Tasks

Normal Tasks

Background Tasks
```

may be separated.

---

# AUTOSAR Perspective

AUTOSAR OS does not implement classic MLQ.

Instead it relies on:

```text
Priority-Based Scheduling
```

with:

```text
Tasks

Events

ISRs
```

assigned priorities.

---

# Real World Analogy

Hospital

---

# Queue 1

```text
Emergency Patients
```

---

# Queue 2

```text
Regular Patients
```

---

# Queue 3

```text
Routine Checkups
```

Doctor always treats:

```text
Emergency Patients
```

first.

This is MLQ.

---

# Interview Questions

## Q1. What is Multilevel Queue Scheduling?

Ready Queue divided into multiple separate queues.

---

## Q2. Can each queue have a different scheduling algorithm?

```text
Yes
```

---

## Q3. What is the biggest limitation?

```text
Processes Cannot Move Between Queues
```

---

## Q4. Can MLQ cause starvation?

```text
Yes
```

Low-priority queues may never execute.

---

## Q5. How is MLQ different from Priority Scheduling?

Priority Scheduling:

```text
Priority Per Process
```

MLQ:

```text
Priority Per Queue
```

---

## Q6. How can starvation be reduced?

```text
Time Slicing

Aging
```

---

## Q7. Does Linux use MLQ?

Not directly.

Linux uses:

```text
CFS
```

but scheduling classes resemble MLQ.

---

## Q8. What improvement came after MLQ?

```text
Multilevel Feedback Queue
```

because it allows process movement.

---

# ⚠️ Common Interview Trap

Question:

```text
Can a process move from one queue to another in MLQ?
```

Answer:

```text
No.
```

Queue assignment is fixed.

That feature exists in:

```text
MLFQ
(Multilevel Feedback Queue)
```

---

# 📝 Quick Revision

```text
MLQ
---
Multilevel Queue Scheduling

Concept
-------
Multiple Ready Queues

Examples
--------
System Queue
Interactive Queue
Batch Queue

Scheduling
----------
Different Algorithm Per Queue

Advantages
----------
Fast Response
Flexible Policies

Disadvantages
-------------
Starvation
Static Queue Assignment

Important Difference
--------------------
MLQ:
No Queue Movement

MLFQ:
Queue Movement Allowed

Interview Keywords
------------------
Queue Priority
Static Assignment
Starvation
Multiple Scheduling Policies
```

---

# 🎯 Key Takeaway

Multilevel Queue Scheduling divides processes into separate queues based on their type and importance. Each queue may use a different scheduling algorithm and priority level.

While MLQ improves organization and responsiveness, it suffers from:

```text
Static Queue Assignment

Starvation
```

These limitations led to the development of:

```text
Multilevel Feedback Queue (MLFQ)
```

which is considered one of the most powerful CPU scheduling algorithms and is heavily asked in interviews.
