# Operating System — Practical Guide

---

# Practical 1: Basic Unix Commands

## Setup

**Option A — Native Linux:** Open the terminal (Ctrl+Alt+T on Ubuntu).

**Option B — WSL on Windows:**

```bash
wsl --install
```

Restart, set username/password. Launch "Ubuntu" from Start Menu.

**Option C — Online:** [webminal.org](https://www.webminal.org).

## 1.1 Navigation Commands

### `pwd` — Print Working Directory

```bash
$ pwd
/home/student
```

### `cd` — Change Directory

```bash
$ cd /tmp          # go to /tmp
$ cd ..            # go up one level
$ cd ~             # go to home directory
$ cd               # also goes to home
```

### `ls` — List Directory Contents

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

**Understanding `ls -l` output:** `-rwxr-xr-x` → type(`-`=file, `d`=dir) + owner(`rwx`) + group(`r-x`) + others(`r-x`).

## 1.2 File and Directory Management

### `mkdir` — Make Directory

```bash
$ mkdir oslab
$ mkdir -p oslab/week1/notes    # create nested directories
$ ls -R oslab
oslab:
week1

oslab/week1:
notes
```

### `touch` — Create Empty File

```bash
$ touch oslab/hello.txt
$ ls oslab
hello.txt  week1
```

### `cp` — Copy

```bash
$ cp oslab/hello.txt oslab/hello_backup.txt
$ cp -r oslab/week1 oslab/week2    # copy directory recursively
```

### `mv` — Move / Rename

```bash
$ mv oslab/hello_backup.txt oslab/week1/    # move file
$ mv oslab/hello.txt oslab/greet.txt        # rename
```

### `rm` — Remove

```bash
$ rm oslab/greet.txt                # delete file
$ rm -r oslab/week2                 # delete directory recursively
```

### `rmdir` — Remove Empty Directory

```bash
$ rmdir oslab/week1/notes
```

## 1.3 File Viewing Commands

### `cat` — Display Entire File

```bash
$ echo -e "Line 1\nLine 2\nLine 3" > sample.txt
$ cat sample.txt
Line 1
Line 2
Line 3
```

### `head` and `tail`

```bash
$ head -2 sample.txt
Line 1
Line 2

$ tail -1 sample.txt
Line 3
```

### `wc` — Word Count

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

## 1.4 grep — Search Patterns

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

## 1.5 Permissions — `chmod`

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

**Permission numbers:** r=4, w=2, x=1. So 755 = rwx(7) r-x(5) r-x(5).

## 1.6 I/O Redirection and Pipes

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

## 1.7 Other Useful Commands

```bash
$ whoami
student

$ date
Tue May 13 10:10:00 NPT 2026

$ cal
      May 2026
Su Mo Tu We Th Fr Sa
                1  2
 3  4  5  6  7  8  9
...

$ man ls                     # manual page for ls (press q to quit)

$ find . -name "*.txt"       # find all .txt files
./sample.txt
./data.txt
./fruits.txt
```

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

`#!/bin/bash` is the **shebang** — it tells the system which interpreter to use.

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

### For Loop — Print 1 to 5

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

### While Loop — Sum of First N Natural Numbers

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

# Practical 3: Implementation of ls and grep Commands

These programs are written in C and compiled/run on a Linux system.

## Setup

```bash
$ sudo apt install gcc      # install GCC compiler (if not installed)
$ gcc --version
gcc (Ubuntu 13.2.0) 13.2.0
```

## 3.1 Simple `ls` — List Directory Contents

### Code: `myls.c`

```c
#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>

int main(int argc, char *argv[]) {
    char *path = (argc > 1) ? argv[1] : ".";
    DIR *dir = opendir(path);

    if (dir == NULL) {
        perror("Cannot open directory");
        return 1;
    }

    struct dirent *entry;
    while ((entry = readdir(dir)) != NULL) {
        /* Skip hidden files (starting with '.') */
        if (entry->d_name[0] != '.')
            printf("%s\n", entry->d_name);
    }

    closedir(dir);
    return 0;
}
```

### Compile and Run

```bash
$ gcc -o myls myls.c
$ ./myls
myls.c
myls
fruits.txt
sample.txt

$ ./myls /tmp
systemd-private
```

**Key functions:**

- `opendir(path)` — opens a directory stream.
- `readdir(dir)` — reads next entry, returns `struct dirent*` with `d_name` field.
- `closedir(dir)` — closes the directory stream.

## 3.2 `ls -l` — Long Listing with File Details

### Code: `myls_l.c`

```c
#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>
#include <sys/stat.h>
#include <pwd.h>
#include <grp.h>
#include <time.h>
#include <string.h>

void print_permissions(mode_t mode) {
    printf("%c", S_ISDIR(mode) ? 'd' : '-');
    printf("%c", (mode & S_IRUSR) ? 'r' : '-');
    printf("%c", (mode & S_IWUSR) ? 'w' : '-');
    printf("%c", (mode & S_IXUSR) ? 'x' : '-');
    printf("%c", (mode & S_IRGRP) ? 'r' : '-');
    printf("%c", (mode & S_IWGRP) ? 'w' : '-');
    printf("%c", (mode & S_IXGRP) ? 'x' : '-');
    printf("%c", (mode & S_IROTH) ? 'r' : '-');
    printf("%c", (mode & S_IWOTH) ? 'w' : '-');
    printf("%c", (mode & S_IXOTH) ? 'x' : '-');
}

int main(int argc, char *argv[]) {
    char *path = (argc > 1) ? argv[1] : ".";
    DIR *dir = opendir(path);
    if (dir == NULL) {
        perror("Cannot open directory");
        return 1;
    }

    struct dirent *entry;
    struct stat st;
    char fullpath[1024];

    while ((entry = readdir(dir)) != NULL) {
        if (entry->d_name[0] == '.') continue;

        snprintf(fullpath, sizeof(fullpath), "%s/%s", path, entry->d_name);
        if (stat(fullpath, &st) == -1) continue;

        print_permissions(st.st_mode);
        printf(" %2ld", (long)st.st_nlink);
        printf(" %-8s", getpwuid(st.st_uid)->pw_name);
        printf(" %-8s", getgrgid(st.st_gid)->gr_name);
        printf(" %8ld", (long)st.st_size);

        char timebuf[64];
        strftime(timebuf, sizeof(timebuf), "%b %d %H:%M", localtime(&st.st_mtime));
        printf(" %s", timebuf);

        printf(" %s\n", entry->d_name);
    }

    closedir(dir);
    return 0;
}
```

### Compile and Run

```bash
$ gcc -o myls_l myls_l.c
$ ./myls_l
-rw-r--r--  1 student  student       24 May 13 10:05 sample.txt
-rwxr-xr-x  1 student  student    16832 May 13 10:20 myls
-rw-r--r--  1 student  student      890 May 13 10:18 myls.c
```

**Additional functions used:**

- `stat(path, &st)` — fills `struct stat` with file metadata (size, permissions, owner, timestamps).
- `getpwuid(uid)` — converts user ID to username.
- `getgrgid(gid)` — converts group ID to group name.
- `strftime()` — formats time for display.
- `S_IRUSR`, `S_IWUSR`, etc. — permission bit masks.

## 3.3 Simple `grep` — Search Pattern in File

### Code: `mygrep.c`

```c
#include <stdio.h>
#include <string.h>

#define MAX_LINE 1024

int main(int argc, char *argv[]) {
    if (argc != 3) {
        printf("Usage: %s <pattern> <filename>\n", argv[0]);
        return 1;
    }

    char *pattern = argv[1];
    char *filename = argv[2];

    FILE *fp = fopen(filename, "r");
    if (fp == NULL) {
        perror("Cannot open file");
        return 1;
    }

    char line[MAX_LINE];
    int line_num = 0;

    while (fgets(line, sizeof(line), fp) != NULL) {
        line_num++;
        if (strstr(line, pattern) != NULL) {
            printf("%d: %s", line_num, line);
        }
    }

    fclose(fp);
    return 0;
}
```

### Compile and Run

Create a test file first:

```bash
$ cat > testfile.txt
The operating system manages hardware.
A process is a running program.
The OS provides abstraction.
Memory management is a key function of OS.
```

(Press Ctrl+D to save)

```bash
$ gcc -o mygrep mygrep.c
$ ./mygrep "OS" testfile.txt
3: The OS provides abstraction.
4: Memory management is a key function of OS.

$ ./mygrep "process" testfile.txt
2: A process is a running program.
```

**Key functions:**

- `fopen(filename, "r")` — opens file for reading.
- `fgets(line, size, fp)` — reads one line at a time into buffer.
- `strstr(line, pattern)` — returns pointer to first occurrence of pattern in line, or NULL if not found.
- `fclose(fp)` — closes the file.

## 3.4 `grep` with Options (`-i`, `-c`, `-v`)

### Code: `mygrep2.c`

```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

#define MAX_LINE 1024

/* Convert string to lowercase for case-insensitive search */
void to_lower(char *dst, const char *src) {
    while (*src) {
        *dst++ = tolower((unsigned char)*src++);
    }
    *dst = '\0';
}

int main(int argc, char *argv[]) {
    if (argc < 3) {
        printf("Usage: %s [-i] [-c] [-v] <pattern> <filename>\n", argv[0]);
        return 1;
    }

    int ignore_case = 0, count_only = 0, invert = 0;
    int i;

    /* Parse option flags */
    for (i = 1; i < argc - 2; i++) {
        if (strcmp(argv[i], "-i") == 0) ignore_case = 1;
        else if (strcmp(argv[i], "-c") == 0) count_only = 1;
        else if (strcmp(argv[i], "-v") == 0) invert = 1;
    }

    char *pattern = argv[argc - 2];
    char *filename = argv[argc - 1];

    FILE *fp = fopen(filename, "r");
    if (fp == NULL) {
        perror("Cannot open file");
        return 1;
    }

    char line[MAX_LINE], line_low[MAX_LINE], pat_low[MAX_LINE];
    int match_count = 0;

    if (ignore_case) to_lower(pat_low, pattern);

    while (fgets(line, sizeof(line), fp) != NULL) {
        int found;
        if (ignore_case) {
            to_lower(line_low, line);
            found = (strstr(line_low, pat_low) != NULL);
        } else {
            found = (strstr(line, pattern) != NULL);
        }

        if (invert) found = !found;

        if (found) {
            match_count++;
            if (!count_only) printf("%s", line);
        }
    }

    if (count_only) printf("%d\n", match_count);

    fclose(fp);
    return 0;
}
```

### Compile and Run

```bash
$ gcc -o mygrep2 mygrep2.c

$ ./mygrep2 -i "os" testfile.txt
The operating system manages hardware.
The OS provides abstraction.
Memory management is a key function of OS.

$ ./mygrep2 -c "OS" testfile.txt
2

$ ./mygrep2 -v "OS" testfile.txt
The operating system manages hardware.
A process is a running program.
```

**Options implemented:**

- `-i` — case-insensitive matching using `tolower()`.
- `-c` — prints only count of matching lines.
- `-v` — inverts match (prints lines that do NOT contain the pattern).

---

# Practical 4: Programs Using I/O System Calls of UNIX

Unlike C library functions (`fopen`, `fgets`, `fprintf`), UNIX I/O system calls (`open`, `read`, `write`, `close`, `lseek`) interact directly with the kernel. They use integer **file descriptors** instead of `FILE*` pointers.

| System Call                 | Purpose                        | Header       |
| --------------------------- | ------------------------------ | ------------ |
| `open(path, flags, mode)`   | Open/create a file, returns fd | `<fcntl.h>`  |
| `read(fd, buf, n)`          | Read n bytes into buf          | `<unistd.h>` |
| `write(fd, buf, n)`         | Write n bytes from buf         | `<unistd.h>` |
| `close(fd)`                 | Close file descriptor          | `<unistd.h>` |
| `lseek(fd, offset, whence)` | Move file pointer              | `<unistd.h>` |

**Standard file descriptors:** 0 = stdin, 1 = stdout, 2 = stderr.

## 4.1 Write and Read a File Using System Calls

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

## 4.2 Copy File Using System Calls

### Code: `filecopy.c`

```c
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>

int main(int argc, char *argv[]) {
    if (argc != 3) {
        write(2, "Usage: ./filecopy <src> <dst>\n", 29);
        return 1;
    }

    int src = open(argv[1], O_RDONLY);
    if (src == -1) { perror("open src"); return 1; }

    int dst = open(argv[2], O_CREAT | O_WRONLY | O_TRUNC, 0644);
    if (dst == -1) { perror("open dst"); close(src); return 1; }

    char buf[1024];
    int n;
    while ((n = read(src, buf, sizeof(buf))) > 0) {
        write(dst, buf, n);
    }

    close(src);
    close(dst);
    printf("File copied: %s -> %s\n", argv[1], argv[2]);
    return 0;
}
```

### Compile and Run

```bash
$ echo "Operating System Lab" > source.txt
$ gcc -o filecopy filecopy.c
$ ./filecopy source.txt dest.txt
File copied: source.txt -> dest.txt
$ cat dest.txt
Operating System Lab
```

## 4.3 Get File Information Using `stat()` System Call

### Code: `filestat.c`

```c
#include <stdio.h>
#include <sys/stat.h>
#include <time.h>

int main(int argc, char *argv[]) {
    if (argc != 2) { printf("Usage: %s <file>\n", argv[0]); return 1; }

    struct stat st;
    if (stat(argv[1], &st) == -1) { perror("stat"); return 1; }

    printf("File: %s\n", argv[1]);
    printf("Size: %ld bytes\n", (long)st.st_size);
    printf("Inode: %ld\n", (long)st.st_ino);
    printf("Links: %ld\n", (long)st.st_nlink);
    printf("Permissions: %o\n", st.st_mode & 0777);
    printf("Last modified: %s", ctime(&st.st_mtime));

    if (S_ISREG(st.st_mode)) printf("Type: Regular file\n");
    else if (S_ISDIR(st.st_mode)) printf("Type: Directory\n");

    return 0;
}
```

### Compile and Run

```bash
$ gcc -o filestat filestat.c
$ ./filestat source.txt
File: source.txt
Size: 21 bytes
Inode: 524301
Links: 1
Permissions: 644
Last modified: Tue May 13 10:30:00 2026
Type: Regular file
```

## 4.4 Create a Child Process Using `fork()`

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

## 4.5 Execute a Program Using `exec()`

### Code: `execdemo.c`

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    pid_t pid = fork();

    if (pid == 0) {
        printf("Child: running 'ls -l' via exec\n");
        execlp("ls", "ls", "-l", NULL);
        perror("exec failed");  /* only reached if exec fails */
    } else {
        wait(NULL);
        printf("Parent: child finished.\n");
    }
    return 0;
}
```

### Compile and Run

```bash
$ gcc -o execdemo execdemo.c
$ ./execdemo
Child: running 'ls -l' via exec
total 48
-rwxr-xr-x 1 student student 16832 May 13 10:35 execdemo
-rw-r--r-- 1 student student   310 May 13 10:35 execdemo.c
...
Parent: child finished.
```

**Key:** `execlp()` replaces the child process image with a new program. The child never returns from exec unless it fails.

---

# Practical 5: Scheduling Algorithms and Producer-Consumer Problem

## 5.1 FCFS (First Come First Serve) Scheduling

### Code: `fcfs.c`

```c
#include <stdio.h>

