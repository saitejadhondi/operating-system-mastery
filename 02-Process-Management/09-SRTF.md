# ⚡ Shortest Remaining Time First (SRTF) Scheduling

> Shortest Remaining Time First (SRTF) is the preemptive version of Shortest Job First (SJF). Whenever a new process arrives with a shorter remaining burst time than the currently running process, the CPU is immediately preempted and assigned to the new process.

---

# 📌 Introduction

In SJF:

```text
Smallest Burst Time
        ↓
Selected Once
        ↓
Runs To Completion
```

Problem:

If a shorter process arrives later:

```text
Running Process Continues
```

even if a better choice exists.

To solve this:

```text
SRTF
(Shortest Remaining Time First)
```

was introduced.

---

# 🏛️ What is SRTF Scheduling?

## Definition

SRTF is a preemptive scheduling algorithm where the process with the shortest remaining execution time gets the CPU.

---

# Rule

```text
Smallest Remaining Time
          ↓
Gets CPU
```

---

# Key Difference

## SJF

```text
Burst Time Considered Once
```

---

## SRTF

```text
Remaining Time Considered Continuously
```

---

# Type of Scheduling

SRTF is:

```text
Preemptive
```

---

# Why Preemptive?

Suppose:

```text
P1 = 10 ms
```

is executing.

Then:

```text
P2 = 2 ms
```

arrives.

SRTF immediately switches to:

```text
P2
```

because:

```text
2 < Remaining Time Of P1
```

---

# Scheduling Workflow

```text
Process Arrives
       │
       ▼
Compare Remaining Times
       │
       ▼
Shortest Remaining Time?
       │
      Yes
       │
       ▼
Preempt Current Process
       │
       ▼
Execute New Process
```

---

# Example 1

Processes:

| Process | Arrival Time | Burst Time |
| ------- | ------------ | ---------- |
| P1      | 0            | 8          |
| P2      | 1            | 4          |
| P3      | 2            | 2          |
| P4      | 3            | 1          |

---

# Step 1

Time:

```text
0
```

Available:

```text
P1
```

Execute:

```text
P1
```

---

# Timeline

```text
0 → 1
```

Remaining:

```text
P1 = 7
```

---

# Step 2

Time:

```text
1
```

P2 arrives.

Remaining times:

```text
P1 = 7

P2 = 4
```

Choose:

```text
P2
```

Preemption occurs.

---

# Step 3

Time:

```text
2
```

P3 arrives.

Remaining:

```text
P2 = 3

P3 = 2
```

Choose:

```text
P3
```

Preemption occurs again.

---

# Step 4

Time:

```text
3
```

P4 arrives.

Remaining:

```text
P3 = 1

P4 = 1
```

Tie:

```text
Earlier Arrival Wins
```

Continue P3.

---

# Complete Gantt Chart

```text
0  1  2  4  5   8      15
|P1|P2|P3|P4|P2|   P1   |
```

---

# Completion Times

| Process | CT |
| ------- | -- |
| P3      | 4  |
| P4      | 5  |
| P2      | 8  |
| P1      | 15 |

---

# Turnaround Time

Formula:

```text
TAT = CT - AT
```

---

| Process | CT | AT | TAT |
| ------- | -- | -- | --- |
| P1      | 15 | 0  | 15  |
| P2      | 8  | 1  | 7   |
| P3      | 4  | 2  | 2   |
| P4      | 5  | 3  | 2   |

---

# Waiting Time

Formula:

```text
WT = TAT - BT
```

---

| Process | TAT | BT | WT |
| ------- | --- | -- | -- |
| P1      | 15  | 8  | 7  |
| P2      | 7   | 4  | 3  |
| P3      | 2   | 2  | 0  |
| P4      | 2   | 1  | 1  |

---

# Average Waiting Time

```text
(7 + 3 + 0 + 1) / 4

= 2.75 ms
```

---

# Compare With SJF

For same workload:

```text
SJF WT > SRTF WT
```

because SRTF reacts dynamically.

---

# Visual Representation

```text
Long Process Running
          │
          ▼
Short Process Arrives
          │
          ▼
Immediate CPU Switch
```

---

# Example 2

Processes:

| Process | AT | BT |
| ------- | -- | -- |
| P1      | 0  | 7  |
| P2      | 2  | 4  |
| P3      | 4  | 1  |

---

# Execution

Time:

```text
0 → 2
```

Run:

```text
P1
```

Remaining:

```text
5
```

---

P2 arrives:

```text
P2 = 4

P1 = 5
```

Switch to:

```text
P2
```

---

At:

```text
4
```

P3 arrives:

```text
P3 = 1

P2 = 2
```

Switch to:

```text
P3
```

---

# Gantt Chart

```text
0    2    4   5    7      12
| P1 | P2 |P3| P2 |  P1  |
```

---

# Why SRTF Works Better?

SRTF minimizes:

```text
Average Waiting Time
```

and

```text
Average Turnaround Time
```

by always selecting the shortest remaining work.

---

# Mathematical Property

SRTF is optimal for:

```text
Minimum Average Waiting Time
```

among preemptive scheduling algorithms.

---

# Response Time

Formula:

```text
RT =
First CPU Allocation
-
Arrival Time
```

---

Example:

```text
P2 arrives at 1

Starts at 1
```

Response Time:

```text
0
```

---

# Context Switching Overhead

