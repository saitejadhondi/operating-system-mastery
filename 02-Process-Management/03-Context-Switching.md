# 🔄 Context Switching

> Context Switching is one of the most important concepts in Operating Systems. It enables multitasking by allowing the CPU to switch execution from one process or thread to another. Every modern OS including Linux, Windows, Android, FreeRTOS, and AUTOSAR OS relies on context switching.

---

# 📌 Introduction

Imagine you are using:

```text
Google Chrome

VS Code

Spotify

Terminal
```

all at the same time.

You might think:

```text
All applications are running simultaneously
```

But on a single-core CPU:

```text
Only ONE process executes at any instant.
```

The Operating System creates the illusion of parallel execution using:

```text
Context Switching
```

---

# 🏛️ What is Context Switching?

## Definition

Context Switching is the process of saving the state of a currently running process or thread and restoring the state of another process or thread.

---

# Simple Definition

```text
Stop Process A
Save Its State

Start Process B
Restore Its State
```

This operation is called:

```text
Context Switch
```

---

# Why is Context Switching Needed?

A CPU can execute:

```text
One process per core
```

at a time.

However:

```text
Hundreds of processes
```

may exist simultaneously.

The OS must:

```text
Share CPU Time
```

among processes.

---

# Example

Running:

```text
Chrome

VS Code

Spotify
```

CPU executes:

```text
Chrome
   ↓
VS Code
   ↓
Spotify
   ↓
Chrome
```

rapidly.

Users perceive parallel execution.

---

# What is Context?

The "Context" of a process means:

```text
Everything required to resume execution later.
```

---

# Context Includes

```text
Program Counter

CPU Registers

Stack Pointer

Process State

Memory Information
```

---

# Example

Suppose:

```c
int main()
{
    a();
    b();
    c();
}
```

CPU currently executing:

```text
b()
```

To resume later, OS must remember:

```text
Current Instruction

Register Values

Stack State
```

---

# Where is Context Stored?

Inside the:

```text
PCB
(Process Control Block)
```

---

# Context Switching Flow

```text
Process A Running
        │
        ▼
Save Context To PCB_A
        │
        ▼
Load Context From PCB_B
        │
        ▼
Process B Running
```

---

# Visual Representation

```text
CPU
 │
 ▼

Running Process A
       │
       ▼
Save Context
       │
       ▼
Load Process B Context
       │
       ▼
Running Process B
```

---

# Step-by-Step Context Switching

---

# Step 1: Process A Running

```text
CPU
 │
 ▼
Process A
```

Registers contain:

```text
R1 = 10

R2 = 20

R3 = 30
```

---

# Step 2: Interrupt Occurs

Possible reasons:

```text
Time Slice Expired

I/O Request

Higher Priority Process

System Call
```

---

# Step 3: Save Process A Context

OS saves:

```text
Registers

Program Counter

Stack Pointer

State
```

into:

```text
PCB_A
```

---

# Step 4: Scheduler Runs

Scheduler selects:

```text
Process B
```

---

# Step 5: Load Process B Context

OS loads:

```text
Registers

Program Counter

Stack Pointer
```

from:

```text
PCB_B
```

---

# Step 6: Process B Executes

```text
CPU
 │
 ▼
Process B
```

Execution continues from the exact point it previously stopped.

---

# Context Switching Diagram

```text
Running A
    │
    ▼
Save A Context
    │
    ▼
Scheduler
    │
    ▼
Load B Context
    │
    ▼
Running B
```

---

# What Triggers a Context Switch?

---

# 1️⃣ Timer Interrupt

Most common reason.

---

## Scenario

Time slice expires.

```text
Process A
      │
      ▼
Time Quantum Ends
      │
      ▼
Context Switch
```

---

# Example

Round Robin Scheduling:

```text
Process A → 10 ms

Process B → 10 ms

Process C → 10 ms
```

---

# 2️⃣ I/O Request

Process requests:

```text
Disk

Keyboard

Network
```

Process enters:

```text
Waiting State
```

CPU switches to another process.

---

# Example

```text
Chrome Requests Network Data
           │
           ▼
Waiting
           │
           ▼
CPU Executes VS Code
```

---

# 3️⃣ Higher Priority Process

Common in:

```text
RTOS

AUTOSAR OS

Linux
```

---

# Example

```text
Task A Priority = 2

Task B Priority = 10
```

Task B becomes ready.

Scheduler switches immediately.

---

# 4️⃣ System Call

Example:

```c
read();

write();

fork();
```

Entering kernel mode may cause scheduling decisions.

---

# Process Context Switching vs Thread Context Switching

---

# Process Context Switch

Switching between:

```text
Process A

Process B
```

---

# Requires

