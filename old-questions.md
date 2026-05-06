## 2082 Bhadra

**Question 1** [2+4]
Difference between MBR and GPT Partitions. How does an operating system provide abstraction to user level application from underlying hardware? Explain.

---

**Question 2** [3+6]
Describe the various states of the process. Schedule the following set of processes according to HRRN and Round Robin algorithm (Time quantum: 4).

| Process | Arrival time | Burst time |
| ------- | ------------ | ---------- |
| A       | 0            | 12         |
| B       | 2            | 8          |
| C       | 5            | 7          |
| D       | 10           | 9          |

(i) Draw Gantt Chart
(ii) Find average turnaround time and waiting time for each scheduling algorithm.

---

**Question 3**

**a)** [1+5] Define race condition. Explain how producer-consumer problem can be solved using semaphore with its respective pseudo-code implementations.

**b)** [7] Consider a system with 5 concurrent processes (P₀, P₁, P₂, P₃, P₄) and 4 resources (R₀, R₁, R₂, R₃) types in the system are 6, 4, 4, 2 respectively. Current allocation and maximum need/claim table are as follows:

| Process | R₁  | R₂  | R₃  | R₄  | R₁  | R₂  | R₃  | R₄  |
| ------- | --- | --- | --- | --- | --- | --- | --- | --- |
| P₀      | 2   | 0   | 1   | 1   | 3   | 2   | 1   | 1   |
| P₁      | 1   | 1   | 0   | 0   | 1   | 2   | 0   | 2   |
| P₂      | 1   | 1   | 0   | 0   | 1   | 1   | 2   | 0   |
| P₃      | 1   | 0   | 1   | 0   | 3   | 2   | 1   | 0   |
| P₄      | 0   | 1   | 0   | 1   | 2   | 1   | 0   | 1   |

Use Banker's algorithm to claim that the system is in safe state and show the safe sequence.

---

**Question 4**

**a)** [1+2+4] What is RAID? Explain how Write Ahead Logging (WAL) helps to achieve the concept of stable storage. A NVMe SSD with capacity of 2 Tera Bytes costs NPR. 15,000 and A SATA SSD with capacity of 1 Tera Bytes cost NPR. 5,500. Now, calculate the cost of storing a file with capacity of 160 Mega Bytes on each device. Which device is cost efficient and by how much? Explain.

**b)** [5] Consider the following page-reference string: 7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2, 1, 2, 0, 1, 7, 0, 1. Assuming 3 frames, how many page faults would occur for the following page replacement algorithms: (i) FIFO (ii) Optimal (iii) LRU.

---

**Question 5** [1+3]
What is file attribute? Describe different file allocation methods.

---

**Question 6** [3]
Explain the types of attacks with suitable examples.

---

**Question 7** [4]
Explain about the Type 1 and Type 2 hypervisors in virtualization.

---

**Question 8** [3]
List any 2 key features of OS you studied as case study and explain how they contribute to its performance or usability.

---

**Question 9** [2×3]
Write short notes on: (Any Two)

a) Kubernetes and Docker
b) Thrashing
c) Sandboxing
d) PowerShell
