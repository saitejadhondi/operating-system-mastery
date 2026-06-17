# ⚖️ Highest Response Ratio Next (HRRN) Scheduling

> Highest Response Ratio Next (HRRN) is a non-preemptive CPU scheduling algorithm designed to overcome the starvation problem of SJF while still providing low average waiting time. HRRN selects the process with the highest response ratio rather than simply choosing the shortest job.

---

# 📌 Introduction

We learned:

```text
FCFS
-----
No Starvation
Poor Waiting Time

SJF
----
Minimum Waiting Time
Can Cause Starvation
```

Problem:

```text
Long Processes
Can Wait Forever
```

in SJF.

To solve this problem:

```text
HRRN
(Highest Response Ratio Next)
```

was introduced.

---

# 🏛️ What is HRRN?

## Definition

HRRN selects the process with the highest response ratio for execution.

Instead of selecting:

```text
Shortest Job
```

it selects:

```text
Highest Response Ratio
```

---

# Response Ratio Formula

Formula:

Where:

```text
RR = Response Ratio

WT = Waiting Time

BT = Burst Time
```

---

# Alternative Form

```text
RR = 1 + (WT / BT)
```

---

# Key Idea

As waiting time increases:

```text
Response Ratio Increases
```

Eventually:

```text
Long Processes
Get CPU
```

This prevents starvation.

---

# Why HRRN Was Introduced?

Consider SJF:

| Process | Burst Time |
| ------- | ---------- |
| P1      | 100        |
| P2      | 2          |
| P3      | 1          |
| P4      | 2          |

SJF executes:

```text
P3 → P2 → P4 → P1
```

If short jobs keep arriving:

```text
P1
```

may wait forever.

---

# HRRN Solution

Waiting time contributes to priority.

The longer a process waits:

```text
Higher Response Ratio
```

it receives.

---

# Characteristics

✅ No Starvation

✅ Better Fairness

✅ Lower Waiting Time

✅ Considers Waiting Time

❌ More Calculations

❌ Non-Preemptive

---

# Type of Scheduling

HRRN is:

```text
Non-Preemptive
```

Once selected:

```text
Process Runs Until Completion
```

---

# Scheduling Workflow

```text
Ready Queue
      │
      ▼
Calculate Response Ratio
      │
      ▼
Select Highest Ratio
      │
      ▼
Execute Process
      │
      ▼
Recalculate Ratios
```

---

# Example 1

Processes:

| Process | Arrival | Burst |
| ------- | ------- | ----- |
| P1      | 0       | 8     |
| P2      | 1       | 4     |
| P3      | 2       | 2     |

---

# Step 1

Time:

```text
0
```

Only:

```text
P1
```

available.

Execute:

```text
P1
```

---

# Gantt Chart

```text
0            8
|     P1     |
```

---

# Step 2

At Time 8

Available:

```text
P2
P3
```

---

# Calculate Response Ratio

## P2

```text
WT = 8 - 1 = 7

BT = 4
```

Response Ratio:

```text
RR = (7 + 4)/4

= 2.75
```

---

## P3

```text
WT = 8 - 2 = 6

BT = 2
```

Response Ratio:

```text
RR = (6 + 2)/2

= 4
```

---

# Selection

```text
P3
```

because:

```text
4 > 2.75
```

---

# Gantt Chart

```text
0          8      10
|    P1    | P3 |
```

---

# Step 3

Remaining:

```text
P2
```

Execute.

---

# Final Gantt Chart

```text
0          8      10      14
|    P1    | P3 |  P2  |
```

---

# Completion Time

| Process | CT |
| ------- | -- |
| P1      | 8  |
| P3      | 10 |
| P2      | 14 |

---

# Turnaround Time

Formula:

```text
TAT = CT - AT
```

---

| Process | CT | AT | TAT |
| ------- | -- | -- | --- |
| P1      | 8  | 0  | 8   |
| P2      | 14 | 1  | 13  |
| P3      | 10 | 2  | 8   |

---

# Waiting Time

Formula:

```text
WT = TAT - BT
```

---

| Process | TAT | BT | WT |
| ------- | --- | -- | -- |
| P1      | 8   | 8  | 0  |
| P2      | 13  | 4  | 9  |
| P3      | 8   | 2  | 6  |

---

# Average Waiting Time

```text
(0 + 9 + 6) / 3

= 5 ms
```

---

# Example 2

At Time 10

Processes:

| Process | BT | WT |
| ------- | -- | -- |
| P1      | 10 | 20 |
| P2      | 5  | 5  |
| P3      | 2  | 2  |

---

# Calculate Ratios

## P1

```text
RR = (20 + 10)/10

= 3
```

---

## P2

```text
RR = (5 + 5)/5

= 2
```

---

## P3

```text
RR = (2 + 2)/2

= 2
```

---

# Selection

```text
P1
```

because:

```text
3
```

is highest.

Notice:

```text
Long Process Gets Chance
```

This prevents starvation.

---

# Why HRRN Prevents Starvation?

