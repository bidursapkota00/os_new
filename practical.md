# Operating System Practical Guide

---

# Practical 1: Basic Unix Commands

## Setup

**Option A (Native Linux):** Open the terminal (Ctrl+Alt+T on Ubuntu).

**Option B (WSL on Windows):**

```bash
wsl --install
# reboot
wsl --install -d Ubuntu
# password: 12345678
```

`--install` enables WSL and installs the default Linux distribution. `-d Ubuntu` specifies Ubuntu as the distribution to install.

Restart, set username/password. Launch "Ubuntu" from Start Menu.

**Option C (Online):** [webminal.org](https://www.webminal.org).

## 1.1 Navigation Commands

### `pwd` (Print Working Directory)

```bash
$ pwd
/home/student
```

### `cd` (Change Directory)

```bash
$ cd /tmp          # go to /tmp
$ cd ..            # go up one level
$ cd ~             # go to home directory
$ cd               # also goes to home
```

`/tmp` is the target directory path. `..` refers to the parent directory. `~` is a shortcut for the current user's home directory.

### `ls` (List Directory Contents)

```bash
$ cd /
$ ls
home  dev  tmp

$ ls -l
total 12
drwxr-xr-x 2 student student 4096 May 13 10:00 Desktop
drwxr-xr-x 2 student student 4096 May 13 10:00 Documents
drwxr-xr-x 2 student student 4096 May 13 10:00 Downloads

$ ls -a
.  ..  .bashrc  .profile  Desktop  Documents  Downloads

$ ls -la /tmp
total 8
drwxrwxrwt 2 root root 4096 May 13 10:00 .
drwxr-xr-x 23 root root 4096 May 13 10:00 ..
```

`-l` shows detailed (long) format including permissions, owner, size, and date. `-a` shows all files including hidden ones (names starting with `.`). `-la` combines both flags. `/tmp` after the command specifies which directory to list.

**Understanding `ls -l` output:** `-rwxr-xr-x` → type(`-`=file, `d`=dir) + owner(`rwx`) + group(`r-x`) + others(`r-x`).

## 1.2 File and Directory Management

### `mkdir` (Make Directory)

```bash
$ mkdir oslab
$ mkdir -p oslab/week1/notes    # create nested directories
$ ls -R oslab
oslab:
week1

oslab/week1:
notes
```

`-p` creates parent directories as needed. Without `-p`, the command fails if the parent directory does not exist. `-R` in `ls -R` lists contents recursively, showing all subdirectories and their contents.

### `touch` (Create Empty File)

```bash
$ touch oslab/hello.txt
$ ls oslab
hello.txt  week1
```

### `cp` (Copy)

```bash
$ cp oslab/hello.txt oslab/hello_backup.txt
$ cp -r oslab/week1 oslab/week2    # copy directory recursively
```

The first argument is the source file and the second is the destination. `-r` copies directories recursively, including all files and subdirectories inside them.

### `mv` (Move or Rename)

```bash
$ mv oslab/hello_backup.txt oslab/week1/    # move file
$ mv oslab/hello.txt oslab/greet.txt        # rename
```

The first argument is the source and the second is the destination. If the destination is a directory, the file is moved into it. If the destination is a new filename in the same directory, the file is renamed.

### `rm` (Remove)

```bash
$ rm oslab/greet.txt                # delete file
$ rm -r oslab/week2                 # delete directory recursively
```

Without flags, `rm` deletes only files. `-r` removes directories and all their contents recursively.

### `rmdir` (Remove Empty Directory)

```bash
$ rmdir oslab/week1/notes
```

## 1.3 File Viewing Commands

### `cat` (Display Entire File)

```bash
$ echo -e "Line 1\nLine 2\nLine 3" > sample.txt
$ cat sample.txt
Line 1
Line 2
Line 3
```

In the `echo` command, `-e` enables interpretation of escape characters like `\n` (newline). `>` redirects the output into a file, creating it if it does not exist.

### `head` and `tail`

```bash
$ head -2 sample.txt
Line 1
Line 2

$ tail -1 sample.txt
Line 3
```

`-2` in `head -2` displays the first 2 lines of the file. `-1` in `tail -1` displays the last 1 line. Without the number flag, both commands default to 10 lines.

### `wc` (Word Count)

```bash
$ wc sample.txt
 3  6 24 sample.txt
```

Output: lines, words, bytes.

### `sort`

```bash
$ echo -e "banana\napple\ncherry" > fruits.txt
$ sort fruits.txt
apple
banana
cherry
```

## 1.4 grep (Search Patterns)

```bash
$ echo -e "hello world\nHello OS\ngoodbye" > data.txt
$ grep "hello" data.txt
hello world

$ grep -i "hello" data.txt       # case-insensitive
hello world
Hello OS

$ grep -n "hello" data.txt       # show line numbers
1:hello world

$ grep -c "hello" data.txt       # count matches
1
```

The first argument is the search pattern and the second is the file to search in. `-i` makes the search case-insensitive. `-n` shows the line number before each matching line. `-c` prints only the count of matching lines instead of the lines themselves.

## 1.5 awk (Text Processing)

The `awk` command processes text line by line and splits each line into fields separated by whitespace. `$1` refers to the first field, `$2` to the second, and so on. `$0` represents the entire line.

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

The pattern inside single quotes is the awk program. `$1`, `$2` etc. refer to the first, second fields of each line. `$0` is the entire line. `-F":"` sets the field separator to colon instead of the default whitespace. A condition before `{...}` like `$2 >= 85` filters which lines to process.

## 1.6 Permissions with `chmod`

```bash
$ ls -l sample.txt
-rw-r--r-- 1 student student 24 May 13 10:05 sample.txt

$ chmod 755 sample.txt
$ ls -l sample.txt
-rwxr-xr-x 1 student student 24 May 13 10:05 sample.txt

$ chmod u-x,g+w sample.txt       # symbolic mode
$ ls -l sample.txt
-rw-rwr-x 1 student student 24 May 13 10:05 sample.txt
```

`755` is the octal permission mode where each digit represents owner, group, and others. In symbolic mode, `u` is the owner (user), `g` is the group, and `o` is others. `+` adds a permission and `-` removes it. `r` is read, `w` is write, and `x` is execute.

**Permission numbers:** r=4, w=2, x=1. So 755 = rwx(7) r-x(5) r-x(5).

### `chown` (Change Ownership)

The `chown` command changes the owner and/or group of a file or directory. Only the root user (or using `sudo`) can change file ownership.

```bash
$ ls -l sample.txt
-rwxr-xr-x 1 student student 24 May 13 10:05 sample.txt

$ sudo chown root sample.txt          # change owner to root
$ ls -l sample.txt
-rwxr-xr-x 1 root student 24 May 13 10:05 sample.txt

$ sudo chown student:staff sample.txt  # change owner and group
$ ls -l sample.txt
-rwxr-xr-x 1 student staff 24 May 13 10:05 sample.txt

$ sudo chown -R student:student oslab/ # change ownership recursively
```

`sudo` runs the command with root (superuser) privileges. The format is `chown owner:group filename`. `-R` applies the change recursively to all files and subdirectories inside the specified directory.

## 1.7 Process Management

### `ps` (Process Status)

The `ps` command displays information about running processes.

```bash
$ ps                          # show processes in current terminal
  PID TTY          TIME CMD
 1234 pts/0    00:00:00 bash
 5678 pts/0    00:00:00 ps

$ ps aux                      # show all processes with details
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1  16956  4392 ?        Ss   10:00   0:01 /sbin/init
student   1234  0.0  0.0   7236  3984 pts/0    Ss   10:01   0:00 bash
...

$ ps aux | grep bash          # filter for bash processes
student   1234  0.0  0.0   7236  3984 pts/0    Ss   10:01   0:00 bash
```

Without flags, `ps` shows only processes in the current terminal session. `a` shows processes from all users, `u` shows detailed user-oriented output (CPU, memory, etc.), and `x` includes processes not attached to a terminal. `| grep bash` pipes the output through grep to filter for lines containing "bash".

### `top` (Real-Time Process Monitor)

The `top` command provides a live, updating view of system processes sorted by CPU usage. Press `q` to quit.

```bash
$ top
top - 10:15:00 up 1:00, 1 user, load average: 0.15, 0.10, 0.05
Tasks: 120 total,   1 running, 119 sleeping,   0 stopped,   0 zombie
%Cpu(s):  2.3 us,  1.0 sy,  0.0 ni, 96.5 id,  0.2 wa,  0.0 hi,  0.0 si
MiB Mem:   7980.0 total,  5230.0 free,  1200.0 used,  1550.0 buff/cache

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
 1001 student   20   0  450000  30000  20000 S   2.0   0.4   0:05.12 firefox
    1 root      20   0   16956   4392   3200 S   0.0   0.1   0:01.00 init
...
```

### `kill` (Terminate a Process)

The `kill` command sends a signal to a process to terminate it. You need the PID (Process ID) which can be found using `ps` or `top`.

```bash
$ sleep 100 &                  # start a background process
[1] 9876

$ ps aux | grep sleep
student   9876  0.0  0.0   5476   580 pts/0    S    10:15   0:00 sleep 100

$ kill 9876                    # send default SIGTERM (graceful stop)
[1]+  Terminated              sleep 100

$ sleep 200 &
[1] 9900
$ kill -9 9900                 # send SIGKILL (force kill, cannot be ignored)
[1]+  Killed                  sleep 200
```

`&` at the end of a command runs it in the background, returning control to the terminal. The number after `kill` is the PID (Process ID) of the process to terminate. `-9` specifies the signal number, where 9 is SIGKILL (force kill). Without `-9`, `kill` sends SIGTERM (signal 15) which allows the process to clean up before exiting.

## 1.8 I/O Redirection and Pipes

```bash
$ echo "OS practical" > output.txt       # write (overwrite)
$ echo "is fun" >> output.txt            # append
$ cat output.txt
OS practical
is fun

$ cat output.txt | wc -l                 # pipe output to wc
2

$ sort < fruits.txt > sorted.txt         # input redirect + output redirect
$ cat sorted.txt
apple
banana
cherry
```

`>` redirects output to a file and overwrites it if it already exists. `>>` appends output to the end of the file without overwriting. `|` (pipe) sends the output of one command as input to the next command. `<` redirects input from a file, so `sort < fruits.txt` reads from fruits.txt instead of keyboard input. `-l` in `wc -l` counts only the number of lines.

## 1.9 Other Useful Commands

```bash
$ whoami
student

$ date
Tue May 13 10:10:00 NPT 2026

$ man ls                     # manual page for ls (press q to quit)

$ find . -name "*.txt"       # find all .txt files
./sample.txt
./data.txt
./fruits.txt
```

`man` followed by a command name opens its manual page. In `find`, `.` specifies the directory to search in (current directory). `-name "*.txt"` matches files whose name ends with `.txt`, where `*` is a wildcard for any characters.

---

# Practical 2: Shell Programming

## 2.1 Creating and Running a Script

```bash
$ nano hello.sh
```

Write:

```bash
#!/bin/bash
echo "Hello, OS Lab!"
```

Run:

```bash
$ chmod +x hello.sh
$ ./hello.sh
Hello, OS Lab!
```

- Use `code .` to open folder in vscode.
- OR: Use `explorer.exe .` to open file explorer then open folder in vscode using open with vscode.
- `#!/bin/bash` is the **shebang** line. It tells the system which interpreter to use.

## 2.2 Variables and User Input

```bash
#!/bin/bash
name="Student"
echo "Welcome, $name"

read -p "Enter your age: " age
echo "You are $age years old."
```

**Output:**

```
Welcome, Student
Enter your age: 20
You are 20 years old.
```

## 2.3 Arithmetic Operations

```bash
#!/bin/bash
read -p "Enter two numbers: " a b
echo "Sum: $((a + b))"
echo "Difference: $((a - b))"
echo "Product: $((a * b))"
echo "Quotient: $((a / b))"
echo "Remainder: $((a % b))"
```

**Output:**

```
Enter two numbers: 15 4
Sum: 19
Difference: 11
Product: 60
Quotient: 3
Remainder: 3
```

## 2.4 Conditional Statements

### if-elif-else

```bash
#!/bin/bash
read -p "Enter a number: " n
if [ $n -gt 0 ]; then
    echo "$n is positive"
elif [ $n -lt 0 ]; then
    echo "$n is negative"
else
    echo "It is zero"
fi
```

**Output:**

```
Enter a number: -5
-5 is negative
```

**Comparison operators:** `-eq` (equal), `-ne` (not equal), `-gt` (greater), `-lt` (less), `-ge` (>=), `-le` (<=).

### Check Even or Odd

```bash
#!/bin/bash
read -p "Enter a number: " n
if [ $((n % 2)) -eq 0 ]; then
    echo "$n is even"
else
    echo "$n is odd"
fi
```

**Output:**

```
Enter a number: 7
7 is odd
```

### Find Largest of Three Numbers

```bash
#!/bin/bash
read -p "Enter three numbers: " a b c
if [ $a -ge $b ] && [ $a -ge $c ]; then
    echo "Largest: $a"
elif [ $b -ge $a ] && [ $b -ge $c ]; then
    echo "Largest: $b"
else
    echo "Largest: $c"
fi
```

**Output:**

```
Enter three numbers: 10 25 18
Largest: 25
```

## 2.5 Loops

### For Loop: Print 1 to 5

```bash
#!/bin/bash
for i in 1 2 3 4 5; do
    echo "Number: $i"
done
```

**Output:**

```
Number: 1
Number: 2
Number: 3
Number: 4
Number: 5
```

### While Loop: Sum of First N Natural Numbers

```bash
#!/bin/bash
read -p "Enter N: " n
sum=0
i=1
while [ $i -le $n ]; do
    sum=$((sum + i))
    i=$((i + 1))
done
echo "Sum of first $n natural numbers: $sum"
```

**Output:**

```
Enter N: 10
Sum of first 10 natural numbers: 55
```

### Until Loop

```bash
#!/bin/bash
count=1
until [ $count -gt 5 ]; do
    echo "Count: $count"
    count=$((count + 1))
done
```

**Output:**

```
Count: 1
Count: 2
Count: 3
Count: 4
Count: 5
```

## 2.6 Factorial

```bash
#!/bin/bash
read -p "Enter a number: " num
fact=1
for (( i=1; i<=num; i++ )); do
    fact=$((fact * i))
done
echo "Factorial of $num is: $fact"
```

**Output:**

```
Enter a number: 5
Factorial of 5 is: 120
```

## 2.7 Fibonacci Sequence

```bash
#!/bin/bash
read -p "Enter number of terms: " n
a=0
b=1
echo "Fibonacci sequence:"
for (( i=0; i<n; i++ )); do
    echo -n "$a "
    fn=$((a + b))
    a=$b
    b=$fn
done
echo ""
```

**Output:**

```
Enter number of terms: 8
Fibonacci sequence:
0 1 1 2 3 5 8 13
```

## 2.8 Prime Number Check

```bash
#!/bin/bash
read -p "Enter a number: " num
if [ $num -le 1 ]; then
    echo "$num is not prime"
    exit 0
fi
is_prime=1
for (( i=2; i*i<=num; i++ )); do
    if [ $((num % i)) -eq 0 ]; then
        is_prime=0
        break
    fi
done
if [ $is_prime -eq 1 ]; then
    echo "$num is prime"
else
    echo "$num is not prime"
fi
```

**Output:**

```
Enter a number: 17
17 is prime
```

## 2.9 Palindrome Check

```bash
#!/bin/bash
read -p "Enter a string: " str
rev=$(echo "$str" | rev)
if [ "$str" = "$rev" ]; then
    echo "'$str' is a palindrome"
else
    echo "'$str' is not a palindrome"
fi
```

**Output:**

```
Enter a string: madam
'madam' is a palindrome
```

## 2.10 Multiplication Table

```bash
#!/bin/bash
read -p "Enter a number: " n
for (( i=1; i<=10; i++ )); do
    echo "$n x $i = $((n * i))"
done
```

**Output:**

```
Enter a number: 7
7 x 1 = 7
7 x 2 = 14
7 x 3 = 21
...
7 x 10 = 70
```

## 2.11 Functions

```bash
#!/bin/bash
add() {
    echo $(( $1 + $2 ))
}

result=$(add 10 20)
echo "Sum = $result"
```

**Output:**

```
Sum = 30
```

## 2.12 Case Statement (Menu-Driven Calculator)

```bash
#!/bin/bash
read -p "Enter two numbers: " a b
echo "1.Add 2.Subtract 3.Multiply 4.Divide"
read -p "Enter choice: " ch
case $ch in
    1) echo "Result: $((a + b))" ;;
    2) echo "Result: $((a - b))" ;;
    3) echo "Result: $((a * b))" ;;
    4) echo "Result: $((a / b))" ;;
    *) echo "Invalid choice" ;;
esac
```

**Output:**

```
Enter two numbers: 12 4
1.Add 2.Subtract 3.Multiply 4.Divide
Enter choice: 3
Result: 48
```

## 2.13 Arrays

```bash
#!/bin/bash
fruits=("Apple" "Banana" "Cherry" "Date")
echo "First fruit: ${fruits[0]}"
echo "All fruits: ${fruits[@]}"
echo "Count: ${#fruits[@]}"

for f in "${fruits[@]}"; do
    echo "- $f"
done
```

**Output:**

```
First fruit: Apple
All fruits: Apple Banana Cherry Date
Count: 4
- Apple
- Banana
- Cherry
- Date
```

## 2.14 File Operations in Script

```bash
#!/bin/bash
file="testfile.txt"
if [ -f "$file" ]; then
    echo "$file exists"
    echo "Lines: $(wc -l < $file)"
else
    echo "$file does not exist"
fi
```

**File test operators:** `-f` (is file), `-d` (is directory), `-e` (exists), `-r` (readable), `-w` (writable), `-x` (executable), `-s` (non-empty).

---

# Practical 3: Programs Using System Calls of UNIX

Unlike C library functions (`fopen`, `fgets`, `fprintf`), UNIX I/O system calls (`open`, `read`, `write`, `close`, `lseek`) interact directly with the kernel. They use integer file descriptors instead of `FILE*` pointers.

| System Call                 | Purpose                        | Header       |
| --------------------------- | ------------------------------ | ------------ |
| `open(path, flags, mode)`   | Open/create a file, returns fd | `<fcntl.h>`  |
| `read(fd, buf, n)`          | Read n bytes into buf          | `<unistd.h>` |
| `write(fd, buf, n)`         | Write n bytes from buf         | `<unistd.h>` |
| `close(fd)`                 | Close file descriptor          | `<unistd.h>` |
| `lseek(fd, offset, whence)` | Move file pointer              | `<unistd.h>` |

**Standard file descriptors:** 0 = stdin, 1 = stdout, 2 = stderr.

## 3.1 Write and Read a File Using System Calls

### Code: `io_basic.c`

```c
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>
#include <string.h>

int main() {
    int fd;
    char write_buf[] = "Hello from UNIX system calls!\n";
    char read_buf[100];

    /* Create and open file for read/write; truncate if exists */
    fd = open("output.txt", O_CREAT | O_RDWR | O_TRUNC, 0644);
    if (fd == -1) { perror("open"); return 1; }
    printf("File opened (fd = %d)\n", fd);

    /* Write to file */
    write(fd, write_buf, strlen(write_buf));
    printf("Written: %s", write_buf);

    /* Move pointer back to beginning */
    lseek(fd, 0, SEEK_SET);

    /* Read from file */
    int n = read(fd, read_buf, sizeof(read_buf) - 1);
    read_buf[n] = '\0';
    printf("Read back: %s", read_buf);

    close(fd);
    printf("File closed.\n");
    return 0;
}
```

### Compile and Run

```bash
$ gcc -o io_basic io_basic.c
$ ./io_basic
File opened (fd = 3)
Written: Hello from UNIX system calls!
Read back: Hello from UNIX system calls!
File closed.

$ cat output.txt
Hello from UNIX system calls!
```

**Open flags:** `O_RDONLY` (read), `O_WRONLY` (write), `O_RDWR` (both), `O_CREAT` (create), `O_TRUNC` (truncate), `O_APPEND` (append).

**lseek whence:** `SEEK_SET` (from start), `SEEK_CUR` (from current), `SEEK_END` (from end).

## 3.2 Create a Child Process Using `fork()`

### Code: `forkdemo.c`

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    pid_t pid = fork();

    if (pid < 0) {
        perror("fork");
        return 1;
    } else if (pid == 0) {
        /* Child process */
        printf("Child: PID = %d, Parent PID = %d\n", getpid(), getppid());
    } else {
        /* Parent process */
        wait(NULL);  /* Wait for child to finish */
        printf("Parent: PID = %d, Child PID = %d\n", getpid(), pid);
    }
    return 0;
}
```

### Compile and Run

```bash
$ gcc -o forkdemo forkdemo.c
$ ./forkdemo
Child: PID = 12346, Parent PID = 12345
Parent: PID = 12345, Child PID = 12346
```

**Key:** `fork()` returns 0 in child, child's PID in parent. `wait()` makes parent wait for child to finish.

---

# Practical 4: Scheduling Algorithms and Producer-Consumer Problem

## 4.1 FCFS (First Come First Serve) Scheduling

### Code: `fcfs.c`

```c
#include<stdio.h>

