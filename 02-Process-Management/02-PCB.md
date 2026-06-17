# 📦 Process Control Block (PCB)

> The Process Control Block (PCB) is one of the most important data structures in an Operating System. Every process has a PCB, and without it, the Operating System cannot manage processes, perform scheduling, or execute context switching.

---

# 📌 Introduction

When a process is created, the Operating System must keep track of:

* Process ID
* Current State
* CPU Registers
* Memory Information
* Scheduling Information
* Open Files

Where is all this information stored?

Answer:

```text
Process Control Block (PCB)
```

---

# 🏛️ What is a PCB?

## Definition

A PCB (Process Control Block) is a kernel data structure that contains all information needed by the Operating System to manage a process.

---

## Simple Definition

Think of PCB as:

```text
Identity Card
+
Resume
+
Current Status
```

of a process.

---

# Why Do We Need PCB?

Suppose the CPU is executing:

```text
Process A
```

Then the scheduler decides to run:

```text
Process B
```

The OS must save:

```text
Current Instruction

Registers

Memory Information
```

of Process A.

This information is stored in the PCB.

---

# Real Life Analogy

Imagine a hospital.

Each patient has:

```text
Name

Age

Medical History

Current Status

Treatment Details
```

stored in a file.

Similarly, every process has a PCB.

---

# PCB Architecture

```text
+-------------------------+
| Process Control Block   |
+-------------------------+
| Process ID (PID)        |
| Process State           |
| Program Counter         |
| CPU Registers           |
| Scheduling Information  |
| Memory Information      |
| I/O Status Information  |
| Accounting Information  |
+-------------------------+
```

---

# Major Components of PCB

---

# 1️⃣ Process ID (PID)

Every process has a unique identifier.

Example:

```text
Chrome PID = 4521

VS Code PID = 6789

Spotify PID = 8120
```

---

# Why PID?

The OS uses PID to:

* Identify processes
* Send signals
* Schedule processes
* Track resources

---

# Linux Example

```bash
ps -ef
```

Output:

```text
PID   CMD

1234  chrome

5678  code
```

---

# 2️⃣ Process State

Stores the current state of the process.

Possible states:

```text
New

Ready

Running

Waiting

Terminated
```

---

# Example

```text
Chrome
```

currently waiting for network data.

PCB stores:

```text
State = Waiting
```

---

# 3️⃣ Program Counter (PC)

Stores the address of the next instruction to execute.

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

Currently executing:

```text
b()
```

Program Counter stores the next instruction address.

---

# Why Important?

During context switching:

```text
Process A Paused
```

Later:

```text
Process A Resumes
```

Program Counter tells CPU where to continue.

---

# 4️⃣ CPU Registers

Stores CPU execution context.

---

## Registers Include

```text
General Registers

Stack Pointer

Program Counter

Status Register
```

---

# Example

CPU currently executing:

```text
Process A
```

Registers contain:

```text
R1 = 10

R2 = 25

R3 = 100
```

During context switching these values are saved in PCB.

---

# 5️⃣ CPU Scheduling Information

Used by scheduler.

---

## Contains

```text
Priority

Queue Position

Scheduling Policy

Time Slice
```

---

# Example

```text
Process A Priority = 5

Process B Priority = 10
```

Scheduler may execute Process B first.

---

# 6️⃣ Memory Management Information

Stores process memory details.

---

## Examples

```text
Page Table Pointer

Segment Table

Base Register

Limit Register
```

---

# Why Needed?

Allows OS to:

```text
Virtual Address
       ↓
Physical Address
```

translation.

---

# Example

```text
Process A

Virtual Address:
0x1000
```

PCB helps locate actual memory.

---

# 7️⃣ I/O Status Information

Stores information about devices used by process.

---

## Examples

```text
Open Files

Printers

Sockets

Disk Requests
```

---

# Example

Chrome currently accessing:

```text
file.txt
```

PCB stores open file information.

---

# 8️⃣ Accounting Information

Used for monitoring and billing.

---

## Stores

```text
CPU Usage

Memory Usage

Process Creation Time

Execution Time
```

---

# Example

Linux command:

```bash
top
```

displays information derived from PCB.

---

# Complete PCB Structure

```text
+----------------------------------+
| PCB                              |
+----------------------------------+
| PID                              |
| Process State                    |
| Program Counter                  |
| CPU Registers                    |
| Scheduling Information           |
| Memory Information               |
| I/O Information                  |
| Accounting Information           |
+----------------------------------+
```