int main() {
    int n, i;
    printf("Enter number of processes: ");
    scanf("%d", &n);

    int bt[n], wt[n], tat[n], at[n];
    for (i = 0; i < n; i++) {
        printf("P%d - Arrival Time & Burst Time: ", i + 1);
        scanf("%d %d", &at[i], &bt[i]);
    }

    /* Sort by arrival time (simple selection sort) */
    for (i = 0; i < n - 1; i++)
        for (int j = i + 1; j < n; j++)
            if (at[j] < at[i]) {
                int t;
                t = at[i]; at[i] = at[j]; at[j] = t;
                t = bt[i]; bt[i] = bt[j]; bt[j] = t;
            }

    int ct = 0;  /* current time */
    float total_wt = 0, total_tat = 0;

    printf("\nProcess\tAT\tBT\tWT\tTAT\n");
    for (i = 0; i < n; i++) {
        if (ct < at[i]) ct = at[i];  /* CPU idle */
        wt[i] = ct - at[i];
        tat[i] = wt[i] + bt[i];
        ct += bt[i];
        total_wt += wt[i];
        total_tat += tat[i];
        printf("P%d\t%d\t%d\t%d\t%d\n", i + 1, at[i], bt[i], wt[i], tat[i]);
    }
    printf("Avg WT = %.2f, Avg TAT = %.2f\n", total_wt / n, total_tat / n);
    return 0;
}
```

### Compile and Run

```bash
$ gcc -o fcfs fcfs.c
$ ./fcfs
Enter number of processes: 3
P1 - Arrival Time & Burst Time: 0 5
P2 - Arrival Time & Burst Time: 1 3
P3 - Arrival Time & Burst Time: 2 8