```text
Register Save

Memory Map Switch

Page Table Switch

PCB Update
```

---

# Expensive Operation

---

# Thread Context Switch

Switching between:

```text
Thread A

Thread B
```

inside same process.

---

# Requires

```text
Register Save

Stack Switch
```

Shared memory remains unchanged.

---

# Faster Operation

---

# Comparison

| Feature              | Process Switch | Thread Switch |
| -------------------- | -------------- | ------------- |
| Address Space Change | Yes            | No            |
| Page Table Switch    | Yes            | No            |
| Overhead             | High           | Low           |
| Speed                | Slower         | Faster        |

---

# Why Context Switching is Expensive?

During switching:

```text
CPU Does No Useful Work
```

This is called:

```text
Context Switching Overhead
```

---

# Overhead Includes

```text
Saving Registers

Loading Registers

Kernel Execution

Cache Effects

TLB Effects
```

---

# Cache Impact

Suppose:

```text
Process A
```

loads data into cache.

After switch:

```text
Process B
```

needs different data.

CPU cache becomes less effective.

---

# TLB Impact

Memory translation information may become invalid.

Results:

```text
More TLB Misses
```

after switching.

---

# Linux Perspective

Linux performs context switching using:

```c
schedule()
```

function.

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
context_switch()
```

---

# Linux Scheduler

Linux scheduler decides:

```text
Which Process Runs Next?
```

using scheduling policies.

---

# Linux Commands

View context switches:

```bash
vmstat
```

---

Example:

```bash
vmstat 1
```

---

Output:

```text
cs
```

represents:

```text
Context Switches Per Second
```

---

# Another Method

```bash
pidstat -w
```

Displays process context switches.

---

# RTOS Perspective

RTOS heavily relies on context switching.

---

# Example

FreeRTOS

```text
Task A

Task B

Task C
```

Scheduler rapidly switches tasks.

---

# RTOS Context Switch Trigger

```text
Tick Interrupt
```

or

```text
Higher Priority Task Ready
```

---

# AUTOSAR OS Perspective

AUTOSAR OS performs:

```text
Task Switching

ISR Switching

Event-Based Scheduling
```

using context switching.

---

# Automotive Example

```text
Engine Task

ABS Task

Airbag Task
```

Scheduler switches based on priority.

---

# Airbag Example

```text
Engine Task Running
       │
       ▼
Crash Detected
       │
       ▼
Airbag Task Ready
       │
       ▼
Immediate Context Switch
```

---

# Real World Analogy

Imagine a teacher helping students.

```text
Student A
      ↓
Teacher Helps

Student B
      ↓
Teacher Helps

Student C
      ↓
Teacher Helps
```

Before leaving:

```text
Teacher Notes Progress
```

Later resumes from same point.

These notes are equivalent to:

```text
Process Context
```

---

# Interview Questions

## Q1. What is Context Switching?

Saving the state of one process/thread and restoring another process/thread.

---

## Q2. Why is Context Switching Required?

To share CPU among multiple processes.

---

## Q3. What information is saved during Context Switching?

```text
Program Counter

Registers

Stack Pointer

Process State
```

---

## Q4. Where is Context Stored?

PCB (Process Control Block).

---

## Q5. Why is Context Switching Expensive?

Because CPU performs administrative work instead of executing application code.

---

## Q6. Which is faster?

Process switching or thread switching?

Thread switching.

---

## Q7. Does Context Switching improve performance?

Not directly.

It improves:

```text
Responsiveness

Resource Utilization
```

---

## Q8. What causes Context Switching?

* Timer Interrupt
* I/O Request
* Higher Priority Process
* System Calls

---

# ⚠️ Common Interview Trap

Question:

```text
Can context switching happen without changing processes?
```

Answer:

```text
Yes.
```

Switching between:

```text
Thread A

Thread B
```

within the same process is also a context switch.

---

# 📝 Quick Revision

```text
Context Switching
-----------------
Save Current Context
Load New Context

Stored In
---------
PCB

Context Includes
----------------
Program Counter

Registers

Stack Pointer

State

Triggers
--------
Timer Interrupt

I/O Request

System Call

Higher Priority Process

Process Switch
--------------
Expensive

Thread Switch
-------------
Faster

Linux
-----
schedule()

RTOS
----
Tick Interrupt
```

---

# 🎯 Key Takeaway

Context Switching is the mechanism that enables multitasking operating systems to share CPU resources among multiple processes and threads.

The Operating System saves the current execution context into a PCB, selects another process using the scheduler, restores its context, and resumes execution.

Understanding Context Switching is essential for:

* CPU Scheduling
* Linux Scheduler
* RTOS Scheduling
* AUTOSAR OS
* Multithreading
* Performance Optimization
* Kernel Development