int main() {
    int n;
    printf("Enter number of process: ");
    scanf("%d", &n);

    int at[n], bt[n], ct[n], tat[n], wt[n], d[n];
    for(int i=0; i<n; i++) {
        printf("\nFor P%d: Enter at and bt: ", i+1);
        scanf("%d %d", &at[i], &bt[i]);
        d[i] = 0; ct[i]=0; tat[i]=0; wt[i]=0;
    }

    int t=0, stat=0, swt=0, c=0;
    while(c<n) {
        int min_at=9999, idx=-1;
        for(int i=0; i<n; i++) {
            if(!d[i] && at[i]<min_at && at[i]<=t) {
                min_at=at[i];
                idx=i;
            }
        }
        if(idx==-1) {t++; continue;}
        ct[idx]=t+bt[idx];
        tat[idx]=ct[idx]-at[idx];
        wt[idx]=tat[idx]-bt[idx];
        swt += wt[idx];
        stat += tat[idx];
        d[idx] = 1;
        c++;
        t = ct[idx];
    }

    printf("\n\nProcess\tat\tbt\tct\ttat\twt");
    for(int i=0; i<n; i++) {
        printf("\nP%d\t%d\t%d\t%d\t%d\t%d", i+1, at[i], bt[i], ct[i], tat[i], wt[i]);
    }
    printf("\nTotal\t\t\t\t%d\t%d\n", stat, swt);

    printf("\n\natat = %.2f", (float)stat/n);
    printf("\nawt = %.2f\n", (float)swt/n);

    return 0;
}
```

### Compile and Run

```bash
$ gcc -o fcfs fcfs.c
$ ./fcfs
Enter number of process: 4

