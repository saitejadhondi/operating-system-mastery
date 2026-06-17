# 🎯 Priority Scheduling

> Priority Scheduling is one of the most important CPU scheduling algorithms in Operating Systems. Every process is assigned a priority, and the CPU is allocated to the process with the highest priority. This algorithm forms the foundation of RTOS, AUTOSAR OS, Embedded Systems, and Real-Time Scheduling.

---

# 📌 Introduction

Consider an automotive system:

```text id="j8a1de"
Airbag Deployment Task

Engine Monitoring Task

Display Update Task

Music Player Task
```

Should all tasks be treated equally?

```text id="lf0s3y"
NO
```

An Airbag task is far more important than updating a music display.

This is where:

```text id="q3tm4w"
Priority Scheduling
```

comes into play.

---

# 🏛️ What is Priority Scheduling?

## Definition

Priority Scheduling is a CPU scheduling algorithm where the process with the highest priority gets the CPU first.

---

# Rule

```text id="m7h5rj"
Higher Priority
       ↓
Execute First
```

---

# Example

| Process | Priority |
| ------- | -------- |
| P1      | 3        |
| P2      | 1        |
| P3      | 5        |
| P4      | 2        |

Assume:

```text id="s8kt9r"
Larger Number
=
Higher Priority
```

Execution Order:

```text id="cbfdr0"
P3 → P1 → P4 → P2
```

---

# Priority Representation

Two conventions exist.

---

# Convention 1

```text id="pkgh17"
Higher Number
=
Higher Priority
```

Example:

```text id="cy3yo0"
10 > 5
```

---

# Convention 2

```text id="n7yx91"
Lower Number
=
Higher Priority
```

Example:

```text id="j6y4gs"
1 > 5
```

Used by many operating systems.

---

# Interview Tip

Always ask:

```text id="k26d0w"
Which Convention Is Being Used?
```

before solving problems.

---

# Types of Priority Scheduling

Priority Scheduling can be:

```text id="mdu61p"
Non-Preemptive
```

or

```text id="uvh0bi"
Preemptive
```

---

# 1️⃣ Non-Preemptive Priority Scheduling

Once a process gets CPU:

```text id="jlwmx8"
Runs Until Completion
```

even if a higher-priority process arrives.

---

# Example

P1 starts execution.

While running:

```text id="qnkq2g"
P2
Priority = Higher
```

arrives.

P1 continues.

No interruption occurs.

---

# 2️⃣ Preemptive Priority Scheduling

If a higher-priority process arrives:

```text id="uq5g4u"
Current Process Stopped
```

and CPU immediately switches.

---

# Example

```text id="ok4hmk"
P1 Running
Priority = 2
```

Suddenly:

```text id="d6gsl3"
P2 Arrives
Priority = 10
```

CPU immediately executes:

```text id="n1vdv6"
P2
```

---

# Scheduling Workflow

```text id="dz7j9p"
Ready Queue
      │
      ▼
Find Highest Priority
      │
      ▼
Allocate CPU
      │
      ▼
Process Completes
```

---

# Example 1 (Non-Preemptive)

Processes:

| Process | Burst | Priority |
| ------- | ----- | -------- |
| P1      | 10    | 3        |
| P2      | 1     | 1        |
| P3      | 2     | 4        |
| P4      | 1     | 5        |

Assume:

```text id="aaxwy5"
Higher Number
=
Higher Priority
```

---

# Execution Order

```text id="gz7k8g"
P4 → P3 → P1 → P2
```

---

# Gantt Chart

```text id="cr5vlc"
0   1    3      13      14
|P4| P3 |  P1  |  P2  |
```

---

# Waiting Time

| Process | WT |
| ------- | -- |
| P4      | 0  |
| P3      | 1  |
| P1      | 3  |
| P2      | 13 |

---

# Average Waiting Time

```text id="kifc0s"
(0 + 1 + 3 + 13)/4

= 4.25
```

---

# Example 2 (Preemptive)

