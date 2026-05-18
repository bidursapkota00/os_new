---
marp: true
theme: default
paginate: true
style: |
  * {
    box-sizing: border-box;
  }
  /* Slide container */
  section {
    background-color: #fff;
    font-family: 'Times New Roman', Times, serif;
    font-size: 28pt;
    color: black;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    padding: 0;
    padding-bottom: 10pt;
  }

  /* Heading banner */
  section h1 {
    background-color: rgb(25, 107, 36);
    color: white;
    font-family: 'Times New Roman', Times, serif;
    font-size: 44pt;
    margin: 0;
    padding: 8pt;
    text-align: center;
    width: 100%;
  }

  /* Body content fills remaining space */
  section p,
  section ul,
  section ol,
  section pre {
    font-family: 'Times New Roman', Times, serif;
    font-size: 28pt;
    color: black;
    margin: 0;
  }

  section ul {
    text-align: left;
    list-style-type: disc;
    list-style-position: inside;
    padding: 0;
  }

  section ol {
    text-align: left;
    list-style-type: decimal;
    list-style-position: inside;
    padding: 0;
  }

  section ol li::marker {
    font-weight: bold;
  }

  section ul li::marker {
    margin-right: 10pt;
    content: "•  ";
  }

  section pre {
    font-size: 20pt;
  }

  section::after {
    bottom: 5px;
  }

  h1 {
    margin-bottom: 10pt;
  }

  h1 ~ * {
    margin: 0 10pt;
  }

  /* Title slide - no green banner */
  section.title-slide {
    justify-content: center;
    align-items: center;
    padding: 40pt 100pt;
  }

  section.title-slide h1 {
    background-color: transparent;
    color: black;
    font-size: 60pt;
    font-weight: bold;
    text-align: center;
    padding: 0;
    margin-bottom: 30pt;
  }

  section.title-slide p {
    text-align: right;
    font-size: 28pt;
    width: 100%;
    margin: 0;
    line-height: 1.6;
  }

  section p:has(img) {
    display: flex;
    justify-content: center;
    align-items: center;
    flex: 1 1 0;
    min-height: 0;
    margin: 0;
  }

  img {
    max-width: 100%;
    max-height: 100%;
    object-fit: contain;
  }

  marp-pre {
    margin: 10pt;
  }

  blockquote {
    margin-bottom: 20pt;
  }

  section h3 {
    margin-top: 15pt;
    margin-bottom: 15pt;
  }

  section h4 {
    margin-top: 10pt;
    margin-bottom: 10pt;
  }

  table {
    margin: 0;
    padding: 0 10pt;
  }

  th, td {
    border: 1px solid black !important;
  }

  tr {
    background: white !important;
  }

  section ul ul {
    list-style-type: circle;
    margin-left: 30pt;
  }

  section ul ul ul {
    list-style-type: square;
    margin-left: 30pt;
  }

  section ol ol {
    list-style-type: lower-alpha;
    margin-left: 30pt;
  }

  section ol ol ol {
    list-style-type: lower-roman;
    margin-left: 30pt;
  }

  section ul ol,
  section ol ul {
    margin-left: 30pt;
  }

  section li li {
    margin-top: 4pt;
  }

  section ul ul li::marker,
  section ol ul li::marker {
    content: normal;
  }
---

<!-- _class: title-slide -->

# Operating System

ENCT 254

---

# Overview

**Year:** II
**Part:** II

<br>

**Lecture:** 3 cr.  
**Tutorial:** 1 cr.  
**Practical:** 1.5 cr.

---

# Course Objectives

The objective of this course is to familiarize students with the different aspects of operating systems and encourage them to use these ideas in designing operating systems.

---

# Course Contents

### 1 Introduction (6 hours)

- 1.1 Introduction to operating systems
- 1.2 OS as an extended machine and resource manager
- 1.3 History of operating system
- 1.4 Type of operating system: Mainframe, server, personal, smartphone and handheld, IOT and embedded, real-time, smart-card
- 1.5 Operating system components: Kernel, shell, utilities, applications

---

# Course Contents

### 1 Introduction (6 hours)

- 1.6 Types of OS kernel: Monolithic, micro, nano, layered, hybrid, exo-kernel
- 1.7 System calls, shell commands, shell programming
- 1.8 POSIX standard
- 1.9 Bootloader, MBR/GPT, UEFI and legacy boot

---

# Course Contents

### 2 Process Management (7 hours)

- 2.1 Process description, states and control
- 2.2 Scheduling algorithms
  - 2.2.1 First Come First Serve (FCFS)
  - 2.2.2 Shortest Job First (SJF)
  - 2.2.3 Shortest Remaining Time (SRT)
  - 2.2.4 Round Robin (RR)
  - 2.2.5 Highest Response Ratio Next (HRNN)
  - 2.2.6 Completely Fair Scheduler (CFS) used in Linux

---

# Course Contents

### 2 Process Management (7 hours)

- 2.3 Threads and thread scheduling

---

# Course Contents

### 3 Process Communication and Synchronization (10 hours)

