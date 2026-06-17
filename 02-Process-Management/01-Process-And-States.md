# 🔄 Process and Process States

> A Process is the fundamental unit of execution in an Operating System. Understanding processes and their states is essential for learning CPU scheduling, context switching, synchronization, Linux internals, RTOS, and kernel development.

---

# 📌 Introduction

When you run an application:

```text
Chrome
VS Code
Spotify
Calculator
```

the Operating System creates one or more **Processes**.

A process is not simply a program file.

A process is a **running instance of a program**.

---

# 🏛️ What is a Process?

## Definition

A Process is a program that is currently executing.

---

## Program vs Process

### Program

```text
Stored on Disk

chrome.exe

hello.out

calculator.exe
```

Passive entity.

---

### Process

```text
Loaded Into Memory

Executing Instructions

Using CPU
```

Active entity.

---

# Process Creation

```text
Program On Disk
       │
       ▼
Loaded Into Memory
       │
       ▼
Process Created
       │
       ▼
Execution Starts
```

---

# Real Example

When you launch:

```text
Google Chrome
```

the OS:

1. Loads executable into memory
2. Allocates resources
3. Creates PCB
4. Assigns PID
5. Schedules CPU

Now Chrome becomes a process.

---

# Components of a Process

Every process consists of:

```text
Code Section

Data Section

Heap

Stack

Registers

Program Counter

Open Files

Process ID
```

---

# Process Memory Layout

```text
High Address
+-------------------+
|       Stack       |
+-------------------+
|       Heap        |
+-------------------+
| Initialized Data  |
+-------------------+
| Uninitialized     |
| Data (.bss)       |
+-------------------+
| Code (.text)      |
+-------------------+
Low Address
```

---

# Code Section (.text)

Contains:

```c
int main()
{
    printf("Hello");
}
```

Machine instructions reside here.

---

# Data Section

Stores:

```c
int x = 10;
```

Initialized global variables.

---

# BSS Section

Stores:

```c
int count;
```

Uninitialized global variables.

---

# Heap

Dynamic memory allocation.

Example:

```c
malloc()
calloc()
realloc()
```

Memory grows upward.

---

# Stack

Stores:

* Function calls
* Local variables
* Return addresses

Memory grows downward.

---

# Process Attributes

Every process has:

| Attribute       | Description             |
| --------------- | ----------------------- |
| PID             | Process ID              |
| State           | Running, Ready, Waiting |
| Priority        | Scheduling Priority     |
| Registers       | CPU Context             |
| Program Counter | Next Instruction        |
| Open Files      | File Descriptors        |

---

# Process States

A process continuously changes states during execution.

---

# Why States Exist?

CPU is limited.

Many processes compete for CPU time.

The OS must track process status.

---

# Basic Process State Model

```text
         +---------+
         |  New    |
         +---------+
              |
              ▼
         +---------+
         |  Ready  |
         +---------+
              |
              ▼
         +---------+
         | Running |
         +---------+
              |
       +------+------+
       |             |
       ▼             ▼
 +-----------+   +---------+
 | Waiting   |   |Terminated|
 +-----------+   +---------+
       |
       ▼
    Ready
```

---

# 1️⃣ New State

Process is being created.

---

## Activities

OS performs:

```text
Allocate Memory

Create PCB

Assign PID

Initialize Resources
```

---

## Example

Double-click:

```text
chrome.exe
```

OS creates process.

---

# 2️⃣ Ready State

Process is ready to execute.

Waiting for CPU allocation.

---

## Characteristics

```text
Memory Allocated

Resources Available

Waiting For CPU
```

---

## Example

```text
Chrome Ready

VS Code Running
```

Chrome waits for CPU.

---

# 3️⃣ Running State

Process currently executing on CPU.

---

## Characteristics

```text
Instructions Executing

CPU Allocated
```

---

## Example

```text
Chrome Rendering Page
```

CPU actively executing instructions.

---

# 4️⃣ Waiting (Blocked) State

Process waiting for an event.

---

## Examples

Waiting for:

```text
Disk I/O

Keyboard Input

Network Packet

File Access
```

---

## Scenario

```text
Process Requests File
         │
         ▼
Disk Reading
         │
         ▼
Process Waiting
```

CPU assigned elsewhere.

---

# 5️⃣ Terminated State

Process execution completed.

---

## Reasons

### Normal Completion

```c
return 0;
```

---

### Error