For P1: Enter at and bt: 0 10

For P2: Enter at and bt: 1 6

For P3: Enter at and bt: 3 2

For P4: Enter at and bt: 5 4


Process at      bt      ct      tat     wt
P1      0       10      10      10      0
P2      1       6       16      15      9
P3      3       2       18      15      13
P4      5       4       22      17      13
Total                           57      35


atat = 14.25
awt = 8.75
```

## 4.2 SJF (Shortest Job First), Non-Preemptive

### Code: `sjf.c`

```c
#include<stdio.h>

int main() {
    int n;
    printf("Enter number of process: ");
    scanf("%d", &n);

    int at[n], bt[n], ct[n], tat[n], wt[n], d[n];
    for(int i=0; i<n; i++) {
        printf("\nFor P%d: Enter at and bt: ", i+1);
        scanf("%d %d", &at[i], &bt[i]);
        d[i] = 0; ct[i]=0; tat[i]=0; wt[i]=0;
    }

    int t=0, stat=0, swt=0, c=0;
    while(c<n) {
        int min_bt=9999, idx=-1;
        for(int i=0; i<n; i++) {
            if(!d[i] && bt[i]<min_bt && at[i]<=t) {
                min_bt=bt[i];
                idx=i;
            }
        }
        if(idx==-1) {t++; continue;}
        ct[idx]=t+bt[idx];
        tat[idx]=ct[idx]-at[idx];
        wt[idx]=tat[idx]-bt[idx];
        swt += wt[idx];
        stat += tat[idx];
        d[idx] = 1;
        c++;
        t = ct[idx];
    }

    printf("\n\nProcess\tat\tbt\tct\ttat\twt");
    for(int i=0; i<n; i++) {
        printf("\nP%d\t%d\t%d\t%d\t%d\t%d", i+1, at[i], bt[i], ct[i], tat[i], wt[i]);
    }
    printf("\nTotal\t\t\t\t%d\t%d\n", stat, swt);

    printf("\n\natat = %.2f", (float)stat/n);
    printf("\nawt = %.2f\n", (float)swt/n);

    return 0;
}
```

### Compile and Run

```bash
$ gcc -o sjf sjf.c
$ ./sjf
Enter number of process: 4

