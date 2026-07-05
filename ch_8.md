# 8 Overview of Contemporary OS

# 8.1 Windows and Linux-based OS

> **List any 2 key features of the OS you studied as a case study and explain how they contribute to its performance or usability. [3 marks] (2082 Bhadra)**
> **Explain any one functions of OS you studied as case study with its contributions. [3 marks] (Model Question)**

### Windows Operating System

Windows is a family of proprietary operating systems developed by Microsoft. Modern versions (Windows 10/11) are built on the Windows NT architecture and use a hybrid kernel. Windows is the most widely used desktop OS in the world, known for its graphical user interface and broad hardware/software compatibility.

**Architecture:** The Windows architecture is divided into two processor access modes:

1. **User Mode:** Where user applications (browsers, word processors) run with restricted access to system resources and memory. Applications cannot directly interact with hardware.
2. **Kernel Mode:** Where the OS core, device drivers, and the kernel reside with unrestricted access to system memory and CPU instructions.

**Key Architectural Components:**

- **Windows Kernel:** Manages low-level operations such as thread scheduling, interrupt handling, and multiprocessor synchronization.
- **Windows Executive:** A set of kernel-mode services that handle memory management, process/thread management, security, and I/O.
- **Hardware Abstraction Layer (HAL):** A software layer that hides differences between hardware platforms, allowing the kernel to remain consistent across different hardware.
- **Environment Subsystems:** Allow Windows to support different types of applications (e.g., Win32, POSIX) by providing the necessary APIs to interact with the kernel.

**Key Features of Windows:**

1. **NTFS File System:** NTFS (New Technology File System) is a journaling file system that maintains a log of changes via the Master File Table (MFT), enabling quick recovery after crashes. It supports access control lists (ACLs) for per-file/folder permissions, transparent compression, file-level encryption (EFS), disk quotas, and alternate data streams (ADS). It supports very large volumes and file sizes.
2. **Plug and Play (PnP):** Windows automatically detects and configures newly connected hardware devices without requiring manual driver installation or system restarts, greatly improving usability.
3. **Windows Registry:** A centralized hierarchical database that stores configuration settings for the OS, hardware, installed applications, and user preferences.
4. **Preemptive Multitasking:** Windows uses preemptive scheduling where the OS decides when to switch between processes, ensuring no single process monopolizes the CPU.

---

### Linux Operating System

Linux is a free, open-source, Unix-like operating system originally created by Linus Torvalds in 1991, inspired by Andrew Tanenbaum's MINIX. Linux refers specifically to the kernel, while complete systems (Ubuntu, Fedora, Debian, Arch Linux) are called Linux distributions.

**History:** UNIX was born at Bell Labs when Ken Thompson wrote a stripped-down version of MULTICS for a PDP-7. Dennis Ritchie joined the effort and designed the C language, in which UNIX was rewritten. AT&T distributed UNIX to universities; UC Berkeley ported it to the VAX (4BSD) and implemented virtual memory, TCP/IP, vi editor, and csh shell. In 1987, Tanenbaum released MINIX for OS classes. In 1991, Linus Torvalds added features to MINIX and released Linux, a full-blown UNIX clone.

**Architecture:** The Linux system is organized in layers:

1. **Hardware Layer:** Physical components (CPU, RAM, storage devices, peripherals).
2. **Kernel:** The monolithic kernel with modular design — the entire core OS service runs in a single address space (kernel space) for high performance, but supports dynamically loadable kernel modules (LKM), allowing drivers and features to be added/removed at runtime without rebooting.
3. **System Libraries:** Predefined functions (e.g., GNU C Library, glibc) that allow applications to access kernel services without needing direct kernel-level access.
4. **Shell and Utilities:** The interface (CLI or GUI) through which users interact with the system.

**Key Kernel Subsystems:**