```text
Segmentation Fault
```

---

### User Termination

```bash
kill PID
```

---

# Extended Process States

Modern OS implementations include additional states.

---

# Suspended Ready

Process swapped out of memory.

Ready to run later.

---

# Suspended Waiting

Process:

```text
Waiting Event
+
Swapped To Disk
```

---

# Extended State Diagram

```text
New
 │
 ▼
Ready
 │
 ▼
Running
 │
 ├────────► Terminated
 │
 ▼
Waiting
 │
 ▼
Ready

Suspended Ready
Suspended Waiting
```

---

# Process State Transitions

## New → Ready

Process created successfully.

---

## Ready → Running

CPU scheduler selects process.

---

## Running → Waiting

Process requests I/O.

---

## Waiting → Ready

I/O operation completes.

---

## Running → Ready

Preemption occurs.

---

## Running → Terminated

Process finishes execution.

---

# Real Linux Example

View running processes:

```bash
ps -ef
```

---

View process tree:

```bash
pstree
```

---

View process status:

```bash
top
```

---

# Linux Process States

Linux uses:

| State | Meaning               |
| ----- | --------------------- |
| R     | Running               |
| S     | Sleeping              |
| D     | Uninterruptible Sleep |
| T     | Stopped               |
| Z     | Zombie                |

---

# Zombie Process

Process completed.

Parent has not collected exit status.

---

## Example

```text
Child Exits
      │
      ▼
Parent Does Not Call wait()
      │
      ▼
Zombie Created
```

---

# Orphan Process

Parent terminates before child.

---

## Example

```text
Parent Dies
      │
      ▼
Child Continues
```

Child adopted by:

```text
init/systemd
```

---

# Process Life Cycle Example

Opening Chrome:

```text
New
 │
 ▼
Ready
 │
 ▼
Running
 │
 ▼
Waiting (Network)
 │
 ▼
Ready
 │
 ▼
Running
 │
 ▼
Terminated
```

---

# Process vs Thread

| Process                    | Thread                  |
| -------------------------- | ----------------------- |
| Independent Execution Unit | Smallest Execution Unit |
| Own Memory Space           | Shared Memory           |
| Expensive Context Switch   | Faster Context Switch   |
| IPC Required               | Direct Communication    |

---

# RTOS Perspective

Many RTOS implementations use:

```text
Tasks
```

instead of traditional processes.

Examples:

* FreeRTOS
* Zephyr
* ThreadX

---

# AUTOSAR Perspective

AUTOSAR OS manages:

```text
Tasks

Events

Resources

ISR
```

rather than traditional Linux-style processes.

---

# Interview Questions

## Q1. What is a Process?

A process is a program in execution.

---

## Q2. Difference Between Program and Process?

Program is passive.

Process is active.

---

## Q3. What are the five basic process states?

```text
New

Ready

Running

Waiting

Terminated
```

---

## Q4. Why does a process enter Waiting state?

Waiting for:

* Disk I/O
* Keyboard Input
* Network Event

---

## Q5. What is Ready State?

Process has all required resources except CPU.

---

## Q6. What causes Ready → Running transition?

CPU scheduler dispatches process.

---

## Q7. What is a Zombie Process?

Terminated process whose parent has not collected exit status.

---

## Q8. What is an Orphan Process?

A child process whose parent terminated first.

---

## Q9. Difference Between Ready and Waiting?

Ready:

```text
Waiting For CPU
```

Waiting:

```text
Waiting For Event
```

---

# ⚠️ Common Interview Trap

Question:

```text
Can multiple processes be in Running state simultaneously?
```

Answer:

```text
Single-Core CPU
--------------
Only One

Multi-Core CPU
--------------
Multiple Processes
```

One running process per CPU core.

---

# 📝 Quick Revision

```text
Process
-------
Program In Execution

Process States
--------------
New
Ready
Running
Waiting
Terminated

Ready
-----
Waiting For CPU

Waiting
-------
Waiting For Event

Linux States
------------
R
S
D
T
Z

Special Processes
-----------------
Zombie
Orphan
```

---

# 🎯 Key Takeaway

A Process is a running instance of a program.

The Operating System continuously moves processes between different states to efficiently utilize CPU resources and handle multiple applications simultaneously.

Understanding process states is essential before learning:

* PCB
* Context Switching
* CPU Scheduling
* Threads
* Synchronization
* Linux Scheduling
* RTOS Task Management
