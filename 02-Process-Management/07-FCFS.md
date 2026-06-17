# 🥇 First Come First Serve (FCFS) Scheduling

> First Come First Serve (FCFS) is the simplest CPU scheduling algorithm. Processes are executed in the order they arrive in the Ready Queue. FCFS is easy to implement and serves as the foundation for understanding more advanced scheduling algorithms.

---

# 📌 Introduction

Imagine standing in a ticket counter queue.

```text
Person A Arrives First

Person B Arrives Second

Person C Arrives Third
```

Who gets service first?

```text
Person A
```

This is exactly how FCFS scheduling works.

---

# 🏛️ What is FCFS Scheduling?

## Definition

FCFS (First Come First Serve) is a scheduling algorithm in which the process that arrives first gets the CPU first.

---

# Rule

```text
First Arrived
      ↓
First Executed
```

---

# Queue Structure

FCFS uses:

```text
FIFO Queue

(First In First Out)
```

---

# Example

Arrival Order:

```text
P1

P2

P3

P4
```

Execution Order:

```text
P1

P2

P3

P4
```

---

# Characteristics

✅ Simple

✅ Fair Arrival Order

✅ Easy To Implement

❌ Poor Average Waiting Time

❌ Convoy Effect

❌ Not Suitable For Interactive Systems

---

# Type of Scheduling

FCFS is:

```text
Non-Preemptive
```

Once a process gets CPU:

```text
Runs Until Completion
```

or

```text
Blocks For I/O
```

---

# FCFS Scheduling Workflow

```text
Process Arrives
       │
       ▼
Ready Queue
       │
       ▼
CPU Executes
       │
       ▼
Process Finishes
```

---

# Example 1

Processes:

| Process | Burst Time |
| ------- | ---------- |
| P1      | 5          |
| P2      | 3          |
| P3      | 2          |

Arrival Time:

```text
All Arrive At Time 0
```

---

# Step 1: Build Gantt Chart

```text
0      5      8     10
| P1 | P2 | P3 |
```

Execution Order:

```text
P1 → P2 → P3
```

---

# Completion Time (CT)

Completion Time = Time when process finishes.

| Process | Completion Time |
| ------- | --------------- |
| P1      | 5               |
| P2      | 8               |
| P3      | 10              |

---

# Turnaround Time (TAT)

Formula:

```text
TAT = Completion Time - Arrival Time
```

---

| Process | CT | AT | TAT |
| ------- | -- | -- | --- |
| P1      | 5  | 0  | 5   |
| P2      | 8  | 0  | 8   |
| P3      | 10 | 0  | 10  |

---

# Waiting Time (WT)

Formula:

```text
WT = Turnaround Time - Burst Time
```

---

| Process | TAT | BT | WT |
| ------- | --- | -- | -- |
| P1      | 5   | 5  | 0  |
| P2      | 8   | 3  | 5  |
| P3      | 10  | 2  | 8  |

---

# Average Waiting Time

Formula:

```text
Average WT =
(WT1 + WT2 + WT3)
/ Number Of Processes
```

Calculation:

```text
(0 + 5 + 8) / 3

= 4.33 ms
```

---

# Average Turnaround Time

Formula:

```text
Average TAT =
(TAT1 + TAT2 + TAT3)
/ Number Of Processes
```

Calculation:

```text
(5 + 8 + 10)/3

= 7.67 ms
```

---

# Example 2 (Different Arrival Times)

Processes:

| Process | Arrival Time | Burst Time |
| ------- | ------------ | ---------- |
| P1      | 0            | 6          |
| P2      | 2            | 4          |
| P3      | 4            | 2          |

---

# Gantt Chart

```text
0        6       10      12
|   P1   |  P2   |  P3  |
```

Even though:

```text
P2 Arrives At 2

P3 Arrives At 4
```

they must wait because FCFS is non-preemptive.

---

# Waiting Time Calculation

## P1

```text
WT = 0
```

---

## P2

```text
WT = 6 - 2

= 4
```

---

## P3

```text
WT = 10 - 4

= 6
```

---

# Average Waiting Time

```text
(0 + 4 + 6)/3

= 3.33
```

---

# Response Time

## Definition

Time from arrival until first CPU allocation.

Formula:

```text
Response Time =
First CPU Start Time
-
Arrival Time
```

---

# FCFS Property

