# ⚡ Preemptive vs Non-Preemptive Scheduling

> Preemptive and Non-Preemptive Scheduling are the two fundamental approaches used by Operating Systems to allocate CPU time. Understanding these concepts is essential before learning FCFS, SJF, SRTF, Priority Scheduling, Round Robin, Linux Scheduling, RTOS Scheduling, and AUTOSAR OS scheduling.

---

# 📌 Introduction

Imagine there is only:

```text
1 CPU
```

but multiple processes want to execute.

Example:

```text
Chrome

VS Code

Spotify

Terminal
```

Question:

```text
Can the OS force a running process to give up the CPU?
```

The answer determines whether scheduling is:

```text
Preemptive
```

or

```text
Non-Preemptive
```

---

# 🏛️ What is CPU Scheduling?

CPU Scheduling is the process of deciding:

```text
Who Gets CPU?

When?

For How Long?
```

Scheduling algorithms can be categorized into:

```text
Non-Preemptive Scheduling

Preemptive Scheduling
```

---

# 1️⃣ Non-Preemptive Scheduling

## Definition

In Non-Preemptive Scheduling, once a process gets the CPU, it keeps the CPU until:

```text
Process Finishes
          OR
Process Voluntarily Waits
```

The OS cannot forcibly remove it.

---

# Example

Suppose:

```text
Process A = 10 ms

Process B = 5 ms

Process C = 2 ms
```

Arrival:

```text
A → B → C
```

Execution:

```text
AAAAAAAAAA
BBBBB
CC
```

---

# Timeline

```text
0         10        15       17
|----A----|---B----|---C----|
```

---

# Characteristics

✅ Simple

✅ Low Overhead

✅ Easy Implementation

❌ Poor Response Time

❌ Long Waiting Time

❌ Can Cause Starvation

---

# Real Life Analogy

Single Bathroom

```text
Person A Enters
      │
      ▼
Must Finish Completely
      │
      ▼
Person B Enters
```

No interruptions allowed.

---

# Examples of Non-Preemptive Algorithms

### FCFS

```text
First Come First Serve
```

---

### Non-Preemptive SJF

```text
Shortest Job First
```

---

### Non-Preemptive Priority Scheduling

```text
Highest Priority Executes
Until Completion
```

---

# 2️⃣ Preemptive Scheduling

## Definition

In Preemptive Scheduling, the Operating System can forcibly take the CPU away from a running process.

---

# Example

Process A:

```text
20 ms
```

Currently running.

Suddenly:

```text
Process B
Priority = High
```

arrives.

OS immediately performs:

```text
Context Switch
```

and executes Process B.

---

# Timeline

```text
AAAAA
     ↓
Process B Arrives

AAAAA BBB AAAAAAAAAA
```

---

# Characteristics

✅ Better Response Time

✅ Fair CPU Sharing

✅ Supports Interactive Systems

✅ Suitable For Modern OS

❌ More Context Switches

❌ Higher Overhead

❌ More Complex

---

# Real Life Analogy

Emergency Room

```text
Normal Patient
      │
      ▼
Critical Patient Arrives
      │
      ▼
Doctor Immediately Switches
```

This is preemption.

---

# What Causes Preemption?

---

# 1️⃣ Time Quantum Expiry

Used in:

```text
Round Robin Scheduling
```

Example:

```text
Time Slice = 10 ms
```

After 10 ms:

```text
Process Removed

Next Process Runs
```

---

# 2️⃣ Higher Priority Process Arrives

Example:

```text
Task A Priority = 2

Task B Priority = 10
```

Task B arrives.

OS switches immediately.

---

# 3️⃣ Interrupt

Hardware interrupt occurs.

Example:

```text
Keyboard Input

Network Packet

Timer Interrupt
```

---

# 4️⃣ RTOS Event

High-priority real-time task becomes ready.

---

# Example

```text
Engine Task Running
```

Suddenly:

```text
Airbag Task Ready
```

Immediate preemption occurs.

---

# Visual Comparison

## Non-Preemptive

```text
Process A
───────────────
Process B Waits
```

---

## Preemptive

```text
Process A
─────
     ↓
Process B
────
     ↓
Process A
────────
```

---

# Comparison Table

| Feature              | Non-Preemptive | Preemptive |
| -------------------- | -------------- | ---------- |
| CPU Taken Forcefully | No             | Yes        |
| Context Switches     | Fewer          | More       |
| Overhead             | Low            | Higher     |
| Response Time        | Poor           | Better     |
| Complexity           | Simple         | Complex    |
| Interactive Systems  | Not Suitable   | Suitable   |
| RTOS Support         | Limited        | Excellent  |

---

# Context Switching Relationship

Preemptive Scheduling requires:

```text
Context Switching
```

frequently.

---

# Flow

```text
Running Process
       │
       ▼
Preemption
       │
       ▼
Save Context
       │
       ▼
Load New Process
```