- **Process Management:** Handles task scheduling using the Completely Fair Scheduler (CFS). Processes are created using `fork()` and programs executed using `exec()`. Child processes that exit before parents collect their status enter the zombie state.
- **Memory Management:** Implements virtual memory with four-level page tables. Distinguishes between three memory zones: ZONE_DMA, ZONE_NORMAL, and ZONE_HIGHMEM. Uses the buddy algorithm for memory allocation.
- **Virtual File System (VFS):** Provides a standard abstraction layer so that different file systems (ext4, XFS, NFS) present a uniform interface to user programs.
- **I/O and Device Drivers:** All devices are treated as files. The major device table maps device operations to appropriate driver functions.
- **Networking:** Supports reliable connection-oriented byte/packet streams and unreliable packet transmission via the socket interface.

**Linux Scheduling:** Three classes of threads exist for scheduling purposes:

- Real-time FIFO (priorities 0–99, non-preemptive)
- Real-time Round Robin (priorities 0–99, preemptive)
- Timesharing (priorities 100–139, normal user processes)

Highest priority = 0, Lowest priority = 140.

**Linux File System:** Uses the ext2/ext4 file system structure. Each disk partition is organized into block groups, each containing a superblock, group descriptor, block bitmap, inode bitmap, inode table, and data blocks. Directories map file names to inode numbers. Inodes store file metadata and pointers to data blocks. Linux supports hard links (multiple names for the same inode) and mounting (attaching file systems to the directory tree).

**Linux Security:** Uses a permission model based on owner, group, and others, with read (r), write (w), and execute (x) permissions for each. Security system calls control user IDs, file permissions, and access control.

**Shells in Linux:** sh (Bourne Shell), csh (C Shell with C-like operators), ksh (Korn Shell combining sh and csh features), bash (Bourne-Again Shell, default on most Linux systems, POSIX-conforming).

---

# 8.2 Embedded and Mobile OS

### Embedded Operating Systems

An embedded OS is a specialized operating system designed to run on embedded systems — dedicated hardware devices with specific, fixed functions. Unlike general-purpose OS, an embedded OS is optimized for a particular task and typically operates under constraints of limited memory, processing power, and energy.

**Characteristics:**

- Small memory footprint and minimal resource usage.
- Fast boot times and deterministic behavior.
- Typically do not allow user-installed applications; functionality is fixed at manufacturing.
- High reliability — must run continuously without failure (e.g., medical monitors, automotive controllers).
- Often have no user interface or only a minimal one (LEDs, simple displays).

**Examples:** Embedded Linux, Windows IoT, VxWorks, QNX, ThreadX.

**Applications:** Automotive ECUs (Engine Control Units), home appliances (washing machines, microwaves), ATMs, medical devices, networking routers, and industrial automation controllers.

### Mobile Operating Systems

A mobile OS is designed specifically for smartphones, tablets, and other handheld devices. It balances rich functionality with power efficiency, limited hardware resources, and touch-based user interfaces. Unlike traditional embedded OS, mobile OS supports general-purpose use with third-party application support.

### Android

Android is an open-source, Linux-based mobile OS developed by Google. It is the most widely used mobile OS globally.

**Architecture (layered):**

1. **Linux Kernel:** Foundation layer providing drivers, memory management, process management, power management, and security.
2. **Hardware Abstraction Layer (HAL):** Interfaces that allow the framework to access hardware capabilities without knowing the specific underlying hardware implementation.
3. **Native Libraries:** C/C++ libraries (e.g., WebKit for web rendering, SQLite for databases, OpenGL for graphics).
4. **Android Runtime (ART):** Provides the execution environment for apps using Ahead-Of-Time (AOT) compilation for improved performance. Replaced the older Dalvik virtual machine.
5. **Application Framework:** High-level Java/Kotlin APIs used by developers (Activity Manager, Notification Manager, Content Providers, Window Manager).
6. **Applications:** Pre-installed and user-downloaded apps at the top layer.