Processes:

| Process | AT | BT | Priority |
| ------- | -- | -- | -------- |
| P1      | 0  | 8  | 2        |
| P2      | 2  | 4  | 5        |

Assume:

```text id="okc2ie"
Higher Number
=
Higher Priority
```

---

# Timeline

Time:

```text id="sryjlwm"
0
```

Execute:

```text id="pqcgkr"
P1
```

---

At:

```text id="s8yxii"
2
```

P2 arrives.

Priority:

```text id="fz2f8z"
P1 = 2

P2 = 5
```

---

# Preemption Occurs

```text id="kn8fx2"
P1 Stopped

P2 Starts
```

---

# Gantt Chart

```text id="lkgzyv"
0     2      6        12
| P1 |  P2  |   P1   |
```

---

# Completion Times

| Process | CT |
| ------- | -- |
| P2      | 6  |
| P1      | 12 |

---

# Why Priority Scheduling?

Some tasks are more important than others.

Example:

```text id="qg2iyq"
Emergency Task

Normal Task

Background Task
```

Emergency task must execute first.

---

# Starvation Problem

The biggest drawback.

---

# What is Starvation?

A low-priority process waits indefinitely because higher-priority processes continuously arrive.

---

# Example

```text id="m6tncq"
P1 Priority = 1
```

waiting.

Continuously arriving:

```text id="91zh6n"
P2 Priority = 10

P3 Priority = 9

P4 Priority = 8
```

---

# Result

```text id="eytffy"
P1 Never Executes
```

---

# Visual Representation

```text id="z6a4nj"
Low Priority Task
        │
        ▼
Waiting

High Priority Task
Executes

High Priority Task
Executes

High Priority Task
Executes
```

---

# Solution: Aging

Most important interview concept.

---

# What is Aging?

Gradually increasing priority of waiting processes.

---

# Example

Initially:

```text id="9jlwmk"
Priority = 1
```

After waiting:

```text id="fr6kk4"
Priority = 2

Priority = 3

Priority = 4

...
```

Eventually:

```text id="vut9z1"
Process Gets CPU
```

---

# Priority Inversion

Extremely important for RTOS interviews.

---

# What is Priority Inversion?

A high-priority task waits for a resource held by a low-priority task.

---

# Example

```text id="gnnsg6"
High Priority Task
      │
      ▼
Needs Mutex
      │
      ▼
Mutex Held By
Low Priority Task
```

---

# Problem

High-priority task becomes blocked.

---

# Real Example

```text id="e9gluv"
Airbag Task
```

waiting for:

```text id="zz3gct"
Engine Logging Task
```

This is dangerous.

---

# Solution

```text id="3m3z4x"
Priority Inheritance
```

---

# Priority Inheritance

Low-priority task temporarily receives:

```text id="um0g4v"
High Priority
```

until resource released.

---

# Advantages

### Simple Concept

Easy implementation.

---

### Supports Critical Tasks

Important tasks execute first.

---

### Real-Time Friendly

Widely used in RTOS.

---

### Flexible

Priority can be static or dynamic.

---

# Disadvantages

### Starvation

Major issue.

---

### Priority Inversion

Requires additional mechanisms.

---

### Unfairness

Low-priority tasks may suffer.

---

### Complex Tuning

Choosing priorities is difficult.

---

# Priority Types

## Static Priority

Assigned once.

Never changes.

Example:

```text id="yzh3pi"
Airbag = 10

Display = 2
```

---

## Dynamic Priority

Can change over time.

Example:

```text id="o9c0h6"
Linux Scheduler
```

adjusts priorities dynamically.

---

# FCFS vs Priority

| Feature               | FCFS          | Priority |
| --------------------- | ------------- | -------- |
| Selection             | Arrival Order | Priority |
| Starvation            | No            | Yes      |
| Response Time         | Poor          | Better   |
| Critical Task Support | No            | Yes      |

---

# RR vs Priority