For P1: Enter at and bt: 0 7

For P2: Enter at and bt: 2 4

For P3: Enter at and bt: 4 1

For P4: Enter at and bt: 5 4


Process at      bt      ct      tat     wt
P1      0       7       7       7       0
P2      2       4       12      10      6
P3      4       1       8       4       3
P4      5       4       16      11      7
Total                           32      16


atat = 8.00
awt = 4.00
```

## 4.3 Round Robin Scheduling

### Code: `rr.c`

```c
#include<stdio.h>

int main() {
    int n, q;
    printf("Enter number of process: ");
    scanf("%d", &n);
    printf("\nEnter quantum: ");
    scanf("%d", &q);

    int at[n], bt[n], ct[n], tat[n], wt[n], rem[n], visited[n], pid[n];
    for(int i=0; i<n; i++) {
        printf("\nFor P%d: Enter at and bt: ", i+1);
        scanf("%d %d", &at[i], &bt[i]);
        rem[i] = bt[i]; pid[i]=i+1;
        ct[i]=0; tat[i]=0; wt[i]=0; visited[i]=0;
    }

    for(int i=0; i<n-1; i++) {
        for(int j=i+1; j<n; j++) {
            if(at[i] > at[j]) {
                int temp;
                temp = at[i]; at[i] = at[j]; at[j] = temp;
                temp = bt[i]; bt[i] = bt[j]; bt[j] = temp;
                temp = rem[i]; rem[i] = rem[j]; rem[j] = temp;
                temp = pid[i]; pid[i] = pid[j]; pid[j] = temp;
            }
        }
    }

    int queue[100];
    int front=0, rear=0;

    int t=0, stat=0, swt=0, c=0;
    while(c<n) {
        for(int i=0; i<n; i++) {
            if(at[i]<=t && !visited[i]) {
                queue[rear++] = i;
                visited[i] = 1;
            }
        }

        if(front == rear) {t++; continue;}

        int p = queue[front++];
        if(rem[p]>q) {
            rem[p]-=q;
            t+=q;
        } else {
            ct[p]=t+rem[p];
            rem[p] = 0;
            tat[p]=ct[p]-at[p];
            wt[p]=tat[p]-bt[p];
            swt += wt[p];
            stat += tat[p];
            c++;
            t = ct[p];
        }

        for(int i=0; i<n; i++) {
            if(at[i]<=t && !visited[i]) {
                queue[rear++] = i;
                visited[i] = 1;
            }
        }

        if(rem[p] > 0) queue[rear++] = p;
    }

    printf("\n\nProcess\tat\tbt\tct\ttat\twt");
    for(int i=0; i<n; i++) {
        printf("\nP%d\t%d\t%d\t%d\t%d\t%d", pid[i], at[i], bt[i], ct[i], tat[i], wt[i]);
    }
    printf("\nTotal\t\t\t\t%d\t%d\n", stat, swt);

    printf("\n\natat = %.2f", (float)stat/n);
    printf("\nawt = %.2f\n", (float)swt/n);

    return 0;
}
```

### Compile and Run

```bash
$ gcc -o rr rr.c
$ ./rr
Enter number of process: 4

