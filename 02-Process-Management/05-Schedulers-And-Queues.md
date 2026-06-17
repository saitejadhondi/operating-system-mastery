# ⚙️ Schedulers and Scheduling Queues

> The Operating System may have hundreds of processes in memory, but only a few CPU cores. The Scheduler is responsible for deciding which process gets CPU time. Understanding schedulers and queues is essential before learning CPU Scheduling Algorithms such as FCFS, SJF, Round Robin, and Priority Scheduling.

---

# 📌 Introduction

Suppose your system is running:

```text
Chrome

VS Code

Spotify

Terminal

Zoom

Slack
```

At the same time.

Question:

```text
Which process gets CPU first?
```

Who decides?

Answer:

```text
The Scheduler
```

---

# Why Do We Need Scheduling?

CPU is a limited resource.

Example:

```text
100 Processes

4 CPU Cores
```

Only:

```text
4 Processes
```

can execute simultaneously.

The Operating System must decide:

```text
Who Runs?

When?

For How Long?
```

---

# What is a Scheduler?

## Definition

A Scheduler is an Operating System component responsible for selecting processes for execution.

---

# Responsibilities

```text
Process Selection

CPU Allocation

Queue Management

Context Switching Decisions

Priority Handling
```

---

# Scheduling System Overview

```text
New Processes
      │
      ▼
Job Queue
      │
      ▼
Ready Queue
      │
      ▼
CPU
      │
      ▼
Waiting Queue
      │
      ▼
Ready Queue
```

---

# Scheduling Queues

Processes move through different queues.

---

# 1️⃣ Job Queue

Contains:

```text
All Processes In The System
```

including:

```text
New

Ready

Waiting
```

processes.

---

# Example

```text
Chrome

VS Code

Spotify

Zoom

Slack
```

All belong to Job Queue.

---

# 2️⃣ Ready Queue

Contains processes:

```text
Ready To Execute

Waiting For CPU
```

---

# Example

```text
Process A

Process B

Process C
```

all waiting for CPU.

---

# Diagram

```text
Ready Queue

+-----------+
| Process A |
+-----------+

+-----------+
| Process B |
+-----------+

+-----------+
| Process C |
+-----------+
```

---

# 3️⃣ Waiting Queue

Contains blocked processes.

Waiting for:

```text
Disk

Keyboard

Network

Printer
```

---

# Example

```text
Chrome Waiting For Network

VS Code Waiting For File
```

---

# Queue Movement

```text
Ready
   │
   ▼
Running
   │
   ▼
Waiting
   │
   ▼
Ready
```

---

# Types of Schedulers

Operating Systems typically use:

```text
Long-Term Scheduler

Short-Term Scheduler

Medium-Term Scheduler
```

---

# 1️⃣ Long-Term Scheduler

Also called:

```text
Job Scheduler
```

---

# Purpose

Controls:

```text
How Many Processes Enter Memory
```

---

# Flow

```text
Job Queue
     │
     ▼
Memory
```

---

# Example

100 jobs submitted.

Only:

```text
20 Jobs
```

loaded into memory.

Decision made by:

```text
Long-Term Scheduler
```

---

# Responsibilities

✅ Controls degree of multiprogramming

✅ Prevents memory overload

✅ Balances CPU-bound and I/O-bound jobs

---

# Frequency

Runs:

```text
Rarely
```

---

# 2️⃣ Short-Term Scheduler

Also called:

```text
CPU Scheduler
```

---

# Purpose

Selects:

```text
Which Ready Process
Gets CPU Next
```

---

# Flow

```text
Ready Queue
      │
      ▼
CPU
```

---

# Example

Ready Queue:

```text
A

B

C
```

Scheduler selects:

```text
B
```

for execution.

---

# Frequency

Runs:

```text
Very Frequently
```

milliseconds.

---

# Most Important Scheduler

For interviews:

```text
Short-Term Scheduler
```

is usually implied when someone says:

```text
Scheduler
```

---

# 3️⃣ Medium-Term Scheduler

Responsible for:

```text
Swapping
```

---

# Purpose

Temporarily removes processes from memory.

---

# Flow

```text
Memory Full
      │
      ▼
Swap Process To Disk
```

---

# Example

```text
Process A
```

inactive for long time.

OS swaps it to disk.

---

# Benefits

✅ Frees RAM

✅ Prevents Thrashing

---

# Frequency

Runs occasionally.

---

# Scheduler Comparison