Consider:

```text
Long Job
```

waiting for a long time.

As:

```text
WT ↑
```

then:

```text
RR ↑
```

Eventually:

```text
Response Ratio Becomes Highest
```

and process gets CPU.

---

# Visual Representation

```text
Waiting Time
      │
      ▼
Response Ratio Increases
      │
      ▼
Priority Increases
      │
      ▼
Process Executes
```

---

# Comparison With SJF

## SJF

Selection Based On:

```text
Burst Time Only
```

---

## HRRN

Selection Based On:

```text
Burst Time
+
Waiting Time
```

---

# Example

Processes:

| Process   | BT |
| --------- | -- |
| Long Job  | 20 |
| Short Job | 2  |

---

# SJF

```text
Short Job Always Wins
```

---

# HRRN

After enough waiting:

```text
Long Job Wins
```

---

# Advantages

### Prevents Starvation

Biggest benefit.

---

### Better Fairness

Waiting processes gain priority.

---

### Good Average Waiting Time

Close to SJF performance.

---

### Suitable For Batch Systems

Widely discussed in classical OS scheduling.

---

# Disadvantages

### Response Ratio Calculation

Requires recomputation.

---

### Non-Preemptive

Cannot interrupt running process.

---

### Not Ideal For Interactive Systems

Round Robin performs better.

---

### More Complex Than FCFS

Needs continuous ratio evaluation.

---

# Comparison

| Feature    | FCFS           | SJF            | HRRN           |
| ---------- | -------------- | -------------- | -------------- |
| Starvation | No             | Yes            | No             |
| Avg WT     | High           | Lowest         | Low            |
| Fairness   | Medium         | Poor           | Good           |
| Complexity | Low            | Medium         | Higher         |
| Type       | Non-Preemptive | Non-Preemptive | Non-Preemptive |

---

# SJF vs HRRN

| Feature         | SJF        | HRRN            |
| --------------- | ---------- | --------------- |
| Selection Basis | Burst Time | Response Ratio  |
| Starvation      | Possible   | Prevented       |
| Waiting Time    | Lower      | Slightly Higher |
| Fairness        | Lower      | Better          |

---

# Linux Perspective

Linux does not use HRRN.

Reason:

```text
Response Ratio Calculation
```

is expensive for large systems.

Linux uses:

```text
CFS
(Completely Fair Scheduler)
```

instead.

---

# RTOS Perspective

RTOS does not use HRRN.

RTOS focuses on:

```text
Priority

Deadlines

Determinism
```

---

# AUTOSAR Perspective

AUTOSAR OS uses:

```text
Priority-Based Scheduling
```

not HRRN.

Safety-critical systems require:

```text
Predictable Execution
```

rather than response ratio calculations.

---

# Real World Analogy

Bank Queue

Customers:

```text
Customer A
20 Transactions

Customer B
2 Transactions
```

SJF always favors:

```text
Customer B
```

HRRN says:

```text
Customer A Has Waited Long Enough
```

and eventually serves A.

---

# Interview Questions

## Q1. What is HRRN?

Highest Response Ratio Next scheduling algorithm.

---

## Q2. Why was HRRN introduced?

To eliminate starvation in SJF.

---

## Q3. Is HRRN Preemptive?

```text
No
```

It is Non-Preemptive.

---

## Q4. What is the Response Ratio Formula?

Response Ratio:

---

## Q5. What happens if waiting time increases?

```text
Response Ratio Increases
```

---

## Q6. Does HRRN cause starvation?

```text
No
```

---

## Q7. Which is more fair?

```text
HRRN
```

compared to SJF.

---

## Q8. What is the biggest advantage of HRRN?

```text
Prevents Starvation
```

while maintaining low average waiting time.

---

# ⚠️ Common Interview Trap

Question:

```text
Does HRRN always choose the shortest process?
```

Answer:

```text
No.
```

It chooses:

```text
Highest Response Ratio
```

which depends on both:

```text
Burst Time

Waiting Time
```

---

# 📝 Quick Revision

```text
HRRN
----
Highest Response Ratio Next

Formula
-------
RR = (WT + BT)/BT

Type
----
Non-Preemptive

Advantages
----------
No Starvation
Fair
Low Waiting Time

Disadvantages
-------------
More Calculations
Non-Preemptive

Compared To SJF
---------------
More Fair
Prevents Starvation

Interview Keywords
------------------
Response Ratio
Waiting Time
Starvation Prevention
Fair Scheduling
```

---

# 🎯 Key Takeaway

HRRN improves upon SJF by considering both burst time and waiting time. As a process waits longer, its response ratio increases, ensuring that long-running processes eventually receive CPU time.

This makes HRRN one of the best classical scheduling algorithms for balancing:

* Low Waiting Time
* Fairness
* Starvation Prevention

Understanding HRRN helps build intuition before learning:

* Priority Scheduling
* Round Robin
* Multilevel Queue Scheduling
* Multilevel Feedback Queue Scheduling
* Linux CFS Scheduler