Enter quantum: 2

For P1: Enter at and bt: 0 5

For P2: Enter at and bt: 1 3

For P3: Enter at and bt: 2 1

For P4: Enter at and bt: 3 2


Process at      bt      ct      tat     wt
P1      0       5       11      11      6
P2      1       3       10      9       6
P3      2       1       5       3       2
P4      3       2       9       6       4
Total                           29      18


atat = 7.25
awt = 4.50
```

## 5.4 Producer-Consumer Problem Using Semaphores

### Code: `prodcon.c`

```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <semaphore.h>
#include <unistd.h>

#define BUFFER_SIZE 5
#define ITEMS 10

int buffer[BUFFER_SIZE];
int in = 0, out = 0;

sem_t empty, full;
pthread_mutex_t mutex;

void *producer(void *arg) {
    for (int i = 1; i <= ITEMS; i++) {
        sem_wait(&empty);
        pthread_mutex_lock(&mutex);

        buffer[in] = i;
        printf("Produced: %d at index %d\n", i, in);
        in = (in + 1) % BUFFER_SIZE;

        pthread_mutex_unlock(&mutex);
        sem_post(&full);
        usleep(100000);  /* 0.1s delay */
    }
    return NULL;
}

void *consumer(void *arg) {
    for (int i = 1; i <= ITEMS; i++) {
        sem_wait(&full);
        pthread_mutex_lock(&mutex);

        int item = buffer[out];
        printf("Consumed: %d from index %d\n", item, out);
        out = (out + 1) % BUFFER_SIZE;

        pthread_mutex_unlock(&mutex);
        sem_post(&empty);
        usleep(150000);  /* 0.15s delay */
    }
    return NULL;
}