**Key Features:** Open-source nature allows extensive customization by manufacturers; supports multitasking; rich notification system; Google Play Store for app distribution.

### iOS

iOS is a proprietary, Unix-derived (Darwin/XNU kernel) mobile OS developed by Apple exclusively for its devices (iPhone, iPad).

**Architecture (layered):**

1. **Core OS Layer:** Contains the Darwin/XNU kernel (a hybrid kernel combining Mach microkernel with BSD components), managing hardware, memory, filesystems, and low-level security.
2. **Core Services Layer:** Provides fundamental system services and frameworks (iCloud, Core Data, networking, location services).
3. **Media Layer:** Contains technologies for graphics (Core Graphics, Metal), audio (Core Audio), and video processing.
4. **Cocoa Touch Layer:** The highest layer, providing essential frameworks (UIKit, SwiftUI) for building user interfaces, handling touch input, and managing app lifecycle.

**Key Features:** Tight hardware-software integration for optimized performance; strong security model with app sandboxing; consistent user experience across devices; App Store with curated app review process.

---

# 8.3 IoT and RT Operating System

### IoT Operating Systems

An IoT (Internet of Things) OS is a lightweight operating system designed to run on resource-constrained, connected devices such as sensors, actuators, smart home devices, and wearables. IoT devices typically have limited memory (a few KB to a few MB), low processing power, and must operate on minimal energy (often battery-powered for years).

**Requirements of IoT OS:**

- Ultra-small memory footprint (often < 10 KB kernel).
- Low power consumption for battery-operated devices.
- Built-in support for networking protocols (Wi-Fi, Bluetooth, Zigbee, MQTT, CoAP).
- Security features (secure boot, encrypted communication, OTA updates).
- Real-time or near-real-time task responsiveness.

**Examples:**

- **FreeRTOS:** Open-source, market-leading IoT RTOS with a very small footprint (< 10 KB). Supports preemptive and cooperative scheduling, modular design (include only needed features), and integrated AWS IoT cloud connectivity. Ported to 40+ processor architectures. Ideal for simple sensors, wearables, and cost-sensitive consumer devices.
- **Contiki:** Lightweight open-source OS for networked IoT devices, designed for low-power microcontrollers with IPv6 networking support.
- **Zephyr:** A Linux Foundation project providing a small, scalable RTOS for resource-constrained devices with built-in Bluetooth, Wi-Fi, and networking stacks.

### Real-Time Operating Systems (RTOS)

An RTOS is designed for systems where correctness depends not only on the logical result of computation but also on the time at which the results are produced. The primary metric is determinism — guaranteeing that tasks complete within a specific deadline.

**Hard Real-Time vs Soft Real-Time:**

- **Hard Real-Time:** Missing a deadline is catastrophic and may cause system failure or endanger lives. Examples: airbag deployment systems, pacemakers, missile guidance, aircraft flight control systems, nuclear reactor controllers.
- **Soft Real-Time:** Deadlines are important but occasional misses are tolerable with degraded performance. Examples: multimedia streaming, video conferencing, online gaming, live sensor dashboards.

**Key Features of RTOS:**

- **Deterministic Scheduling:** Guarantees that high-priority tasks execute within predictable time bounds. Uses priority-based preemptive scheduling where the highest-priority ready task always runs.
- **Minimal Interrupt Latency:** Time between an interrupt occurring and the OS responding is minimized and bounded.
- **Task Management:** Supports creation, deletion, suspension, and resumption of tasks with priority levels.
- **Inter-Task Communication:** Provides mechanisms like message queues, semaphores, and mutexes for synchronization.
- **Memory Protection:** Prevents tasks from corrupting each other's memory space.

**Examples:**

