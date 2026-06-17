# 🔐 User Mode vs Kernel Mode

> User Mode and Kernel Mode are fundamental concepts in Operating Systems that provide security, protection, and controlled access to hardware resources. Every modern OS including Linux, Windows, Android, macOS, FreeRTOS, and AUTOSAR OS relies on privilege levels.

---

# 📌 Introduction

Imagine if every application could directly:

```text
Access RAM

Modify Hardware

Control CPU

Access Disk

Shutdown System
```

What would happen?

```text
System Crashes

Data Corruption

Security Issues

Malware Attacks
```

To prevent this, Operating Systems separate execution into:

```text
User Mode
     &
Kernel Mode
```

---

# 🏛️ What is User Mode?

## Definition

User Mode is a restricted execution mode where applications run with limited privileges.

Applications cannot directly access hardware resources.

---

# Examples

Applications running in User Mode:

```text
Google Chrome

VS Code

Spotify

Calculator

Microsoft Word
```

---

# User Mode Characteristics

✅ Restricted Privileges

✅ No Direct Hardware Access

✅ Safer Environment

✅ Process Isolation

---

# What User Mode Cannot Do?

Applications cannot directly:

```text
Access Device Registers

Modify Page Tables

Execute Privileged Instructions

Access Physical Memory

Control Interrupts
```

---

# Example

Suppose Chrome wants to read a file:

```c
read(file);
```

Chrome cannot directly access the disk.

Instead:

```text
Chrome
   │
   ▼
System Call
   │
   ▼
Kernel
   │
   ▼
Disk Access
```

---

# What is Kernel Mode?

## Definition

Kernel Mode is the privileged execution mode where the Operating System kernel executes.

The kernel has unrestricted access to system resources.

---

# Kernel Mode Capabilities

The kernel can:

```text
Access Hardware

Manage Memory

Handle Interrupts

Schedule Processes

Access Device Drivers

Control CPU
```

---

# Examples of Kernel Components

```text
Process Scheduler

Memory Manager

File System

Device Drivers

Network Stack
```

---

# Kernel Mode Characteristics

✅ Full Hardware Access

✅ Privileged Instructions Allowed

✅ Resource Management

✅ System Control

---

# Why Do We Need Two Modes?

Without protection:

```text
Application Error
       ↓
Entire System Crash
```

With protection:

```text
Application Error
       ↓
Application Crashes
       ↓
OS Continues Running
```

---

# Architecture

```text
+----------------------+
| User Applications    |
+----------------------+
          │
          ▼
+----------------------+
| User Mode            |
+----------------------+
          │
   System Call
          │
          ▼
+----------------------+
| Kernel Mode          |
+----------------------+
          │
          ▼
+----------------------+
| Hardware             |
+----------------------+
```

---

# CPU Privilege Levels

Modern CPUs support privilege rings.

---

# x86 Architecture

```text
Ring 0  → Kernel Mode

Ring 1

Ring 2

Ring 3  → User Mode
```

---

# Common Usage

```text
Ring 0
Kernel

Ring 3
Applications
```

Most operating systems use only Ring 0 and Ring 3.

---

# User Mode vs Kernel Mode

| Feature                 | User Mode       | Kernel Mode  |
| ----------------------- | --------------- | ------------ |
| Privileges              | Limited         | Full         |
| Hardware Access         | No              | Yes          |
| Memory Access           | Restricted      | Full         |
| Privileged Instructions | Not Allowed     | Allowed      |
| System Stability        | Safer           | Critical     |
| Examples                | Chrome, VS Code | Linux Kernel |

---

# Mode Switching

The CPU continuously switches between:

```text
User Mode
      ↓
Kernel Mode
      ↓
User Mode
```

during execution.

---

# Example

Opening a file:

```c
open("data.txt");
```

---

# Flow

```text
Application
      │
      ▼
System Call
      │
      ▼
Kernel Mode
      │
      ▼
Disk Access
      │
      ▼
Return To User Mode
```

---

# System Calls

System Calls provide a controlled interface between:

```text
User Applications
         &
Operating System
```

---

# Common System Calls

```c
fork()

exec()

read()

write()

open()

close()
```

---

# Example

```c
#include <unistd.h>

write(1, "Hello", 5);
```

Execution flow:

```text
Application
     │
     ▼
write()
     │
     ▼
Kernel
     │
     ▼
Terminal Output
```

---

# Mode Switch Diagram

```text
User Mode
    │
    ▼
System Call
    │
    ▼
Kernel Mode
    │
    ▼
Hardware Access
    │
    ▼
Return
    │
    ▼
User Mode
```

---

# Interrupts and Mode Switching

Interrupts automatically switch CPU into Kernel Mode.

---

# Example

Keyboard Input

```text
Key Pressed
      │
      ▼
Interrupt Generated
      │
      ▼
Kernel Mode
      │
      ▼
Interrupt Handler
      │
      ▼
Return To User Mode
```