int main() {
    sem_init(&empty, 0, BUFFER_SIZE);
    sem_init(&full, 0, 0);
    pthread_mutex_init(&mutex, NULL);

    pthread_t prod, cons;
    pthread_create(&prod, NULL, producer, NULL);
    pthread_create(&cons, NULL, consumer, NULL);

    pthread_join(prod, NULL);
    pthread_join(cons, NULL);

    sem_destroy(&empty);
    sem_destroy(&full);
    pthread_mutex_destroy(&mutex);

    printf("Done.\n");
    return 0;
}
```

### Compile and Run

```bash
$ gcc -o prodcon prodcon.c -lpthread
$ ./prodcon
Produced: 1 at index 0
Produced: 2 at index 1
Consumed: 1 from index 0
Produced: 3 at index 2
Consumed: 2 from index 1
Produced: 4 at index 3
Consumed: 3 from index 2
...
Consumed: 10 from index 4
Done.
```

**Synchronization explained:**

- `sem_t empty` is initialized to BUFFER_SIZE and counts free slots. The producer waits if the buffer is full.
- `sem_t full` is initialized to 0 and counts filled slots. The consumer waits if the buffer is empty.
- `pthread_mutex_t mutex` ensures only one thread accesses the buffer at a time.
- `sem_wait()` decrements the semaphore and blocks if the value is 0. `sem_post()` increments the semaphore and wakes a blocked thread.

---

# Practical 6: Memory Management (Paging and Segmentation)

## 6.1 Paging: Logical to Physical Address Translation

In paging, memory is divided into fixed-size **pages** (logical) and **frames** (physical). A **page table** maps each page number to a frame number.

**Formula:**

- Page Number = Logical Address / Page Size
- Offset = Logical Address % Page Size
- Physical Address = (Frame Number × Page Size) + Offset

### Code: `paging.c`

```c
#include <stdio.h>

