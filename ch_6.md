# 6 Security and System Administration

# 6.1 OS Security

Computer security refers to protecting computer systems (hardware and software) and data from unauthorized access, threats, and attacks. The goal of operating system security is to ensure confidentiality, integrity, and availability of system resources while providing legitimate users with seamless access.

### CIA Triad

The three fundamental goals of information security are:

1. **Confidentiality:** Preventing disclosure of sensitive information to unauthorized people, resources, or processes.
2. **Integrity:** Protecting system information or processes from intentional or accidental modification.
3. **Availability:** Ensuring that systems and data are accessible by authorized users when needed.

A security breach occurs when an intruder successfully bypasses security mechanisms. Breach of confidentiality involves unauthorized reading of data (e.g., theft of credit card information). Breach of integrity involves unauthorized modification of data (e.g., tampering with financial records). Breach of availability involves unauthorized disruption of access (e.g., DoS attacks, ransomware encrypting files).

---

## Cryptography

> **Explain private and public key cryptography with examples. [4 marks] (Model Question)**

Cryptography is the practice of converting readable data (plaintext) into an unreadable format (ciphertext) using encryption algorithms. It ensures data security during storage and transmission.

**Plaintext** is the original readable message before encryption. **Ciphertext** is the scrambled, unreadable output after encryption. **Encryption** converts plaintext into ciphertext using a cryptographic algorithm and a key. **Decryption** is the reverse process, converting ciphertext back into plaintext. A **key** is a piece of information (typically a string of bits) that controls the encryption and decryption process.

### Symmetric Encryption (Secret Key Cryptography)

Uses a single shared key for both encryption and decryption. It is fast and efficient, making it ideal for bulk data encryption (e.g., full-disk encryption, file storage). The primary challenge is securely distributing the shared key between parties. If the key is compromised, all encrypted data becomes vulnerable. Example: AES (Advanced Encryption Standard) used in Wi-Fi security (WPA2).

**How it works:** Sender encrypts plaintext using a secret key → Ciphertext is transmitted → Receiver decrypts ciphertext using the same secret key → Original plaintext is recovered.

### Asymmetric Encryption (Public Key Cryptography)

Uses two mathematically related keys: a **public key** (shared with everyone, used to encrypt data) and a **private key** (kept secret, used to decrypt data). It is more secure than symmetric encryption because the private key never needs to be shared, but it is slower. It solves the key distribution problem inherent in symmetric encryption. Example: RSA encryption used in secure email communication (PGP), end-to-end encryption in messaging apps like WhatsApp.

**How it works:** Sender encrypts plaintext using the receiver's public key → Ciphertext is transmitted → Receiver decrypts ciphertext using their private key → Original plaintext is recovered. Only the holder of the corresponding private key can decrypt data encrypted with the public key.

### Hash Functions

A hash function is a mathematical algorithm that takes an input of any size and produces a fixed-size output called a hash value or digest. Hash functions are one-way (computationally infeasible to reverse), deterministic (same input always produces the same hash), and exhibit the avalanche effect (a single-bit change in input produces a completely different hash). Examples: SHA-256, MD5. Hash functions are used for password storage, data integrity verification, and digital signatures.

### Digital Signature

A digital signature is an electronic equivalent of a handwritten signature that ensures authenticity (the sender is genuine), integrity (the message has not been altered), and non-repudiation (the sender cannot deny sending it).

**Signing Process:** A hash function (e.g., SHA-256) is applied to the message, generating a fixed-length hash value. The hash is then encrypted using the sender's private key, creating the digital signature. The signature is attached to the message and sent to the recipient.

**Verification Process:** The recipient uses the sender's public key to decrypt the signature, retrieving the original hash. The recipient also computes the hash of the received message independently. If the two hashes match, the message is authentic and untampered. If they do not match, the message has been altered or did not come from the claimed sender.

**Example:** Verifying the authenticity of software downloads (e.g., Windows updates, Linux package managers use GPG signatures).

---

## Classification of Attacks

> **Explain the types of attacks with suitable examples. [3 marks] (2082 Bhadra)**

### A. Passive Attacks

Passive attacks involve monitoring or eavesdropping on transmissions without altering the data or system operation. The goal is to obtain information being transmitted between parties. Passive attacks are difficult to detect because they do not alter data or system behavior.

1. **Eavesdropping:** An attacker intercepts and listens to communications between two parties. It can occur on network traffic, phone conversations, or any form of electronic communication.
2. **Traffic Analysis:** An attacker studies the pattern and flow of communication rather than its content. By analyzing traffic patterns, attackers can determine communication frequency, message lengths, and the identity of communicating parties.

### B. Active Attacks

Active attacks involve modification of the data stream or creation of a false stream, actively interfering with system operation. They are easier to detect than passive attacks because they cause observable changes, but can cause significant damage before being identified.