Process	AT	BT	WT	TAT
P1	0	5	0	5
P2	1	3	4	7
P3	2	8	6	14
Avg WT = 3.33, Avg TAT = 8.67
```

## 5.2 SJF (Shortest Job First) — Non-Preemptive

### Code: `sjf.c`

```c
#include <stdio.h>

int main() {
    int n, i;
    printf("Enter number of processes: ");
    scanf("%d", &n);

    int bt[n], at[n], wt[n], tat[n], done[n], order[n];
    for (i = 0; i < n; i++) {
        printf("P%d - Arrival Time & Burst Time: ", i + 1);
        scanf("%d %d", &at[i], &bt[i]);
        done[i] = 0;
    }

    int ct = 0, completed = 0;
    float total_wt = 0, total_tat = 0;

    printf("\nProcess\tAT\tBT\tWT\tTAT\n");
    while (completed < n) {
        int min_bt = 99999, idx = -1;
        for (i = 0; i < n; i++)
            if (!done[i] && at[i] <= ct && bt[i] < min_bt) {
                min_bt = bt[i]; idx = i;
            }
        if (idx == -1) { ct++; continue; }

        wt[idx] = ct - at[idx];
        tat[idx] = wt[idx] + bt[idx];
        ct += bt[idx];
        done[idx] = 1;
        completed++;
        total_wt += wt[idx];
        total_tat += tat[idx];
        printf("P%d\t%d\t%d\t%d\t%d\n", idx + 1, at[idx], bt[idx], wt[idx], tat[idx]);
    }
    printf("Avg WT = %.2f, Avg TAT = %.2f\n", total_wt / n, total_tat / n);
    return 0;
}
```

### Compile and Run

```bash
$ gcc -o sjf sjf.c
$ ./sjf
Enter number of processes: 3
P1 - Arrival Time & Burst Time: 0 5
P2 - Arrival Time & Burst Time: 1 3
P3 - Arrival Time & Burst Time: 2 8