int main() {
    int pages, page_size, i;

    printf("Enter number of pages: ");
    scanf("%d", &pages);
    printf("Enter page size (bytes): ");
    scanf("%d", &page_size);

    int page_table[pages];
    printf("Enter frame number for each page:\n");
    for (i = 0; i < pages; i++) {
        printf("  Page %d -> Frame: ", i);
        scanf("%d", &page_table[i]);
    }

    int logical;
    printf("\nEnter logical address: ");
    scanf("%d", &logical);

    int page_num = logical / page_size;
    int offset = logical % page_size;

    if (page_num >= pages) {
        printf("Error: Page %d does not exist (page fault)!\n", page_num);
        return 1;
    }

    int frame = page_table[page_num];
    int physical = frame * page_size + offset;

    printf("\n--- Address Translation ---\n");
    printf("Page Number : %d\n", page_num);
    printf("Offset      : %d\n", offset);
    printf("Frame Number: %d\n", frame);
    printf("Physical Address: %d\n", physical);

    return 0;
}
```

### Compile and Run

```bash
$ gcc -o paging paging.c
$ ./paging
Enter number of pages: 4
Enter page size (bytes): 1024
Enter frame number for each page:
  Page 0 -> Frame: 2
  Page 1 -> Frame: 4
  Page 2 -> Frame: 1
  Page 3 -> Frame: 7

Enter logical address: 1025

--- Address Translation ---
Page Number : 1
Offset      : 1
Frame Number: 4
Physical Address: 4097
```

**Explanation:** Logical 1025 → Page 1 (1025/1024), Offset 1 (1025%1024) → Frame 4 → Physical = 4×1024+1 = 4097.

## 6.2 FIFO Page Replacement Algorithm

### Code: `fifo_page.c`

```c
#include <stdio.h>

