## Operating System - Model Questions

**1.** Define Bootloader. Explain any 2 types of boot mechanism. How does an operating system act as Extended machine? Explain. **[1+ 3+4]**

**2.** What are the advantages of multithreading? For given process, draw a Gantt Chart and calculate average waiting time for: FCFS and Round Robin (with Quantum Time = 4). Their arrival time, service time in milliseconds. **[2+5]**

| Processes | AT  | BT  |
| --------- | --- | --- |
| P1        | 0   | 3   |
| P2        | 2   | 6   |
| P3        | 4   | 4   |
| P4        | 6   | 5   |
| P5        | 8   | 2   |

**3. a)** What is Peterson's Solution? Explain solution of Reader-Writer problem using semaphore with its respective pseudo-code implementations. **[2+5]**

**3. b)** Under what condition does the solution to the Dining philosopher using semaphore leads to a deadlock conditions? Consider a system with 5 processes (p0, p1, p2, p3, p4) and 4 resource types (R0, R1, R2, R3). The number of instances of each resource type in the systems are: 9, 7, 6, 4 respectively. Allocation table and Maximum claim table are shown below. Is the state safe? If so, show the safe execution of the processes. **[2+6]**

**Allocation Table:**

|        | R0  | R1  | R2  | R3  |
| ------ | --- | --- | --- | --- |
| **P0** | 3   | 1   | 2   | 2   |
| **P1** | 2   | 2   | 1   | 1   |
| **P2** | 2   | 2   | 1   | 0   |
| **P3** | 1   | 0   | 1   | 0   |
| **P4** | 1   | 2   | 0   | 1   |

**Maximum Need Table:**

|        | R0  | R1  | R2  | R3  |
| ------ | --- | --- | --- | --- |
| **P0** | 4   | 3   | 2   | 2   |
| **P1** | 2   | 3   | 1   | 3   |
| **P2** | 2   | 2   | 4   | 2   |
| **P3** | 3   | 2   | 1   | 0   |
| **P4** | 2   | 1   | 0   | 1   |

**4. a)** Explain any two approaches that helps to achieve the concept of stable storage. An HDD Disk with capacity of 512 Giga Bytes and an SSD disk with capacity of 256 Giga Bytes cost NPR. 3,500 and NPR 5,600 respectively. Now, calculate the cost of storing a 300 MB file on each disk. Which disk is cost efficient? **[4+3]**

**4. b)** Given references to the following pages by a program: 1, 2, 3, 2, 1, 5, 2, 1, 6, 2, 5, 6, 3, 1, 3, 6, 1, 2, 4, 3. How many page faults will occur if the program has 4-page frames available to it and use LRU, FIFO and Optimal page replacement algorithm. **[5]**

**5.** Explain the advantages and disadvantages of a contiguous file allocation scheme? **[3]**

**6.** Explain private and public key cryptography with examples. **[4]**

**7.** Explain Hypervisors and its types with examples? **[4]**

**8.** Explain any one functions of OS you studied as case study with its contributions. **[3]**

**9.** Write short notes on (any 2): **(2\*2=4)**

- i. Dockers and Kubernetes
- ii. Secure Boot
- iii. Sandboxing
- iv. WSL
