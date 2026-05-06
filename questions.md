# Past Questions — Operating System

## 1 Introduction (6 hours)

### 1.2 OS as an extended machine and resource manager

- How does an operating system provide abstraction to user level application from underlying hardware? Explain. [4 marks] (2082 Bhadra)

### 1.9 Bootloader, MBR/GPT, UEFI and legacy boot

- Explain the difference between MBR and GPT Partitions. [2 marks] (2082 Bhadra)

---

## 2 Process Management (7 hours)

### 2.1 Process description, states and control

- Describe the various states of the process. [3 marks] (2082 Bhadra)

### 2.2.4 Round Robin (RR)

- Schedule the following set of processes according to Round Robin algorithm (Time quantum: 4). Draw Gantt Chart and find average turnaround time and waiting time. [3 marks] (2082 Bhadra)

| Process | Arrival time | Burst time |
| ------- | ------------ | ---------- |
| A       | 0            | 12         |
| B       | 2            | 8          |
| C       | 5            | 7          |
| D       | 10           | 9          |

### 2.2.5 Highest Response Ratio Next (HRRN)

- Schedule the following set of processes according to HRRN algorithm. Draw Gantt Chart and find average turnaround time and waiting time. [3 marks] (2082 Bhadra)

| Process | Arrival time | Burst time |
| ------- | ------------ | ---------- |
| A       | 0            | 12         |
| B       | 2            | 8          |
| C       | 5            | 7          |
| D       | 10           | 9          |

---

## 3 Process Communication and Synchronization (10 hours)

### 3.1 Principles of concurrency, race condition, critical region

- Define race condition. [1 mark] (2082 Bhadra)

### 3.4 Classical problems of synchronization: Producer-consumer problem

- Explain how the producer-consumer problem can be solved using semaphore with its respective pseudo-code implementations. [5 marks] (2082 Bhadra)

### 3.5 Deadlock: Prevention, ignorance, avoidance, detection and recovery

- Consider a system with 5 concurrent processes (P₀, P₁, P₂, P₃, P₄) and 4 resources (R₀, R₁, R₂, R₃) types in the system are 6, 4, 4, 2 respectively. Current allocation and maximum need/claim table are as follows:

| Process | R₁  | R₂  | R₃  | R₄  | R₁  | R₂  | R₃  | R₄  |
| ------- | --- | --- | --- | --- | --- | --- | --- | --- |
| P₀      | 2   | 0   | 1   | 1   | 3   | 2   | 1   | 1   |
| P₁      | 1   | 1   | 0   | 0   | 1   | 2   | 0   | 2   |
| P₂      | 1   | 1   | 0   | 0   | 1   | 1   | 2   | 0   |
| P₃      | 1   | 0   | 1   | 0   | 3   | 2   | 1   | 0   |
| P₄      | 0   | 1   | 0   | 1   | 2   | 1   | 0   | 1   |

Use Banker's algorithm to claim that the system is in safe state and show the safe sequence. [7 marks] (2082 Bhadra)

---

## 4 I/O and Memory Management (9 hours)

### 4.1.4 RAID

- What is RAID? [1 mark] (2082 Bhadra)

### 4.1.5 Concept of stable storage, cost per bit comparison

- Explain how Write Ahead Logging (WAL) helps to achieve the concept of stable storage. [2 marks] (2082 Bhadra)
- A NVMe SSD with capacity of 2 Tera Bytes costs NPR. 15,000 and A SATA SSD with capacity of 1 Tera Bytes cost NPR. 5,500. Now, calculate the cost of storing a file with capacity of 160 Mega Bytes on each device. Which device is cost efficient and by how much? Explain. [4 marks] (2082 Bhadra)

### 4.2.3 Page replacement algorithms (FIFO, LRU, LFU), page fault and hit ratio

- Consider the following page-reference string: 7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2, 1, 2, 0, 1, 7, 0, 1. Assuming 3 frames, how many page faults would occur for the following page replacement algorithms: (i) FIFO (ii) Optimal (iii) LRU. [5 marks] (2082 Bhadra)

### 4.2.5 Thrashing

- Write a short note on Thrashing. [3 marks] (2082 Bhadra)

---

## 5 File Systems (3 hours)

### 5.1 File concepts: Name, structure, types, access, attributes, operations

- What is a file attribute? [1 mark] (2082 Bhadra)

### 5.3 File system implementation: Inodes, allocation methods (Contiguous, linked, indexed)

- Describe different file allocation methods. [3 marks] (2082 Bhadra)

---

## 6 Security and System Administration (3 hours)

### 6.1 OS security: Cryptography, multi-factor authentication (MFA), secure boot and sandboxing

- Explain the types of attacks with suitable examples. [3 marks] (2082 Bhadra)
- Write a short note on Sandboxing. [3 marks] (2082 Bhadra)

---

## 7 Hypervisors and Virtual Systems (4 hours)

### 7.1 Hypervisors: Type 1 and Type 2

- Explain about the Type 1 and Type 2 hypervisors in virtualization. [4 marks] (2082 Bhadra)

### 7.3 Container virtualization: Docker and Kubernetes

- Write a short note on Kubernetes and Docker. [3 marks] (2082 Bhadra)

### 7.4 PowerShell and Windows Subsystem for Linux (WSL)

- Write a short note on PowerShell. [3 marks] (2082 Bhadra)

---

## 8 Overview of Contemporary OS (3 hours)

### 8.1 Windows and Linux-based OS

- List any 2 key features of the OS you studied as a case study and explain how they contribute to its performance or usability. [3 marks] (2082 Bhadra)