---

# Exceptions and Mode Switching

Exceptions also trigger Kernel Mode.

---

# Examples

```text
Divide By Zero

Invalid Memory Access

Page Fault
```

---

# Example

```c
int x = 10 / 0;
```

CPU generates exception.

Kernel handles it.

---

# Context Switching vs Mode Switching

Many interviewees confuse these.

---

# Context Switching

Switches:

```text
Process A
     ↓
Process B
```

---

# Mode Switching

Switches:

```text
User Mode
     ↓
Kernel Mode
```

---

# Comparison

| Feature            | Context Switch    | Mode Switch |
| ------------------ | ----------------- | ----------- |
| Switch Between     | Processes/Threads | CPU Modes   |
| PCB Required       | Yes               | No          |
| Scheduler Involved | Usually           | No          |
| Cost               | High              | Lower       |

---

# Linux Perspective

Linux kernel executes in:

```text
Kernel Mode
```

Applications execute in:

```text
User Mode
```

---

# Linux Example

View system calls:

```bash
strace ls
```

Output:

```text
open()

read()

write()

close()
```

These calls trigger Kernel Mode.

---

# Example Flow

Running:

```bash
ls
```

results in:

```text
User Mode
      │
      ▼
open()
      │
      ▼
Kernel Mode
      │
      ▼
File System Access
      │
      ▼
User Mode
```

---

# Memory Protection

User processes cannot access kernel memory.

---

# Example

```text
Kernel Space
```

may contain:

```text
Page Tables

Device Drivers

Scheduler Data
```

Applications cannot directly access it.

---

# Address Space Layout

```text
High Address
+----------------------+
| Kernel Space         |
+----------------------+
| User Space           |
+----------------------+
Low Address
```

---

# Security Benefits

User Mode prevents:

```text
Malware

Accidental Crashes

Unauthorized Hardware Access

Memory Corruption
```

---

# RTOS Perspective

RTOS implementations vary.

---

# Small RTOS

Some microcontroller-based RTOS:

```text
No User Mode

No Kernel Mode
```

Everything runs privileged.

---

# Advanced RTOS

Examples:

```text
QNX

SafeRTOS

Integrity
```

support protection levels.

---

# AUTOSAR Perspective

Modern AUTOSAR systems often use:

```text
Memory Protection

Task Protection

Privilege Separation
```

especially on multicore ECUs.

---

# Automotive Example

```text
Infotainment Task

Airbag Task

ABS Task
```

Protection prevents one faulty task from affecting safety-critical tasks.

---

# Real World Analogy

Think of a bank.

---

# User Mode

```text
Customer Area
```

Customers can:

```text
Deposit Money

Withdraw Money
```

but cannot access the vault.

---

# Kernel Mode

```text
Bank Vault
```

Only authorized employees can enter.

---

# Interview Questions

## Q1. What is User Mode?

User Mode is a restricted execution mode where applications run with limited privileges.

---

## Q2. What is Kernel Mode?

Kernel Mode is a privileged execution mode where the operating system has full access to hardware and system resources.

---

## Q3. Why do Operating Systems use User Mode and Kernel Mode?

To provide:

* Security
* Protection
* Stability

---

## Q4. What causes a switch from User Mode to Kernel Mode?

* System Calls
* Interrupts
* Exceptions

---

## Q5. Can User Mode directly access hardware?

No.

It must use system calls.

---

## Q6. What is the difference between Context Switching and Mode Switching?

Context Switching changes processes/threads.

Mode Switching changes CPU privilege levels.

---

## Q7. Which mode executes device drivers?

Kernel Mode.

---

## Q8. Does every system call cause a mode switch?

Yes.

Execution enters Kernel Mode.

---

# ⚠️ Common Interview Trap

Question:

```text
Is User Mode slower than Kernel Mode?
```

Answer:

```text
Not necessarily.
```

The performance cost comes from:

```text
Mode Switching
```

and not from User Mode itself.

---

# 📝 Quick Revision

```text
User Mode
---------
Limited Privileges

No Hardware Access

Applications Run Here

Kernel Mode
-----------
Full Privileges

Hardware Access

OS Runs Here

Mode Switch Triggers
--------------------
System Calls

Interrupts

Exceptions

Examples
--------
read()

write()

fork()

exec()

User Mode
     ↓
Kernel Mode
     ↓
User Mode
```

---

# 🎯 Key Takeaway

User Mode and Kernel Mode form the foundation of operating system security and protection.

Applications execute in User Mode with restricted privileges, while the Operating System executes in Kernel Mode with full access to hardware resources.

System Calls, Interrupts, and Exceptions provide controlled transitions between these modes, allowing modern operating systems to remain secure, stable, and reliable.

Understanding User Mode and Kernel Mode is essential before learning:

* System Calls
* Process Scheduling
* Interrupt Handling
* Memory Protection
* Linux Kernel Internals
* Device Drivers
* RTOS Protection Mechanisms