1. **Masquerade Attack:** One entity pretends to be a different entity to gain unauthorized access. An attacker may use stolen usernames and passwords, forged credentials, or compromised authentication tokens. Solution: Multi-Factor Authentication (MFA).
2. **Replay Attack:** Involves capturing data transmissions and retransmitting them later to produce unauthorized effects. Example: Capturing an encrypted authentication message and replaying it to gain access without knowing the password. Solution: One-Time Passwords (OTP).
3. **Modification of Messages:** Involves capturing messages, altering their content, and transmitting the modified messages. Examples: Changing the amount in a financial transaction, altering the destination address of a message. Solution: Digital Signatures.
4. **Denial of Service (DoS) Attack:** Aims to make a system or network resource unavailable to intended users by overwhelming systems with traffic, exploiting vulnerabilities to crash systems, or consuming resources to prevent legitimate access.

---

## Malware

Malware (malicious software) is any software intentionally designed to cause damage to computers, servers, or networks.

1. **Virus:** Attaches to files and spreads when the file is executed. Requires user action to propagate. Example: "ILOVEYOU" virus spread via email attachments.
2. **Worm:** Self-replicating malware that spreads through networks without user intervention. Example: "WannaCry" ransomware spread through the internet exploiting a Windows vulnerability.
3. **Trojan Horse:** Disguised as a useful program but carries malicious functions such as creating backdoors or stealing data. Example: A fake antivirus software stealing user data.
4. **Spyware:** Secretly collects user data such as keystrokes and browsing history. Example: Keyloggers capturing login credentials.
5. **Ransomware:** Encrypts user files and demands ransom to decrypt them. Example: "CryptoLocker" demanded Bitcoin payments for decryption keys.

---

## Authentication and Multi-Factor Authentication (MFA)

> **Write a short note on Secure Boot. [2 marks] (Model Question)**

Authentication is the process of verifying the identity of a user, process, or device attempting to access a system. Authentication factors include:

1. **Something you know** — Password, PIN, security questions.
2. **Something you have** — Smartphone, security token, smart card.
3. **Something you are** — Biometrics (fingerprint, retina scan, facial recognition).

**Multi-Factor Authentication (MFA)** requires two or more verification factors from different categories to gain access. It adds an extra layer of security beyond traditional password-based login. Even if a password is stolen, an attacker cannot bypass the secondary factors. MFA minimizes risk from password theft or phishing attacks.

**Implementation Examples:** Windows Hello (biometric MFA), Linux PAM (Pluggable Authentication Modules) can integrate OTP-based MFA.

---

## Secure Boot

> **Write a short note on Secure Boot. [2 marks] (Model Question)**

Secure Boot is a firmware-level security mechanism that ensures only trusted software is loaded during the system startup process. It is part of the UEFI specification.

**How it works:** When a device starts, the UEFI firmware checks the digital signature of each piece of boot software (bootloader, OS kernel, critical system files) against a database of trusted keys stored in firmware. Only software with a valid signature from a trusted certificate authority is allowed to boot. Each component in the boot chain verifies the digital signature of the next component before loading it.

The chain of trust starts from hardware-embedded keys that cannot be modified. If any component fails signature verification, the boot process is halted. Secure Boot prevents boot-time malware such as rootkits and bootkits from loading before the operating system. It maintains system integrity from power-on to OS load.

**Examples:** Windows uses Microsoft-signed bootloaders. Linux distributions support Secure Boot via shim + GRUB signed by Microsoft or a distro-specific authority.

---

## Sandboxing

> **Write a short note on Sandboxing. [3 marks] (2082 Bhadra, Model Question)**

Sandboxing is a security mechanism that isolates running programs in a restricted environment with limited access to system resources. A sandbox provides a controlled execution environment where untrusted code can run without affecting the rest of the system. It limits what actions a program can perform, even if the program attempts malicious operations.

**Purpose:** Isolate potentially harmful programs or processes, and prevent applications from modifying system files or accessing sensitive data.

**OS Use Cases:** Running web browsers, PDFs, or unknown executables in sandboxes. Mobile operating systems (Android/iOS) sandbox every app by default, restricting each app to its own environment. Containers (e.g., Docker) act as sandboxed environments at the OS level.

**Techniques used:** Access control (MAC, DAC), virtual machines or containers, capability-based security.

**Examples:** Windows Sandbox provides a temporary virtualized environment for testing apps. AppArmor and SELinux enforce mandatory access control in Linux to implement sandboxing policies.

---

## Firewall

A firewall is a network security device or software that filters and controls traffic between networks based on predefined security rules.