- 3.1 Principles of concurrency, race condition, critical region
- 3.2 Mutual exclusion, semaphores, and mutex
- 3.3 Message passing and monitors
- 3.4 Classical problems of synchronization: Readers-writers problem, producer-consumer problem, dining philosopher problem
- 3.5 Deadlock: Prevention, ignorance, avoidance, detection and recovery

---

# Course Contents

### 4 I/O and Memory Management (9 hours)

- 4.1 I/O management
  - 4.1.1 Principles of I/O hardware and software
  - 4.1.2 I/O software layer
  - 4.1.3 Disk technologies: Magnetic disk, SSD, NVMe storage
  - 4.1.4 RAID
  - 4.1.5 Concept of stable storage, cost per bit comparison

---

# Course Contents

### 4 I/O and Memory Management (9 hours)

- 4.2 Memory Management
  - 4.2.1 Memory address, swapping and managing free memory space
  - 4.2.2 Virtual memory management, paging, segmentation
  - 4.2.3 Page replacement algorithms (FIFO, LRU, LFU), page fault and hit ratio
  - 4.2.4 Allocation of frames
  - 4.2.5 Thrashing

---

# Course Contents

### 5 File Systems (3 hours)

- 5.1 File concepts: Name, structure, types, access, attributes, operations
- 5.2 Directory structures: Paths and hierarchies (Linux/Windows)
- 5.3 File system implementation: Inodes, allocation methods (Contiguous, linked, indexed)
- 5.4 File system performance: Factors affecting efficiency
- 5.5 Example file systems: NTFS, EXT4, FAT32, NFS

---

# Course Contents

### 6 Security and System Administration (3 hours)

- 6.1 OS security: Cryptography, multi-factor authentication (MFA), secure boot and sandboxing
- 6.2 Access control: Policies, lists, and OS support
- 6.3 System administration: User management, environment setup and tools (AWK, shell scripts, make)

---

# Course Contents

### 7 Hypervisors and Virtual Systems (4 hours)

- 7.1 Hypervisors: Type 1 and type 2
- 7.2 Virtual machines: Creating virtual machine in Qemu/Virtual box/VMWare
- 7.3 Container virtualization: Docker and Kubernetes
- 7.4 Power shell and windows subsystem for LINUX (WSL)
- 7.5 Performance optimization and security in virtualized environments

---

# Course Contents

### 8 Overview of Contemporary OS (3 hours)

- 8.1 Windows and Linux-based OS
- 8.2 Embedded and mobile OS
- 8.3 IoT and RT operating system
- 8.4 Robot and smart card operating system

---

# Tutorials (15 hours)

1. Unix shell programs to do a variety of tasks
2. Problems on scheduling algorithms
3. Problems on page replacement algorithms
4. Problems on deadlock
5. Problems on segmentation and paging
6. Comprehensive study on storage technologies with cost/bit and speed comparisons
7. Study on process management/memory management/IO management/security/file system of a selected OS

---

# Practical (22.5 hours)

1. Basic Unix commands
2. Shell Programming
3. Implementation of the ls and grep commands
4. Programs using the I/O system calls of the UNIX operating system
5. Implementation of scheduling algorithms and the producer-consumer problem using semaphores
6. Implementation of some memory management schemes such as paging and segmentation
7. Term Project

---

# Academic Calender

**Semester Start:** Jestha 4
**Semester End:** Bhadra 11

**Theory class:** Monday, Wednesday
**Practical class:** Monday

**First Exam:** Asar 11
**Second Exam:** Bhadra 1
**Test:** Weekly

---

# Final Exam

The questions will cover all the chapters in the syllabus. The evaluation scheme will be as indicated in the table below:

| Chapter | Hours | Marks Distribution\* |
| ------- | ----- | -------------------- |
| 1       | 6     | 8                    |
| 2       | 7     | 10                   |
| 3       | 10    | 13                   |
| 4       | 9     | 12                   |
| 5       | 3     | 4                    |

---

# Final Exam

| Chapter   | Hours  | Marks distribution\* |
| --------- | ------ | -------------------- |
| 6         | 3      | 4                    |
| 7         | 4      | 5                    |
| 8         | 3      | 4                    |
| **Total** | **45** | **60**               |

_There may be minor deviation in marks distribution._

---

# Internal Marks

| Criteria               | Marks |
| ---------------------- | ----- |
| Homework               | 10    |
| Attendance             | 4     |
| First Term + Unit Test | 10    |
| Second Term            | 10    |
| Other Activities       | 6     |

---

# Practical Marks

| Criteria     | Marks |
| ------------ | ----- |
| Lab Report   | 10    |
| Attendance   | 10    |
| Presentation | 5     |

---

# References

1. Tanenbaum, A.S., Bos, H. (2024). Modern Operating Systems. 3rd Edition. PHI.
2. Stalling, W. (2008). Operating Systems. 6th Edition. Pearson Education.
3. Chaturvedi, A., Rai, B.L. (2017). UNIX and Shell Programming. University Science Press.