int main() {
    int frames, n, i, j;
    printf("Enter number of frames: ");
    scanf("%d", &frames);
    printf("Enter length of reference string: ");
    scanf("%d", &n);

    int ref[n], frame[frames];
    printf("Enter reference string: ");
    for (i = 0; i < n; i++) scanf("%d", &ref[i]);

    for (i = 0; i < frames; i++) frame[i] = -1;

    int faults = 0, ptr = 0;  /* ptr = next frame to replace (FIFO) */

    printf("\nRef\tFrames\t\t\tResult\n");
    for (i = 0; i < n; i++) {
        int found = 0;
        for (j = 0; j < frames; j++)
            if (frame[j] == ref[i]) { found = 1; break; }

        if (!found) {
            frame[ptr] = ref[i];
            ptr = (ptr + 1) % frames;
            faults++;
            printf("%d\t", ref[i]);
            for (j = 0; j < frames; j++) printf("%d ", frame[j]);
            printf("\t\tFault\n");
        } else {
            printf("%d\t", ref[i]);
            for (j = 0; j < frames; j++) printf("%d ", frame[j]);
            printf("\t\tHit\n");
        }
    }
    printf("\nTotal Page Faults: %d\n", faults);
    printf("Hit Ratio: %.2f\n", (float)(n - faults) / n);
    return 0;
}
```

### Compile and Run

```bash
$ gcc -o fifo_page fifo_page.c
$ ./fifo_page
Enter number of frames: 3
Enter length of reference string: 10
Enter reference string: 7 0 1 2 0 3 0 4 2 3

Ref	Frames			Result
7	7 -1 -1 		Fault
0	7 0 -1 			Fault
1	7 0 1 			Fault
2	2 0 1 			Fault
0	2 0 1 			Hit
3	2 3 1 			Fault
0	2 3 0 			Fault
4	4 3 0 			Fault
2	4 2 0 			Fault
3	4 2 3 			Fault

Total Page Faults: 9
Hit Ratio: 0.10
```

## 6.3 Segmentation: Logical to Physical Address Translation

In segmentation, memory is divided into variable-size **segments**. Each segment has a **base** (starting physical address) and a **limit** (maximum size). If offset ≥ limit, a segmentation fault occurs.

**Formula:** Physical Address = Base + Offset (only if Offset < Limit)

### Code: `segmentation.c`

```c
#include <stdio.h>

typedef struct {
    int base;
    int limit;
} Segment;

int main() {
    int n, i;
    printf("Enter number of segments: ");
    scanf("%d", &n);

    Segment seg[n];
    for (i = 0; i < n; i++) {
        printf("Segment %d - Base & Limit: ", i);
        scanf("%d %d", &seg[i].base, &seg[i].limit);
    }

    int seg_num, offset;
    printf("\nEnter segment number: ");
    scanf("%d", &seg_num);
    printf("Enter offset: ");
    scanf("%d", &offset);

    if (seg_num < 0 || seg_num >= n) {
        printf("Error: Invalid segment number!\n");
        return 1;
    }

    if (offset >= seg[seg_num].limit) {
        printf("Error: Segmentation Fault! Offset %d >= Limit %d\n",
               offset, seg[seg_num].limit);
        return 1;
    }

    int physical = seg[seg_num].base + offset;
    printf("\n--- Address Translation ---\n");
    printf("Segment   : %d (Base=%d, Limit=%d)\n",
           seg_num, seg[seg_num].base, seg[seg_num].limit);
    printf("Offset    : %d\n", offset);
    printf("Physical Address: %d\n", physical);

    return 0;
}
```

### Compile and Run

**Valid access:**

```bash
$ gcc -o segmentation segmentation.c
$ ./segmentation
Enter number of segments: 3
Segment 0 - Base & Limit: 1000 400
Segment 1 - Base & Limit: 2000 600
Segment 2 - Base & Limit: 3000 200

Enter segment number: 1
Enter offset: 150

--- Address Translation ---
Segment   : 1 (Base=2000, Limit=600)
Offset    : 150
Physical Address: 2150
```

**Out-of-bounds access:**

```bash
$ ./segmentation
Enter number of segments: 3
Segment 0 - Base & Limit: 1000 400
Segment 1 - Base & Limit: 2000 600
Segment 2 - Base & Limit: 3000 200

Enter segment number: 2
Enter offset: 250

Error: Segmentation Fault! Offset 250 >= Limit 200
```

## 6.4 Paging vs Segmentation

| Aspect        | Paging                              | Segmentation                      |
| ------------- | ----------------------------------- | --------------------------------- |
| Division      | Fixed-size pages                    | Variable-size segments            |
| Address       | Page number + offset                | Segment number + offset           |
| Fragmentation | Internal (unused space within page) | External (gaps between segments)  |
| Table         | Page table (page → frame)           | Segment table (base + limit)      |
| User view     | Transparent to programmer           | Matches logical program structure |