For FCFS:

```text
Response Time
=
Waiting Time
```

because process starts only once.

---

# Convoy Effect

One of the biggest disadvantages of FCFS.

---

# What is Convoy Effect?

A long CPU-bound process delays all short processes behind it.

---

# Example

| Process | Burst Time |
| ------- | ---------- |
| P1      | 50         |
| P2      | 2          |
| P3      | 1          |

---

# Gantt Chart

```text
0                         50 52 53
|-----------P1-----------|P2|P3|
```

---

# Waiting Time

```text
P2 waits 50 ms

P3 waits 52 ms
```

even though they are tiny processes.

---

# Why Bad?

```text
Short Processes Suffer

Response Time Increases

User Experience Degrades
```

---

# Visual Representation

```text
Long Job
████████████████████████████

Short Job
██

Short Job
█
```

All short jobs wait behind long job.

---

# Advantages of FCFS

### Simple

Easy implementation using queue.

---

### No Starvation

Every process eventually executes.

---

### Low Overhead

Minimal scheduling complexity.

---

### Predictable

Execution order known beforehand.

---

# Disadvantages of FCFS

### Convoy Effect

Major drawback.

---

### Poor Response Time

Interactive users wait longer.

---

### Not Suitable For Time Sharing

Modern systems need quick response.

---

### Higher Average Waiting Time

Compared with SJF.

---

# Complexity

Insertion:

```text
O(1)
```

Removal:

```text
O(1)
```

Implementation is extremely simple.

---

# Linux Perspective

Modern Linux:

```text
Does NOT Use FCFS
```

for normal process scheduling.

Why?

Because FCFS causes:

```text
Poor Responsiveness
```

---

# RTOS Perspective

Pure FCFS is rarely used.

RTOS typically uses:

```text
Priority-Based Scheduling
```

---

# Automotive Perspective

Imagine:

```text
Airbag Task

Engine Monitoring Task
```

Using FCFS:

```text
Engine Task Runs First
```

Airbag may wait.

This is unacceptable.

Therefore:

```text
FCFS Not Suitable
```

for safety-critical systems.

---

# Real World Analogy

Bank Queue

```text
Customer A Arrives First
```

Must finish before:

```text
Customer B
```

gets service.

---

# Interview Questions

## Q1. What is FCFS Scheduling?

Processes execute in arrival order.

---

## Q2. Is FCFS Preemptive?

No.

FCFS is Non-Preemptive.

---

## Q3. Which Data Structure is Used?

FIFO Queue.

---

## Q4. What is Convoy Effect?

A long process delays many short processes.

---

## Q5. Does FCFS Cause Starvation?

No.

Every process eventually gets CPU.

---

## Q6. What is the Main Advantage?

Simple implementation.

---

## Q7. What is the Main Disadvantage?

Convoy Effect.

---

## Q8. Why is FCFS not used in modern OS scheduling?

Because it provides poor responsiveness.

---

# ⚠️ Common Interview Trap

Question:

```text
Can FCFS produce optimal waiting time?
```

Answer:

```text
No.
```

FCFS often produces higher average waiting time than SJF.

---

# Comparison With Future Algorithms

| Algorithm   | Average WT | Response Time |
| ----------- | ---------- | ------------- |
| FCFS        | Higher     | Poor          |
| SJF         | Lower      | Better        |
| SRTF        | Lower      | Better        |
| Round Robin | Good       | Excellent     |

---

# 📝 Quick Revision

```text
FCFS
-----
First Come First Serve

Type
----
Non-Preemptive

Data Structure
--------------
FIFO Queue

Advantages
----------
Simple
Fair
No Starvation

Disadvantages
-------------
Convoy Effect
Poor Response Time

Formulas
--------
TAT = CT - AT

WT = TAT - BT

RT = First Start Time - AT

Interview Keyword
-----------------
Convoy Effect
```

---

# 🎯 Key Takeaway

FCFS is the simplest scheduling algorithm where processes execute in the order they arrive. While easy to implement and starvation-free, FCFS suffers from the Convoy Effect and poor response times, making it unsuitable for modern interactive operating systems.

Understanding FCFS is essential before learning:

* SJF (Shortest Job First)
* SRTF (Shortest Remaining Time First)
* Priority Scheduling
* Round Robin
* Multilevel Queue Scheduling
* Linux CFS Scheduler