Major drawback.

---

# Why?

Each preemption causes:

```text
Save Registers

Save Program Counter

Load New Context

Update PCB
```

---

# Example

```text
P1 Running

P2 Arrives

Switch

P3 Arrives

Switch

P4 Arrives

Switch
```

Many context switches occur.

---

# Starvation Problem

Same as SJF.

---

# Scenario

```text
Long Process = 100 ms
```

Continuous arrival of:

```text
1 ms

2 ms

3 ms
```

jobs.

Long process may wait indefinitely.

---

# Example

```text
Long Job Waiting

Short Job Arrives

Short Job Executes

Another Short Job Arrives

Again Executes
```

Long job keeps waiting.

---

# Solution

Use:

```text
Aging
```

Priority gradually increases.

Eventually:

```text
Long Process Runs
```

---

# Advantages

### Minimum Average Waiting Time

Best among practical CPU scheduling methods.

---

### Excellent Response Time

Short jobs get CPU quickly.

---

### Better Throughput

More processes finish earlier.

---

### Suitable For Interactive Systems

Provides responsiveness.

---

# Disadvantages

### Context Switching Overhead

Frequent preemption.

---

### Starvation

Long processes may suffer.

---

### Burst Time Prediction Required

OS must estimate CPU burst.

---

### Complex Implementation

More difficult than FCFS or SJF.

---

# SJF vs SRTF

| Feature               | SJF            | SRTF       |
| --------------------- | -------------- | ---------- |
| Type                  | Non-Preemptive | Preemptive |
| CPU Can Be Taken Away | No             | Yes        |
| Context Switches      | Fewer          | More       |
| Average WT            | Lower          | Even Lower |
| Complexity            | Lower          | Higher     |
| Responsiveness        | Moderate       | Better     |

---

# FCFS vs SJF vs SRTF

| Feature          | FCFS           | SJF            | SRTF       |
| ---------------- | -------------- | -------------- | ---------- |
| Type             | Non-Preemptive | Non-Preemptive | Preemptive |
| Convoy Effect    | Yes            | Reduced        | No         |
| Starvation       | No             | Yes            | Yes        |
| Avg Waiting Time | High           | Lower          | Lowest     |
| Response Time    | Poor           | Better         | Best       |

---

# Linux Perspective

Linux does not implement pure SRTF.

Reason:

```text
Exact Burst Times
Are Unknown
```

Linux instead uses:

```text
CFS
Completely Fair Scheduler
```

which approximates fairness.

---

# RTOS Perspective

RTOS generally prefers:

```text
Priority Scheduling
```

rather than SRTF.

---

# Why?

Real-time systems care about:

```text
Deadlines

Priority

Deterministic Behavior
```

not shortest execution time.

---

# AUTOSAR Perspective

AUTOSAR OS does not use SRTF.

Instead it uses:

```text
Priority-Based Scheduling
```

with:

```text
Preemptive Tasks

Non-Preemptive Tasks
```

---

# Real World Analogy

Supermarket Express Counter

```text
Customer A = 20 Items
```

Currently billing.

Suddenly:

```text
Customer B = 1 Item
```

arrives.

Cashier immediately serves B first.

This resembles SRTF.

---

# Interview Questions

## Q1. What is SRTF?

Shortest Remaining Time First is the preemptive version of SJF.

---

## Q2. What causes preemption in SRTF?

Arrival of a process with shorter remaining burst time.

---

## Q3. What is the biggest advantage of SRTF?

```text
Minimum Average Waiting Time
```

---

## Q4. What is the biggest disadvantage?

```text
Starvation
```

and

```text
Context Switching Overhead
```

---

## Q5. Is SRTF Preemptive?

```text
Yes
```

---

## Q6. Which is better?

```text
SJF or SRTF?
```

For waiting time:

```text
SRTF
```

For simplicity:

```text
SJF
```

---

## Q7. Can SRTF cause starvation?

Yes.

Long processes may never get CPU.

---

## Q8. What is the difference between Burst Time and Remaining Time?

```text
Burst Time
----------
Original CPU Requirement

Remaining Time
--------------
CPU Time Still Needed
```

---

# ⚠️ Common Interview Trap

Question:

```text
Does SRTF always improve performance?
```

Answer:

```text
No.
```

Too many preemptions can increase:

```text
Context Switching

Cache Misses

TLB Misses
```

which may reduce actual performance.

---

# 📝 Quick Revision

```text
SRTF
----
Shortest Remaining Time First

Type
----
Preemptive

Rule
----
Shortest Remaining Time Executes

Advantages
----------
Lowest Average Waiting Time
Good Response Time

Disadvantages
-------------
Starvation
Context Switching Overhead

Triggers
--------
Shorter Process Arrival

Compared To SJF
---------------
More Responsive
More Context Switches

Interview Keywords
------------------
Preemption
Starvation
Minimum Waiting Time
Context Switching
```

---

# 🎯 Key Takeaway

SRTF is the preemptive version of SJF that always executes the process with the shortest remaining CPU time.

It provides excellent responsiveness and minimizes average waiting time, but introduces context-switching overhead and can cause starvation for long-running processes.

Understanding SRTF is essential before learning:

* Priority Scheduling
* Round Robin
* Multilevel Queue Scheduling
* Multilevel Feedback Queue
* Linux CFS Scheduler
* RTOS Scheduling