1. **Packet Filtering Firewall:** Inspects individual data packets based on rules (IP address, port number, protocol). It operates at the network layer. Example: A router blocking access to certain websites.
2. **Proxy Firewall:** Acts as an intermediary between internal and external networks, hiding internal network details. It inspects traffic at the application layer. Example: Corporate networks using a proxy to filter internet access.
3. **Stateful Inspection Firewall:** Tracks active connections and allows only trusted packets that are part of an established session. It reduces rule-checking overhead for ongoing connections and blocks unauthorized access, TCP SYN floods, and other connection-based attacks.

---

# 6.2 Access Control: Policies, Lists, and OS Support

Access control is a security technique that regulates who or what can view or use resources in a computing environment. It is one of the most fundamental security mechanisms in any operating system.

### Principles of Access Control

- **Principle of Least Privilege:** Users should be granted only the minimum access rights necessary to perform their job functions.
- **Separation of Duties:** No single individual should have enough access to misuse the system alone.
- **Need-to-Know:** Access to sensitive information is restricted to only those who require it for their specific duties.
- **Defense in Depth:** Multiple layers of access controls are implemented so that if one layer fails, others continue to provide protection.

### Access Control Models

**Discretionary Access Control (DAC):** The owner of a resource determines who can access it. The owner can grant or revoke permissions at their discretion. It is flexible but less secure because users can inadvertently share access. Example: Linux file permissions (rwx for user/group/other).

**Mandatory Access Control (MAC):** A central authority (typically the OS) controls access based on security classification levels. MAC assigns security labels to both subjects (users/processes) and objects (files/resources). Users cannot change these permissions. Used in high-security environments. Example: SELinux, AppArmor.

**Role-Based Access Control (RBAC):** Permissions are assigned to roles (e.g., Administrator, Editor, Viewer) rather than to individual users. Users are assigned to appropriate roles. Simplifies management in large organizations. Example: Windows group policies.

**Attribute-Based Access Control (ABAC):** Makes access decisions based on attributes of users, resources, and environmental conditions (e.g., time of day, location, device type).

**Rule-Based Access Control:** Uses rules defined by the system administrator to determine access. Rules are applied uniformly regardless of identity.

### Protection Domain

A protection domain specifies the resources that a process can access and the operations it can perform. Each process operates within a protection domain that defines its access rights. A domain can be thought of as a collection of access rights, where each right is an ordered pair **(object, rights-set)**. Objects can be hardware resources (CPU, memory, printers) or software resources (files, programs, semaphores). Subjects are the active entities that access objects, including users, processes, and procedures.

### Access Control Mechanisms

**Access Control Matrix:** A theoretical concept that represents all access permissions as a matrix with subjects as rows and objects as columns. Each cell contains the access rights that the subject has for the object. It is rarely implemented directly due to its large size but serves as a conceptual model. ACLs and capability lists are different ways of sparsely representing this matrix.

**Access Control Lists (ACLs):** Lists associated with objects that specify which subjects can access them and what operations they can perform. ACLs store permissions with each resource, listing all users and their allowed actions. They are easy to manage for systems with many users and few resources. However, finding all resources a particular user can access requires checking ACLs on all resources.

**Capability Lists (C-Lists):** Lists associated with subjects that specify which objects they can access. Capability lists store permissions with each user, listing all resources they can access. They make it easy to see all resources a particular user can access. However, finding all users who can access a particular resource requires checking all capability lists.

### OS Support for Access Control

**Linux/Unix:** Uses DAC via user/group/other permission bits (rwx). Supports ACLs for fine-grained access control. Can implement MAC using SELinux or AppArmor.

**Windows:** Uses ACLs extensively — DACLs (Discretionary ACLs) for allowing/denying access and SACLs (System ACLs) for auditing. Supports RBAC via user roles and group policies. Enforces capability-like security tokens during process execution.

**Android:** Uses sandboxing and UID-based permissions. Supports permissions per app, combining DAC and MAC.

---

# 6.3 System Administration: User Management, Environment Setup and Tools

System administration involves the management of computer systems including hardware, software, networks, and users within an organization. A system administrator's responsibilities include applying OS updates and patches, installing and configuring hardware/software, managing user accounts, performance tuning, maintaining documentation, ensuring security, performing backups, analyzing system logs, and troubleshooting problems.

---

## User Account Management

Operating systems provide a method for creating multiple user accounts on a single installation. Each account can be configured and customized based on individual needs. User-specific data such as desktop settings, application preferences, shortcuts, and data files are stored separately for each account.

### User Account Types

**Standard User Account:** The default type of account that provides basic permissions for common daily tasks. Standard users can launch applications, create documents, modify basic system settings, change personal settings (password, wallpaper, screen saver), access removable media, connect to networks, and personalize display settings. They cannot install system-wide software or modify other users' accounts.

**Administrator Account:** Has full permissions on the system, including all standard user permissions plus the ability to install new software and hardware, modify system-wide configuration, access files in secure locations, configure the firewall, perform complete system backup and restore, and create, remove, or modify other user accounts.

