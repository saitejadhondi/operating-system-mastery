# ⚡ Shortest Job First (SJF) Scheduling

> Shortest Job First (SJF) is one of the most important CPU scheduling algorithms in Operating Systems. It selects the process with the smallest CPU burst time for execution. SJF is famous because it provides the minimum average waiting time among all non-preemptive scheduling algorithms.

---

# 📌 Introduction

In FCFS Scheduling, a long process can delay many short processes.

Example:

```text
P1 = 20 ms

P2 = 2 ms

P3 = 1 ms
```

FCFS executes:

```text
P1 → P2 → P3
```

Result:

```text
Short jobs wait a long time.
```

To solve this problem:

```text
Shortest Job First (SJF)
```

was introduced.

---

# 🏛️ What is SJF Scheduling?

## Definition

SJF is a scheduling algorithm that selects the process with the smallest CPU burst time from the Ready Queue.

---

# Rule

```text
Smallest Burst Time
          ↓
Executed First
```

---

# Example

Processes:

| Process | Burst Time |
| ------- | ---------- |
| P1      | 8          |
| P2      | 4          |
| P3      | 2          |
| P4      | 1          |

Execution Order:

```text
P4 → P3 → P2 → P1
```

---

# Type of Scheduling

Classic SJF is:

```text
Non-Preemptive
```

Once a process gets CPU:

```text
Runs Until Completion
```

---

# SJF Scheduling Workflow

```text
Ready Queue
      │
      ▼
Find Smallest Burst Time
      │
      ▼
Execute Process
      │
      ▼
Remove From Queue
      │
      ▼
Repeat
```

---

# Why is SJF Important?

Among all Non-Preemptive Scheduling Algorithms:

```text
SJF Produces
Minimum Average Waiting Time
```

This is a very common interview question.

---

# Example 1

Processes:

| Process | Burst Time |
| ------- | ---------- |
| P1      | 6          |
| P2      | 8          |
| P3      | 7          |
| P4      | 3          |

Arrival Time:

```text
All Arrive At Time 0
```

---

# Step 1: Arrange By Burst Time

```text
P4 = 3

P1 = 6

P3 = 7

P2 = 8
```

---

# Step 2: Gantt Chart

```text
0      3      9      16      24
| P4 | P1 | P3 | P2 |
```

---

# Completion Time (CT)

| Process | CT |
| ------- | -- |
| P4      | 3  |
| P1      | 9  |
| P3      | 16 |
| P2      | 24 |

---

# Turnaround Time (TAT)

Formula:

```text
TAT = CT - AT
```

---

| Process | CT | AT | TAT |
| ------- | -- | -- | --- |
| P4      | 3  | 0  | 3   |
| P1      | 9  | 0  | 9   |
| P3      | 16 | 0  | 16  |
| P2      | 24 | 0  | 24  |

---

# Waiting Time (WT)

Formula:

```text
WT = TAT - BT
```

---

| Process | TAT | BT | WT |
| ------- | --- | -- | -- |
| P4      | 3   | 3  | 0  |
| P1      | 9   | 6  | 3  |
| P3      | 16  | 7  | 9  |
| P2      | 24  | 8  | 16 |

---

# Average Waiting Time

```text
(0 + 3 + 9 + 16)/4

= 7 ms
```

---

# Compare With FCFS

If FCFS order was:

```text
P1 → P2 → P3 → P4
```

Average Waiting Time:

```text
10.25 ms
```

---

# SJF Result

```text
7 ms
```

Better than FCFS.

---

# Example 2 (With Arrival Time)

Processes:

| Process | Arrival Time | Burst Time |
| ------- | ------------ | ---------- |
| P1      | 0            | 8          |
| P2      | 1            | 4          |
| P3      | 2            | 9          |
| P4      | 3            | 5          |

---

# Execution

At time:

```text
0
```

Only:

```text
P1
```

is available.

So:

```text
P1 Executes First
```

---

# Gantt Chart

```text
0        8       12      17       26
|   P1   |  P2  |  P4  |   P3   |
```

Notice:

After P1 finishes,

```text
P2
```

has the shortest burst time among available processes.

---

# Why SJF is Optimal?

Consider:

```text
Long Job
```

before

```text
Short Job
```

Short job waits unnecessarily.

If:

```text
Short Job
```

runs first,

total waiting time decreases.

---

# Mathematical Property

SJF is proven to produce:

```text
Minimum Average Waiting Time
```

among all non-preemptive scheduling algorithms.

---

# Response Time

Formula:

```text
RT = First CPU Start Time - Arrival Time
```

For Non-Preemptive SJF:

```text
Response Time
=
Waiting Time
```

---

# Starvation Problem

The biggest drawback of SJF.

---

# What is Starvation?

A process waits indefinitely because shorter processes keep arriving.

---

# Example

```text
Long Process = 100 ms
```

Ready Queue:

```text
2 ms

3 ms

1 ms

4 ms

2 ms
```

keep arriving.

Long process may never execute.

---

# Visual Representation

```text
Long Job
   ↓
Waiting

Short Job
Executes

Short Job
Executes

Short Job
Executes

...
```

---

# Why Does Starvation Occur?

SJF always prefers:

```text
Shortest Process
```

which may continuously postpone long jobs.

---

# Solution

Use:

```text
Aging
```

Priority increases over time.

Eventually:

```text
Long Job Executes
```

---

# Convoy Effect Comparison

## FCFS

```text
Long Job
      ↓
Short Jobs Wait
```

Convoy Effect occurs.

---

## SJF

```text
Short Jobs Execute First
```

Convoy Effect largely eliminated.

---

# Advantages of SJF

### Minimum Average Waiting Time

Best known non-preemptive algorithm.

---

### Better Throughput

More processes finish quickly.

---

### Better Resource Utilization

CPU spends less time waiting.

---

### Reduces Convoy Effect

Compared to FCFS.

---

# Disadvantages of SJF

### Starvation

Long jobs may wait indefinitely.

---

### Burst Time Prediction Needed

Operating System must know:

```text
CPU Burst Time
```

before scheduling.

---

### Difficult Practical Implementation

Exact burst time is usually unknown.

---

# How OS Estimates Burst Time?

Operating Systems use:

```text
Exponential Averaging
```

Formula:

Where:

```text
τ = Predicted Burst Time

t = Actual Burst Time

α = Weight Factor
```

---

# Complexity

If Ready Queue is sorted:

```text
O(log n)
```

selection possible.

Otherwise:

```text
O(n)
```

search required.

---

# Linux Perspective

Linux does not use pure SJF.

Why?

Because:

```text
Exact Burst Time
```

is unknown.

Instead Linux uses:

```text
CFS
(Completely Fair Scheduler)
```

which approximates fairness.

---

# RTOS Perspective

RTOS rarely uses SJF.

Reason:

```text
Deadline Predictability
```

is more important.

Most RTOS use:

```text
Priority Scheduling
```

---

# Automotive Perspective

Imagine:

```text
Airbag Task = 20 ms

Display Task = 1 ms
```

SJF would execute:

```text
Display Task First
```

which could be dangerous.

Therefore:

```text
SJF Not Suitable
```

for safety-critical systems.

---

# Real World Analogy

Supermarket Express Lane

Customers:

```text
Customer A = 20 Items

Customer B = 2 Items

Customer C = 1 Item
```

SJF serves:

```text
Customer C

Customer B

Customer A
```

This minimizes average waiting time.

---

# Interview Questions

## Q1. What is SJF Scheduling?

The process with the shortest CPU burst time executes first.

---

## Q2. Is SJF Preemptive?

Classic SJF is:

```text
Non-Preemptive
```

---

## Q3. What is the biggest advantage of SJF?

```text
Minimum Average Waiting Time
```

---

## Q4. What is the biggest disadvantage of SJF?

```text
Starvation
```

---

## Q5. Why is SJF difficult to implement?

Because actual burst time is generally unknown.

---

## Q6. Does SJF cause Convoy Effect?

Very little compared to FCFS.

---

## Q7. What is Aging?

A technique used to prevent starvation.

---

## Q8. Which algorithm is the preemptive version of SJF?

```text
SRTF
(Shortest Remaining Time First)
```

---

# ⚠️ Common Interview Trap

Question:

```text
Is SJF always better than FCFS?
```

Answer:

```text
For Average Waiting Time:
YES

For Fairness:
NO
```

SJF can cause starvation.

---

# Comparison

| Feature       | FCFS           | SJF            |
| ------------- | -------------- | -------------- |
| Type          | Non-Preemptive | Non-Preemptive |
| Average WT    | Higher         | Lower          |
| Convoy Effect | Yes            | Reduced        |
| Starvation    | No             | Yes            |
| Complexity    | Simple         | Higher         |

---

# 📝 Quick Revision

```text
SJF
---
Shortest Job First

Rule
----
Smallest Burst Time First

Type
----
Non-Preemptive

Advantage
---------
Minimum Average Waiting Time

Disadvantages
-------------
Starvation
Burst Time Prediction Required

Compared To FCFS
----------------
Lower Waiting Time
Better Throughput

Interview Keywords
------------------
Starvation
Aging
Minimum Average Waiting Time
```

---

# 🎯 Key Takeaway

SJF Scheduling selects the process with the smallest CPU burst time and is mathematically proven to minimize average waiting time among all non-preemptive scheduling algorithms.

However, it suffers from starvation and requires burst-time prediction, making it difficult to implement in real systems.

Understanding SJF is essential before learning:

* SRTF (Shortest Remaining Time First)
* Priority Scheduling
* Round Robin
* Multilevel Queue Scheduling
* Linux CFS Scheduler