| Feature                | RR      | Priority  |
| ---------------------- | ------- | --------- |
| Fairness               | High    | Lower     |
| Critical Task Handling | Poor    | Excellent |
| Starvation             | No      | Possible  |
| RTOS Usage             | Limited | Extensive |

---

# Linux Perspective

Linux uses priorities extensively.

---

# Linux Nice Values

```bash id="vk9x2o"
nice -n 10 process
```

Priority range:

```text id="a1m7zc"
-20 → Highest Priority

19 → Lowest Priority
```

---

# Check Priority

```bash id="cc6rwe"
top
```

or

```bash id="zhs1wr"
ps -el
```

---

# RTOS Perspective

Most RTOS systems use:

```text id="pbp9pq"
Priority-Based Preemptive Scheduling
```

---

# Example

FreeRTOS:

```text id="5ebbn9"
Task A Priority = 1

Task B Priority = 5
```

Task B executes first.

---

# AUTOSAR Perspective

AUTOSAR OS is heavily based on:

```text id="ojicj7"
Priority Scheduling
```

---

# AUTOSAR Task Types

```text id="oldu7q"
Basic Tasks

Extended Tasks
```

assigned priorities.

---

# Automotive Example

```text id="sftpb5"
Airbag Task
Priority = Highest

Engine Task
Priority = Medium

Display Task
Priority = Low
```

Airbag always executes first.

---

# Real World Analogy

Hospital Emergency Room

Patients:

```text id="p0t2p2"
Critical Patient

Normal Patient

Routine Checkup
```

Doctor treats:

```text id="w1ljm5"
Critical Patient First
```

This is Priority Scheduling.

---

# Interview Questions

## Q1. What is Priority Scheduling?

CPU allocated to highest-priority process.

---

## Q2. Is Priority Scheduling Preemptive?

Can be:

```text id="spns7f"
Preemptive
or
Non-Preemptive
```

---

## Q3. Biggest Advantage?

```text id="a18llx"
Supports Critical Tasks
```

---

## Q4. Biggest Disadvantage?

```text id="9vpp8m"
Starvation
```

---

## Q5. What is Aging?

A technique that gradually increases priority of waiting processes.

---

## Q6. What is Priority Inversion?

High-priority task waiting for low-priority task.

---

## Q7. Solution for Priority Inversion?

```text id="8ngn6k"
Priority Inheritance
```

---

## Q8. Which scheduling algorithm is used in RTOS?

```text id="ujv6mw"
Priority-Based Scheduling
```

---

# ⚠️ Common Interview Trap

Question:

```text id="cruujj"
Does highest priority always mean highest number?
```

Answer:

```text id="6a6piz"
No.
```

Depends on implementation.

Always verify convention.

---

# 📝 Quick Revision

```text id="8r4bgm"
Priority Scheduling
-------------------
CPU Given To Highest Priority

Types
-----
Preemptive
Non-Preemptive

Advantages
----------
Supports Critical Tasks
RTOS Friendly

Disadvantages
-------------
Starvation
Priority Inversion

Solutions
---------
Aging
Priority Inheritance

RTOS
----
Priority-Based

AUTOSAR
--------
Priority-Based

Interview Keywords
------------------
Starvation
Aging
Priority Inversion
Priority Inheritance
```

---

# 🎯 Key Takeaway

Priority Scheduling is one of the most practical CPU scheduling algorithms and forms the foundation of RTOS, AUTOSAR OS, Embedded Systems, and Real-Time Computing.

While it efficiently handles critical tasks, it introduces challenges such as:

```text id="m84mxs"
Starvation

Priority Inversion
```

which are solved using:

```text id="j1n2ms"
Aging

Priority Inheritance
```

Understanding Priority Scheduling is essential before learning:

* Multilevel Queue Scheduling
* Multilevel Feedback Queue (MLFQ)
* RTOS Scheduling
* AUTOSAR OS Scheduling
* Linux CFS Scheduler
* Real-Time Systems
