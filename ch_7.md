# 7 Hypervisors and Virtual Systems

## Virtualization

Virtualization is the process of creating a virtual representation of physical hardware such as servers, storage, and networks. It allows multiple virtual machines (VMs) to run on a single physical machine, each with its own operating system and applications. Before virtualization, most computers performed a single task at a time, wasting much of their processing power. Virtualization enables full utilization of hardware resources by running several virtual systems on one physical host.

Virtualization is a key technology for providing Infrastructure as a Service (IaaS) in cloud computing, where users access remote computing resources without owning dedicated hardware. Cloud providers use virtualization to split large servers into many smaller virtual ones, allowing businesses to pay only for the resources they use.

**Importance of Virtualization:**

- **Better Resource Utilization:** Instead of maintaining numerous underused machines, multiple programs or systems run on one computer, maximizing hardware efficiency.
- **Cost Savings:** Companies reduce spending on hardware, power, cooling, and maintenance by using fewer physical machines.
- **Flexibility:** Virtual machines can be easily created, relocated, and resized to suit changing requirements without requiring new hardware.
- **Isolation and Security:** Different applications or systems are isolated from each other, so a failure in one VM does not affect others.
- **Simple Recovery:** Virtual machines can be easily backed up, snapshotted, and restored, enabling quick recovery after failures.

---

# 7.1 Hypervisors: Type 1 and Type 2

> **Explain about the Type 1 and Type 2 hypervisors in virtualization. [4 marks] (2082 Bhadra)**
> **Explain Hypervisors and its types with examples? [4 marks] (Model Question)**

A hypervisor (also called a Virtual Machine Monitor or VMM) is the software layer that creates and manages virtual machines. It serves as an intermediary between the physical hardware and the virtual machines, controlling how VMs access and share the physical resources (CPU, memory, storage, network) of the host computer.

### Type 1 Hypervisor (Bare-Metal Hypervisor)

A Type 1 hypervisor is installed directly onto the physical hardware, without a host operating system sitting in between. It acts as the operating system for the machine itself. Because it interacts directly with the CPU, memory, and storage without going through an intermediary OS, it provides high performance and better isolation between VMs.

Type 1 hypervisors are used in data centers, cloud providers, and enterprise server environments where performance and reliability are critical. They are typically managed through remote consoles or management software rather than a local GUI.

**Examples:** VMware ESXi, Microsoft Hyper-V, Xen, KVM (Kernel-based Virtual Machine).

### Type 2 Hypervisor (Hosted Hypervisor)

A Type 2 hypervisor runs as an application on top of an existing host operating system (such as Windows, macOS, or Linux). It relies on the host OS to manage hardware resources. When a VM requests resources, the hypervisor passes the request through the host OS, which then interacts with the hardware. This additional layer introduces overhead, resulting in lower performance compared to Type 1 hypervisors.

Type 2 hypervisors are easier to install and use, making them suitable for desktops, laptops, development, and testing environments where running multiple operating systems on a personal computer is needed.

**Examples:** Oracle VM VirtualBox, VMware Workstation (Windows/Linux), VMware Fusion (macOS), Parallels Desktop (macOS).

### Comparison

| Feature      | Type 1 (Bare-Metal)             | Type 2 (Hosted)                |
| ------------ | ------------------------------- | ------------------------------ |
| Installation | Directly on hardware            | On top of a host OS            |
| Performance  | High (direct hardware access)   | Moderate (host OS overhead)    |
| Use case     | Data centers, cloud, enterprise | Desktops, development, testing |
| Isolation    | Strong                          | Weaker (depends on host OS)    |
| Examples     | VMware ESXi, Hyper-V, Xen, KVM  | VirtualBox, VMware Workstation |

---

# 7.2 Virtual Machines: Creating Virtual Machine in QEMU/VirtualBox/VMware

A virtual machine (VM) is a software-based emulation of a physical computer. Each VM runs its own full operating system (guest OS) and applications, completely isolated from other VMs on the same host. The hypervisor allocates CPU, memory, storage, and network resources to each VM.

### Common VM Management Tools

