# 🔄 Round Robin (RR) Scheduling

> Round Robin (RR) is one of the most widely used CPU scheduling algorithms in modern operating systems. It is a preemptive scheduling algorithm designed specifically for time-sharing systems, ensuring fairness by giving each process a fixed time slice called a Time Quantum.

---

# 📌 Introduction

Imagine 4 people sharing a single computer.

If one person uses it for hours:

```text
Others Must Wait
```

This is unfair.

Instead:

```text
Person A → 5 min
Person B → 5 min
Person C → 5 min
Person D → 5 min
```

Everyone gets a turn.

This is the basic idea behind:

```text
Round Robin Scheduling
```

---

# 🏛️ What is Round Robin Scheduling?

## Definition

Round Robin Scheduling is a preemptive CPU scheduling algorithm where each process gets a fixed CPU time called Time Quantum.

If the process does not finish within that time:

```text
CPU Taken Away
       ↓
Moved To End Of Queue
```

---

# Key Concept

```text
Time Quantum (Time Slice)
```

A small fixed amount of CPU time assigned to each process.

---

# Example

```text
Time Quantum = 4 ms
```

Process:

```text
P1 = 10 ms
```

Execution:

```text
P1 Runs For 4 ms
       ↓
Preempted
       ↓
Moved To Queue End
```

---

# Characteristics

✅ Preemptive

✅ Fair Scheduling

✅ Good Response Time

✅ Suitable For Time Sharing Systems

❌ Context Switching Overhead

❌ Performance Depends On Time Quantum

---

# Type of Scheduling

Round Robin is:

```text
Preemptive
```

---

# Scheduling Workflow

```text
Ready Queue
      │
      ▼
Assign CPU
      │
      ▼
Time Quantum Expires?
      │
   Yes ▼ No
      │
Move To End
      │
      ▼
Next Process
```

---

# Queue Structure

Round Robin uses:

```text
Circular Queue
```

---

# Visual Representation

```text
P1 → P2 → P3 → P4
↑               ↓
└───────────────┘
```

Processes continuously rotate.

---

# Example 1

Processes:

| Process | Burst Time |
| ------- | ---------- |
| P1      | 10         |
| P2      | 5          |
| P3      | 8          |

Time Quantum:

```text
Q = 4 ms
```

---

# Step 1

Execute P1

```text
P1 = 10
```

Runs for:

```text
4 ms
```

Remaining:

```text
6 ms
```

---

# Step 2

Execute P2

```text
P2 = 5
```

Runs for:

```text
4 ms
```

Remaining:

```text
1 ms
```

---

# Step 3

Execute P3

```text
P3 = 8
```

Runs for:

```text
4 ms
```

Remaining:

```text
4 ms
```

---

# Queue Status

```text
P1(6)
P2(1)
P3(4)
```

---

# Continue Execution

```text
P1 → 4 ms
P2 → 1 ms
P3 → 4 ms
P1 → 2 ms
```

---

# Gantt Chart

```text
0   4   8   12  16 17 21 23
|P1|P2|P3|P1|P2|P3|P1|
```

---

# Completion Time

| Process | CT |
| ------- | -- |
| P2      | 17 |
| P3      | 21 |
| P1      | 23 |

---

# Turnaround Time

Formula:

```text
TAT = CT - AT
```

Assume:

```text
AT = 0
```

for all.

---

| Process | CT | TAT |
| ------- | -- | --- |
| P1      | 23 | 23  |
| P2      | 17 | 17  |
| P3      | 21 | 21  |

---

# Waiting Time

Formula:

```text
WT = TAT - BT
```

---

| Process | TAT | BT | WT |
| ------- | --- | -- | -- |
| P1      | 23  | 10 | 13 |
| P2      | 17  | 5  | 12 |
| P3      | 21  | 8  | 13 |

---

# Average Waiting Time

```text
(13 + 12 + 13)/3

= 12.67 ms
```

---

# Example 2

Processes:

| Process | Burst |
| ------- | ----- |
| P1      | 6     |
| P2      | 4     |
| P3      | 2     |

Quantum:

```text
Q = 2
```

---

# Gantt Chart

```text
0 2 4 6 8 10 12
|P1|P2|P3|P1|P2|P1|
```

---

# Why Round Robin is Fair?

Every process receives:

```text
Equal CPU Opportunity
```

No process can monopolize CPU.

---

# Response Time Advantage

Suppose:

```text
20 Processes
```

are waiting.

Under FCFS:

```text
Last Process
May Wait Long Time
```

Under RR:

```text
Every Process
Gets CPU Quickly
```

---

# Time Quantum

Most important concept in Round Robin.

---

# What Happens If Quantum Is Too Large?

Example:

```text
Q = 1000 ms
```

Processes:

```text
P1 = 20 ms

P2 = 10 ms

P3 = 5 ms
```

Each process finishes before quantum expires.

Behavior becomes:

```text
FCFS
```

---

# What Happens If Quantum Is Too Small?

Example:

```text
Q = 1 ms
```

Execution:

```text
P1
P2
P3
P1
P2
P3
...
```

Huge number of:

```text
Context Switches
```

occur.

---

# Optimal Quantum

Should be:

```text
Large Enough
To Reduce Overhead

Small Enough
For Good Response
```

---

# Quantum Comparison

| Quantum Size | Result                      |
| ------------ | --------------------------- |
| Very Large   | FCFS-like                   |
| Moderate     | Best Performance            |
| Very Small   | Excessive Context Switching |

---

# Context Switching

Round Robin generates many context switches.

---

# Example

```text
P1 Running
      ↓
Quantum Expires
      ↓
Save Context
      ↓
Run P2
```

---

# Cost

```text
Registers Saved

PCB Updated

Cache Effects

TLB Effects
```

---

# Starvation

Round Robin does:

```text
NOT
```

cause starvation.

---

# Why?

Every process eventually receives CPU time.

---

# Convoy Effect

FCFS:

```text
Convoy Effect
```

exists.

---

# Round Robin

```text
Convoy Effect
Largely Eliminated
```

because processes rotate.

---

# Advantages

### Fair Scheduling

All processes receive CPU.

---

### No Starvation

Every process gets a turn.

---

### Good Response Time

Ideal for interactive users.

---

### Time Sharing Support

Designed for multi-user systems.

---

# Disadvantages

### Context Switching Overhead

Can be high.

---

### Quantum Selection Difficult

Performance depends heavily on quantum.

---

### Higher Average Waiting Time

Compared to SJF/SRTF.

---

### Lower Throughput

Too many switches reduce efficiency.

---

# FCFS vs RR

| Feature          | FCFS           | RR         |
| ---------------- | -------------- | ---------- |
| Type             | Non-Preemptive | Preemptive |
| Fairness         | Low            | High       |
| Starvation       | No             | No         |
| Response Time    | Poor           | Good       |
| Context Switches | Low            | High       |

---

# SJF vs RR

| Feature       | SJF      | RR        |
| ------------- | -------- | --------- |
| Average WT    | Lower    | Higher    |
| Fairness      | Lower    | Higher    |
| Starvation    | Possible | No        |
| Response Time | Moderate | Excellent |

---

# Linux Perspective

Old UNIX systems used Round Robin extensively.

Modern Linux uses:

```text
CFS
(Completely Fair Scheduler)
```

However:

```text
Real-Time Linux Classes
```

still use RR concepts.

---

# Linux Real-Time Policies

```text
SCHED_FIFO

SCHED_RR
```

---

# RTOS Perspective

Most RTOS systems primarily use:

```text
Priority Scheduling
```

but may use:

```text
Round Robin
```

among tasks having:

```text
Same Priority
```

---

# Example

```text
Task A Priority 5

Task B Priority 5

Task C Priority 5
```

Scheduler rotates tasks.

---

# AUTOSAR Perspective

AUTOSAR OS primarily uses:

```text
Priority-Based Scheduling
```

but time-sharing concepts similar to RR can appear among tasks of equal priority depending on implementation.

---

# Real World Analogy

Imagine a classroom.

Teacher asks questions.

```text
Student A
      ↓
Student B
      ↓
Student C
      ↓
Student D
```

Everyone gets a chance before repeating.

This is Round Robin.

---

# Interview Questions

## Q1. What is Round Robin Scheduling?

A preemptive scheduling algorithm that allocates a fixed time quantum to each process.

---

## Q2. What data structure is used?

```text
Circular Queue
```

---

## Q3. What is Time Quantum?

Maximum CPU time allocated to a process before preemption.

---

## Q4. Is Round Robin Preemptive?

```text
Yes
```

---

## Q5. Can RR cause starvation?

```text
No
```

Every process gets CPU time.

---

## Q6. What happens if quantum is very large?

```text
Round Robin
Becomes FCFS
```

---

## Q7. What happens if quantum is very small?

```text
Too Many Context Switches
```

---

## Q8. Why is Round Robin suitable for interactive systems?

Because response time is good and every process gets CPU quickly.

---

# ⚠️ Common Interview Trap

Question:

```text
Is smaller quantum always better?
```

Answer:

```text
No.
```

Smaller quantum increases:

```text
Context Switching

Cache Misses

CPU Overhead
```

which can reduce performance.

---

# 📝 Quick Revision

```text
Round Robin
-----------
Preemptive

Uses
----
Time Quantum

Data Structure
--------------
Circular Queue

Advantages
----------
Fair
No Starvation
Good Response Time

Disadvantages
-------------
Context Switching Overhead
Quantum Selection Problem

Large Quantum
-------------
Behaves Like FCFS

Small Quantum
-------------
Too Many Context Switches

Linux
-----
SCHED_RR

Interview Keywords
------------------
Time Quantum
Circular Queue
Fairness
Response Time
```

---

# 🎯 Key Takeaway

Round Robin Scheduling is the most important time-sharing scheduling algorithm. By giving every process a fixed time quantum, it ensures fairness, prevents starvation, and provides excellent responsiveness.

The performance of Round Robin depends heavily on the choice of time quantum:

```text
Too Large → FCFS

Too Small → Excessive Context Switching
```

Understanding Round Robin is essential before learning:

* Priority Scheduling
* Multilevel Queue Scheduling
* Multilevel Feedback Queue (MLFQ)
* Linux CFS Scheduler
* RTOS Scheduling
* Real-Time Operating Systems