- **VxWorks:** A proprietary, high-performance commercial RTOS by Wind River for mission-critical and safety-certified systems. Supports symmetric and asymmetric multiprocessing, Type 1 hypervisor virtualization, secure boot, and encryption. Widely used in aerospace (Mars rovers), defense, medical devices, and industrial automation. Provides extensive middleware for networking, file systems, and graphics.
- **QNX:** A microkernel-based commercial RTOS known for high reliability. Used extensively in automotive infotainment systems (e.g., BlackBerry QNX in vehicles), medical devices, and industrial control.
- **FreeRTOS:** Also serves as a general-purpose RTOS for embedded and IoT applications (described above).

---

# 8.4 Robot and Smart Card Operating System

### Robot Operating System (ROS)

ROS (Robot Operating System) is not a traditional operating system but an open-source middleware framework designed for building complex robotic applications. It runs on top of a host OS, typically Linux (Ubuntu). ROS provides the infrastructure for different parts of a robot (sensors, actuators, planning algorithms) to communicate and work together.

**Key Features:**

- **Message-Passing Architecture:** ROS uses a publish-subscribe model where software components (nodes) communicate by publishing messages to topics and subscribing to topics of interest. This decouples components and allows modularity.
- **Hardware Abstraction:** Provides device drivers and standard interfaces for common robot hardware (cameras, LIDARs, motors), allowing developers to write hardware-independent code.
- **Tools and Libraries:** Includes powerful tools for visualization (RViz), simulation (Gazebo), data logging (rosbag), and algorithm libraries for navigation, perception, and manipulation.
- **Package Management:** Software is organized into packages that can be easily shared and reused across the robotics community.
- **Language Support:** Primarily supports C++ and Python, with community-supported bindings for Java (rosjava, used for Android robotics) and other languages.

**ROS 2:** The newer version of ROS designed for production use with real-time capabilities, improved security, support for multi-robot systems, and the DDS (Data Distribution Service) communication middleware replacing the original ROS master architecture.

**Applications:** Autonomous vehicles, industrial robotic arms, drones, humanoid robots, surgical robots, and research platforms.

### Smart Card Operating System

A smart card OS is the most constrained type of operating system, running on a tiny microprocessor chip embedded in smart cards (credit/debit cards, SIM cards, national ID cards, security badges, ePassports). These chips have extremely limited resources — typically a few kilobytes of RAM, tens of kilobytes of ROM, and an 8/16/32-bit processor running at a few MHz.

**Functions of a Smart Card OS:**

- Manages communication between the card and the card reader using the APDU (Application Protocol Data Unit) protocol.
- Provides secure storage and controlled access to sensitive data (cryptographic keys, PINs, personal information).
- Supports cryptographic operations (encryption, decryption, digital signatures) on-card.
- Enables loading and execution of multiple independent applications (applets) on a single card, each isolated from the others by firewalls.

**Major Smart Card OS Platforms:**

1. **Java Card:** The globally dominant smart card platform based on a subset of the Java programming language. It runs a Java Card Virtual Machine (JCVM) on the chip, allowing developers to write portable applets in Java. Applications are isolated by a firewall mechanism that prevents one applet from accessing another's data. Java Card uses the GlobalPlatform standard for card management (loading, deleting, and managing applets). Widely used in SIM cards, EMV payment cards, and government ID cards.

2. **MULTOS:** A multi-application smart card OS with a formally proven secure kernel. Applications are written in MEL (MULTOS Executable Language), C, or Java and run on the MULTOS Executive virtual machine. It uses a certificate-based loading model (applications must be signed by the MULTOS Certificate Authority before loading onto the card), providing strong security assurance. MULTOS is prominent in UK and European banking applications.

**Key Characteristics Common to Smart Card OS:**

- **Extreme Resource Constraints:** Operate within a few KB of RAM and tens of KB of persistent storage.
- **Security-First Design:** Security is the primary design goal. Both platforms meet rigorous Common Criteria security evaluations.
- **Multi-Application Support:** Multiple independent applets can coexist on a single chip, isolated by hardware and software firewalls.
- **Standardized Communication:** Use the ISO 7816 standard for communication between the card and the reader.