Process	AT	BT	WT	TAT
P1	0	5	0	5
P2	1	3	4	7
P3	2	8	6	14
Avg WT = 3.33, Avg TAT = 8.67
```

## 5.3 Round Robin Scheduling

### Code: `rr.c`

```c
#include <stdio.h>

int main() {
    int n, quantum, i;
    printf("Enter number of processes: ");
    scanf("%d", &n);

    int bt[n], at[n], rem[n], wt[n], tat[n];
    for (i = 0; i < n; i++) {
        printf("P%d - Arrival Time & Burst Time: ", i + 1);
        scanf("%d %d", &at[i], &bt[i]);
        rem[i] = bt[i];
    }
    printf("Enter time quantum: ");
    scanf("%d", &quantum);

    int ct = 0, completed = 0;
    while (completed < n) {
        int found = 0;
        for (i = 0; i < n; i++) {
            if (rem[i] > 0 && at[i] <= ct) {
                found = 1;
                if (rem[i] > quantum) {
                    ct += quantum;
                    rem[i] -= quantum;
                } else {
                    ct += rem[i];
                    rem[i] = 0;
                    tat[i] = ct - at[i];
                    wt[i] = tat[i] - bt[i];
                    completed++;
                }
            }
        }
        if (!found) ct++;
    }

    float total_wt = 0, total_tat = 0;
    printf("\nProcess\tAT\tBT\tWT\tTAT\n");
    for (i = 0; i < n; i++) {
        total_wt += wt[i]; total_tat += tat[i];
        printf("P%d\t%d\t%d\t%d\t%d\n", i + 1, at[i], bt[i], wt[i], tat[i]);
    }
    printf("Avg WT = %.2f, Avg TAT = %.2f\n", total_wt / n, total_tat / n);
    return 0;
}
```

### Compile and Run

```bash
$ gcc -o rr rr.c
$ ./rr
Enter number of processes: 3
P1 - Arrival Time & Burst Time: 0 5
P2 - Arrival Time & Burst Time: 1 3
P3 - Arrival Time & Burst Time: 2 8
Enter time quantum: 4

Process	AT	BT	WT	TAT
P1	0	5	7	12
P2	1	3	6	9
P3	2	8	6	14
Avg WT = 6.33, Avg TAT = 11.67
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

- `sem_t empty` (init = BUFFER_SIZE) — counts free slots. Producer waits if buffer full.
- `sem_t full` (init = 0) — counts filled slots. Consumer waits if buffer empty.
- `pthread_mutex_t mutex` — ensures only one thread accesses the buffer at a time.
- `sem_wait()` decrements (blocks if 0). `sem_post()` increments (wakes a blocked thread).

---

# Practical 6: Memory Management — Paging and Segmentation

## 6.1 Paging — Logical to Physical Address Translation

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

## 6.3 Segmentation — Logical to Physical Address Translation

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

## 6.4 Paging vs Segmentation — Quick Comparison

| Aspect        | Paging                              | Segmentation                      |
| ------------- | ----------------------------------- | --------------------------------- |
| Division      | Fixed-size pages                    | Variable-size segments            |
| Address       | Page number + offset                | Segment number + offset           |
| Fragmentation | Internal (unused space within page) | External (gaps between segments)  |
| Table         | Page table (page → frame)           | Segment table (base + limit)      |
| User view     | Transparent to programmer           | Matches logical program structure |