---

# PCB and Context Switching

PCB plays a crucial role during context switching.

---

# Scenario

CPU executing:

```text
Process A
```

Scheduler selects:

```text
Process B
```

---

# Step 1

Save Process A state.

```text
Registers

Program Counter

State
```

saved into:

```text
PCB_A
```

---

# Step 2

Load Process B state.

```text
Registers

Program Counter

State
```

loaded from:

```text
PCB_B
```

---

# Context Switching Flow

```text
Running Process A
        │
        ▼
Save Context To PCB_A
        │
        ▼
Load Context From PCB_B
        │
        ▼
Run Process B
```

---

# PCB Storage Location

PCB is stored in:

```text
Kernel Space
```

---

# Why Not User Space?

Because:

```text
Security

Reliability

Protection
```

must be maintained.

---

# Process Table

Operating System maintains a collection of PCBs.

---

## Architecture

```text
Process Table

+---------+
| PCB A   |
+---------+

+---------+
| PCB B   |
+---------+

+---------+
| PCB C   |
+---------+
```

---

# Linux Perspective

Linux stores process information in:

```c
task_struct
```

---

# Simplified View

```c
struct task_struct
{
    pid_t pid;

    long state;

    int priority;

    mm_struct *mm;

    files_struct *files;
};
```

---

# Linux Commands Related to PCB

---

## View Processes

```bash
ps -ef
```

---

## View Process Details

```bash
cat /proc/<PID>/status
```

Example:

```bash
cat /proc/1234/status
```

---

## View Memory Information

```bash
cat /proc/<PID>/maps
```

---

# RTOS Perspective

RTOS uses:

```text
Task Control Block (TCB)
```

instead of PCB.

---

# TCB Stores

```text
Task State

Stack Pointer

Priority

Registers
```

---

# Example

FreeRTOS:

```text
Task A
Task B
Task C
```

Each task has its own TCB.

---

# AUTOSAR Perspective

AUTOSAR OS maintains task information similar to PCB/TCB.

Stores:

```text
Task State

Priority

Resources

Events
```

---

# PCB vs TCB

| PCB                 | TCB                   |
| ------------------- | --------------------- |
| Process Information | Task Information      |
| General Purpose OS  | RTOS                  |
| Linux, Windows      | FreeRTOS, AUTOSAR     |
| Larger Structure    | Lightweight Structure |

---

# Interview Questions

## Q1. What is a PCB?

PCB is a data structure used by the Operating System to store information about a process.

---

## Q2. Why is PCB required?

To manage processes and perform context switching.

---

## Q3. Where is PCB stored?

Kernel Space.

---

## Q4. What information is stored in PCB?

* PID
* State
* Registers
* Program Counter
* Scheduling Information
* Memory Information
* I/O Information

---

## Q5. Which PCB field is most important during context switching?

```text
Program Counter

CPU Registers
```

---

## Q6. Can a process exist without PCB?

No.

The OS cannot manage the process without a PCB.

---

## Q7. What is Linux equivalent of PCB?

```c
task_struct
```

---

## Q8. Difference Between PCB and TCB?

PCB manages processes.

TCB manages RTOS tasks.

---

# ⚠️ Common Interview Trap

Question:

```text
Does PCB contain the actual process code?
```

Answer:

```text
No.
```

PCB contains metadata about the process.

Actual code resides in:

```text
Code Segment (.text)
```

inside process memory.

---

# 📝 Quick Revision

```text
PCB
---
Process Control Block

Purpose
-------
Stores Process Information

Contains
--------
PID

State

Program Counter

CPU Registers

Scheduling Information

Memory Information

I/O Information

Accounting Information

Used In
-------
Process Management

Scheduling

Context Switching

Linux
-----
task_struct

RTOS
----
TCB
```

---

# 🎯 Key Takeaway

The Process Control Block (PCB) is the Operating System's record for a process. It stores everything required to manage, schedule, suspend, resume, and terminate a process.

Without PCBs, modern multitasking operating systems such as Linux, Windows, and UNIX would not be able to perform process scheduling or context switching.

The PCB is the foundation for understanding:

* Context Switching
* CPU Scheduling
* Process Scheduling Algorithms
* Linux `task_struct`
* RTOS Task Control Blocks (TCB)
* Kernel Process Management