**Guest Account:** Designed for users who require temporary access to a computer. Guest users have a very limited set of permissions — they cannot access other users' files or perform system-wide tasks. The built-in Guest account is disabled by default for security reasons.

Each user account includes a user profile (OS preferences like wallpaper and shortcuts), application settings, a user data folder, security privileges, and file system permissions that define what actions the user can take on which files.

### Common Account Management Operations

Administrators can change passwords, change account names, remove passwords, change account pictures, set up parental controls, change account types, and delete accounts.

---

## Environment Setup for New Users

Setting up an operational environment for a new user involves ensuring the OS and minimum usable application packages and utilities are installed. The required user accounts are created so new users can log in with their username and password. User-friendly modules like user-setup can be created to enable users to change their environment easily — applications can be added or removed without the user having to learn editors or shell languages. New applications can be installed and made accessible to users via such setup utilities.

---

## Shell Scripting

Shell scripting refers to writing a series of commands in a file, intended to be executed by a command-line interpreter (shell) such as Bash, sh, or zsh. It enables users to automate repetitive tasks and system administration processes. A shell script can include variables, conditional statements, loops, and functions, making it a powerful tool for OS interaction. It is widely used in Unix/Linux for administrative automation including software installation, log monitoring, file manipulation, and system backups.

Shell scripts support input/output redirection and piping, allowing complex workflows by chaining multiple commands. Scripts typically begin with a shebang line (e.g., `#!/bin/bash`) to indicate the interpreter. They are saved with `.sh` extension and made executable with `chmod +x script.sh`.

---

## AWK (Text Processing)

AWK is a domain-specific language designed for text processing, typically used as a data extraction and reporting tool. It operates on a per-line basis, dividing each line into fields based on a specified delimiter (default is whitespace) and then executing user-defined actions based on patterns and conditions.

AWK supports variables, control flow statements (loops and conditionals), functions, and built-in arithmetic and string operations. It maintains built-in variables like the current record (line), number of fields, current field values, and line number. `$1` refers to the first field, `$2` to the second, and so on. `$0` represents the entire line.

**Syntax:** `awk 'pattern { action }' filename`

```bash
$ echo -e "Alice 90\nBob 85\nCharlie 78" > scores.txt

$ awk '{print $1}' scores.txt        # print first field (names)
Alice
Bob
Charlie

$ awk '{print $1, $2+10}' scores.txt # print name and score+10
Alice 100
Bob 95
Charlie 88

$ awk '$2 >= 85 {print $1, $2}' scores.txt  # filter rows where score >= 85
Alice 90
Bob 85

$ awk -F":" '{print $1}' /etc/passwd  # use colon as delimiter, print usernames
root
student
...
```

The `-F":"` option sets the field separator to colon instead of the default whitespace. A condition before `{...}` like `$2 >= 85` filters which lines to process.

---

## Make

Make is a build automation tool commonly used in software development to manage project compilation and linking. It uses a configuration file called a **Makefile** that defines rules specifying how to build targets from their dependencies.

Make uses timestamp-based dependency checking to determine whether a file needs to be regenerated. When `make` is run, it compares the timestamps of targets and their prerequisites. If any prerequisite has been modified more recently than the target, or if the target does not exist, make executes the recipe (shell commands) to rebuild it. This ensures only modified parts of a project are recompiled, saving time and resources.

Makefiles support macros (variables), automatic variables (for referring to targets and dependencies), and pattern rules. Although traditionally used for compiling C/C++ code, Make can be used for any task involving dependency management and automation, such as document generation or data processing.

**Makefile structure:**

```makefile
# Variable definitions
CC = gcc
CFLAGS = -Wall

# Rule: target : prerequisites
# [TAB] recipe
my_program: main.o utils.o
	$(CC) -o my_program main.o utils.o

main.o: main.c
	$(CC) $(CFLAGS) -c main.c

clean:
	rm -f *.o my_program
```

Recipe lines must begin with a tab character, not spaces.

---

## CRON Jobs

CRON is a time-based job scheduling daemon in Unix-like operating systems. It enables users and system administrators to schedule commands or scripts to run automatically at specified times and intervals.

CRON uses a configuration file known as the **crontab** (cron table), which contains timing specifications and corresponding commands. The timing is defined using five fields: minute, hour, day of month, month, and day of week. Each user, including the system, can have their own crontab. CRON runs in the background and regularly checks these crontabs to execute scheduled tasks. It is commonly used for tasks like backups, system maintenance, sending emails, and periodic reporting.

**Crontab syntax:** `m h dom mon dow command`

Example: `0 2 * * * /usr/local/bin/backup_script.sh` runs a backup script every day at 2:00 AM.

The `crontab -e` command allows editing the personal or system-wide job schedule.