**QEMU (Quick Emulator):** An open-source machine emulator and virtualizer. QEMU can emulate different hardware architectures (e.g., running ARM software on x86 hardware). When combined with KVM on Linux, it provides near-native performance. It is commonly used in Linux environments and for embedded system development.

**VirtualBox:** A free, open-source, cross-platform Type 2 hypervisor by Oracle. It supports a wide range of guest operating systems and provides a user-friendly GUI. VirtualBox is popular for personal use, learning, and development environments.

**VMware Workstation/Fusion:** Commercial Type 2 hypervisors by VMware. VMware Workstation runs on Windows and Linux, while VMware Fusion runs on macOS. They offer advanced features such as snapshots, cloning, shared virtual networks, and integration with VMware's enterprise products.

### General Steps to Create a Virtual Machine

1. Open the hypervisor application (VirtualBox, VMware, etc.).
2. Create a new VM and specify the guest OS type and version.
3. Allocate hardware resources — RAM, CPU cores, and virtual disk size.
4. Attach an installation ISO image of the desired operating system.
5. Boot the VM and install the guest OS as you would on physical hardware.
6. Install guest additions/tools for improved performance and integration (shared folders, clipboard sharing, display scaling).

---

# 7.3 Container Virtualization: Docker and Kubernetes

> **Write a short note on Kubernetes and Docker. [3 marks] (2082 Bhadra, Model Question)**

### Containerization Concepts

Containerization is OS-level virtualization that creates multiple isolated units called containers in user space. Unlike VMs, containers share the same host kernel but are isolated from each other through private namespaces and resource control mechanisms (cgroups) at the OS level.

In VM-based virtualization, a full operating system runs on top of virtualized hardware in each instance, introducing significant overhead. Containers, in contrast, implement isolation of processes at the OS level, avoiding this overhead. Containers do not require pre-allocated RAM — memory is allocated dynamically during container creation. This results in better resource utilization and much faster boot-up times (milliseconds/seconds vs. minutes for VMs).

### Virtual Machines vs. Containers

| Feature              | Virtual Machines             | Containers                          |
| -------------------- | ---------------------------- | ----------------------------------- |
| Virtualization layer | Hardware (via hypervisor)    | OS (via container engine)           |
| OS requirement       | Each VM runs a full guest OS | All containers share host OS kernel |
| Resource usage       | High (full OS overhead)      | Low (only app and dependencies)     |
| Startup time         | Minutes (booting full OS)    | Milliseconds to seconds             |
| Isolation            | Strong (hardware-level)      | Process-level (namespaces, cgroups) |
| Size                 | Gigabytes                    | Megabytes                           |

### Docker

Docker is an open-source platform that enables developers to package applications along with all their dependencies into containers. A Docker container is a lightweight, standalone, executable package that contains everything needed to run an application — code, runtime, libraries, and system tools.

**Key Components:**

- **Containers:** Running instances of Docker images. Each container is isolated and has its own filesystem, networking, and process space.
- **Images:** Read-only templates used to create containers. An image includes the application code, dependencies, and configuration. Images are built in layers for efficiency.
- **Docker Engine:** The core runtime that creates and runs containers on the host operating system. It has a client-server architecture.
- **Docker Hub:** A public registry (repository) where developers can share and pull pre-built container images.

**Docker Architecture:** Docker uses a client-server architecture. The Docker client communicates with the Docker Daemon (running on the Docker Host) using REST APIs. The `docker build` command tells the Daemon to build an image from a Dockerfile. The `docker pull` command pulls an image from Docker Hub. The `docker run` command creates and starts a container from an image.

### Kubernetes (K8s)

Kubernetes is an open-source container orchestration system for automating the deployment, scaling, and management of containerized applications. Originally developed by Google, it is now maintained by the Cloud Native Computing Foundation (CNCF).

While Docker builds and runs individual containers, Kubernetes manages containers at scale across clusters of machines. It acts as a control plane that monitors container health, performs self-healing (restarting crashed containers), handles load balancing, manages rolling updates, and performs auto-scaling based on the desired state defined in configuration files (YAML).

**Why Kubernetes:** When applications involve hundreds or thousands of containers distributed across machines, manual management becomes impractical. Kubernetes provides desired-state management — you declare how you want things to be, and Kubernetes continuously works to ensure they stay that way.