---

# Why Modern OS Use Preemptive Scheduling?

Modern systems run:

```text
Browsers

Games

Editors

Video Calls

Background Services
```

Users expect:

```text
Instant Response
```

Preemptive scheduling provides responsiveness.

---

# Linux Perspective

Linux uses:

```text
Preemptive Scheduling
```

---

# Example

Linux scheduler:

```c
schedule()
```

can interrupt a running process.

---

# Linux Example

Running:

```bash
yes > /dev/null
```

creates a CPU-intensive process.

Even then:

```bash
firefox
```

opens normally.

Why?

Because Linux preempts the CPU-intensive task.

---

# Windows Perspective

Windows also uses:

```text
Preemptive Multitasking
```

---

# RTOS Perspective

Most RTOS systems use:

```text
Priority-Based Preemptive Scheduling
```

---

# Example

```text
Task A Priority = 1

Task B Priority = 10
```

Task B immediately executes.

---

# Why RTOS Needs Preemption?

Consider:

```text
Airbag Controller
```

Waiting until another task finishes could be dangerous.

Immediate execution is required.

---

# AUTOSAR Perspective

AUTOSAR OS supports:

```text
Preemptive Tasks

Non-Preemptive Tasks
```

---

# AUTOSAR Task Types

### Basic Task

Often preemptive.

---

### Non-Preemptive Task

Runs until completion.

---

# Automotive Example

```text
Engine Monitoring Task
```

running.

Suddenly:

```text
Airbag Event
```

occurs.

Scheduler preempts engine task.

---

# Performance Tradeoff

## Non-Preemptive

```text
Less Overhead
```

because fewer context switches.

---

## Preemptive

```text
Better Responsiveness
```

but more switching overhead.

---

# Gantt Chart Example

Processes:

```text
P1 = 10 ms

P2 = 3 ms
```

P2 arrives after 2 ms.

---

## Non-Preemptive

```text
0          10       13
|----P1----|--P2----|
```

---

## Preemptive

```text
0    2   5         13
|P1|P2|-----P1------|
```

Notice:

```text
P2 finishes much earlier.
```

---

# Real World Analogy

## Non-Preemptive

Single Speaker Presentation

```text
Speaker A
Must Finish
```

before Speaker B.

---

## Preemptive

Meeting Moderator

```text
Speaker A Talking
       │
       ▼
Emergency Announcement
       │
       ▼
Immediate Interruption
```

---

# Interview Questions

## Q1. What is Preemptive Scheduling?

The OS can forcibly remove a running process from the CPU.

---

## Q2. What is Non-Preemptive Scheduling?

A process keeps the CPU until completion or voluntary waiting.

---

## Q3. Which provides better response time?

```text
Preemptive Scheduling
```

---

## Q4. Which has lower overhead?

```text
Non-Preemptive Scheduling
```

because fewer context switches occur.

---

## Q5. Why do modern operating systems use preemptive scheduling?

To improve:

* Responsiveness
* Fairness
* Interactive performance

---

## Q6. Which scheduling type is preferred in RTOS?

```text
Preemptive Scheduling
```

because critical tasks must execute immediately.

---

## Q7. Can AUTOSAR OS support both?

Yes.

AUTOSAR supports:

```text
Preemptive Tasks

Non-Preemptive Tasks
```

---

## Q8. Which causes more context switching?

```text
Preemptive Scheduling
```

---

# ⚠️ Common Interview Trap

Question:

```text
Does Preemptive Scheduling always improve performance?
```

Answer:

```text
No.
```

Preemption improves responsiveness but introduces:

```text
Context Switching Overhead

Cache Misses

TLB Misses
```

Too much preemption can reduce overall throughput.

---

# 📝 Quick Revision

```text
Non-Preemptive
--------------
CPU Not Taken Away

Examples:
FCFS
SJF
Priority

Advantages:
Simple
Low Overhead

Disadvantages:
Poor Response Time

--------------------------------

Preemptive
----------
CPU Can Be Taken Away

Examples:
Round Robin
SRTF
Priority (Preemptive)

Advantages:
Fast Response
Fairness

Disadvantages:
More Context Switches

Linux:
Preemptive

RTOS:
Priority-Based Preemptive

AUTOSAR:
Supports Both
```

---

# 🎯 Key Takeaway

The fundamental difference is:

```text
Non-Preemptive
--------------
Process Gives Up CPU

Preemptive
----------
OS Takes CPU Away
```

Modern Operating Systems such as Linux and Windows use preemptive scheduling for responsiveness, while RTOS and AUTOSAR OS rely heavily on priority-based preemption to meet real-time deadlines.

Understanding this concept is critical before learning:

* FCFS
* SJF
* SRTF
* Priority Scheduling
* Round Robin
* Multilevel Queue Scheduling
* Linux CFS Scheduler
* RTOS Scheduling
* AUTOSAR Task Scheduling