| Feature    | Long-Term  | Medium-Term | Short-Term     |
| ---------- | ---------- | ----------- | -------------- |
| Purpose    | Admit Jobs | Swapping    | CPU Allocation |
| Frequency  | Low        | Medium      | High           |
| Speed      | Slow       | Moderate    | Very Fast      |
| Queue Used | Job Queue  | Memory      | Ready Queue    |

---

# What is a Dispatcher?

Many interviewers ask:

```text
Scheduler vs Dispatcher
```

---

# Scheduler

Decides:

```text
Who Runs Next?
```

---

# Dispatcher

Performs:

```text
Context Switch

Mode Switch

CPU Transfer
```

---

# Flow

```text
Scheduler
     │
     ▼
Select Process
     │
     ▼
Dispatcher
     │
     ▼
Execute Process
```

---

# Dispatcher Responsibilities

```text
Context Switching

Switch To User Mode

Jump To Program Counter
```

---

# Dispatch Latency

Time required for:

```text
Stop Process A

Start Process B
```

---

# Smaller Dispatch Latency

Means:

```text
Better Performance
```

---

# CPU Scheduling Cycle

```text
Ready Queue
      │
      ▼
Scheduler
      │
      ▼
Dispatcher
      │
      ▼
Running
      │
      ▼
Waiting
      │
      ▼
Ready Queue
```

---

# Linux Perspective

Linux uses:

```c
schedule()
```

for scheduling.

---

# Simplified Flow

```text
Timer Interrupt
      │
      ▼
schedule()
      │
      ▼
Select Next Task
      │
      ▼
Context Switch
```

---

# Linux Run Queue

Linux maintains:

```text
Run Queue
```

similar to Ready Queue.

---

# View Scheduler Information

```bash
ps -eo pid,comm,pri
```

---

# RTOS Perspective

RTOS uses:

```text
Priority-Based Scheduling
```

---

# Example

```text
Task A Priority = 10

Task B Priority = 5
```

Task A executes first.

---

# AUTOSAR Perspective

AUTOSAR Scheduler manages:

```text
Tasks

Events

Resources

ISRs
```

using priority-based scheduling.

---

# Automotive Example

```text
Airbag Task

ABS Task

Engine Task
```

Airbag task receives highest priority.

---

# Real World Analogy

Imagine an airport.

---

# Ready Queue

```text
Passengers Waiting
```

---

# Scheduler

```text
Gate Officer
```

decides who boards next.

---

# Dispatcher

```text
Flight Crew
```

actually moves passengers onto the plane.

---

# Interview Questions

## Q1. What is a Scheduler?

A Scheduler selects processes for execution.

---

## Q2. What is a Ready Queue?

Processes ready to run but waiting for CPU.

---

## Q3. Difference Between Job Queue and Ready Queue?

Job Queue contains all processes.

Ready Queue contains only runnable processes.

---

## Q4. What does Long-Term Scheduler do?

Controls how many processes enter memory.

---

## Q5. What does Short-Term Scheduler do?

Selects the next process for CPU execution.

---

## Q6. What does Medium-Term Scheduler do?

Swaps processes between memory and disk.

---

## Q7. Difference Between Scheduler and Dispatcher?

Scheduler selects.

Dispatcher executes the switch.

---

## Q8. Which Scheduler Runs Most Frequently?

Short-Term Scheduler.

---

# ⚠️ Common Interview Trap

Question:

```text
Which scheduler controls the degree of multiprogramming?
```

Answer:

```text
Long-Term Scheduler
```

because it controls how many processes enter memory.

---

# 📝 Quick Revision

```text
Queues
------
Job Queue

Ready Queue

Waiting Queue

Schedulers
----------
Long-Term
(Job Admission)

Medium-Term
(Swapping)

Short-Term
(CPU Selection)

Dispatcher
----------
Context Switch

Mode Switch

CPU Transfer

Linux
-----
schedule()

RTOS
----
Priority Scheduler
```

---

# 🎯 Key Takeaway

Schedulers are responsible for managing CPU allocation and process execution.

The Long-Term Scheduler controls admission of processes, the Medium-Term Scheduler handles swapping, and the Short-Term Scheduler selects processes for CPU execution.

The Dispatcher performs the actual context switch and transfers CPU control.

Understanding schedulers and queues is essential before learning:

* FCFS
* SJF
* SRTF
* Priority Scheduling
* Round Robin
* Multilevel Queue Scheduling
* Linux Scheduler
* RTOS Scheduler