---

# 7.4 PowerShell and Windows Subsystem for Linux (WSL)

> **Write a short note on PowerShell. [3 marks] (2082 Bhadra)**
> **Write a short note on WSL. [2 marks] (Model Question)**

### PowerShell

PowerShell is a cross-platform task automation and configuration management framework developed by Microsoft. It combines a command-line shell, a scripting language built on the .NET Framework, and a configuration management framework.

Unlike traditional shells that work with plain text, PowerShell works with .NET objects, making it more powerful for system administration. It can automate the full VM lifecycle (creation, configuration, snapshots, deletion), perform bulk operations on system resources, and integrate into DevOps pipelines. PowerShell is faster and more powerful than GUI-based tools for advanced administrative tasks.

PowerShell is available on Windows, Linux, and macOS. On Windows, it provides deep integration with the operating system and can manage Active Directory, Windows services, registry, file systems, and network configuration through a consistent scripting interface.

### Windows Subsystem for Linux (WSL)

WSL lets you run a full Linux environment inside Windows without using a traditional virtual machine or dual-boot setup. It enables developers and users to access Linux command-line tools, utilities, and applications alongside their Windows applications with minimal overhead.

**WSL 1:** Acted as a compatibility/translation layer. When a Linux binary made a system call (e.g., `open`, `fork`), the WSL driver intercepted it and translated it into the equivalent Windows NT kernel system call. Linux binaries ran in special "pico processes" that allowed direct interaction with the Windows kernel via this translation driver. WSL 1 had limitations with full system call compatibility.

**WSL 2:** Uses a lightweight utility virtual machine running a genuine Linux kernel. Because it runs a real Linux kernel, all Linux system calls are handled natively, providing full system call compatibility and significantly better performance for file I/O and networking. Despite using a VM, WSL 2 provides a lightweight, seamless experience with fast startup times.

WSL provides access to the Windows filesystem from Linux via `/mnt/c/` and supports running both Windows and Linux commands together. Output can be piped between PowerShell and Linux utilities.

---

# 7.5 Performance Optimization and Security in Virtualized Environments

### Factors Affecting Performance

**Hardware Resources:** CPU overcommitment (allocating more virtual CPUs than physical cores) can lead to contention. RAM bottlenecks cause swapping or crashes. Shared I/O (disk, network) introduces latency when multiple VMs compete for the same physical resources.

**Hypervisor Overhead:** Type 2 hypervisors have more overhead due to their dependence on the host OS layer. Type 1 hypervisors perform closer to native hardware since they access resources directly.

**Storage I/O Latency:** VMs using virtual disks on HDDs perform poorly compared to SSDs. Use of NVMe storage significantly improves disk I/O performance in virtualized environments.

**Nested Virtualization:** Running a VM inside another VM introduces additional delay and overhead. It is not recommended unless explicitly supported by the hypervisor and hardware.

### Security Concerns

**VM Escape:** A critical vulnerability where a malicious process inside a VM breaks out of the virtual environment and gains access to the host system or other VMs. Example: VENOM vulnerability (CVE-2015-3456) exploited a flaw in the virtual floppy drive controller.

**Hypervisor Exploits:** If the hypervisor itself is compromised, all VMs running under it become vulnerable. The hypervisor software must be kept updated, minimal, and hardened.

**Image Vulnerabilities:** Pre-built VM or Docker images downloaded from public repositories may contain embedded malware, backdoors, or outdated packages with known vulnerabilities. Images should be scanned and verified before use.

**Insecure Configuration:** Misconfigured network bridges, shared folders, or open management ports can leak data between VMs or expose internal resources. Administrators must follow best practices including the principle of least privilege and avoiding unnecessary exposure.

### Performance and Security Challenges Summary

**Performance challenges** include resource contention (multiple VMs competing for CPU, RAM, disk, and network), virtualization overhead from the hypervisor layer, I/O bottlenecks in shared environments, and inefficient CPU/I/O scheduling reducing throughput.

**Security challenges** include VM escape attacks, hypervisor vulnerabilities exposing all VMs, malicious or insecure images from untrusted sources, and weak isolation due to poor configuration allowing container-to-host access.
