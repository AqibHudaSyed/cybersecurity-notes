# Linux and SQL for Security Analysts

My notes on operating systems, Linux and SQL: how an OS works, how Linux is built, the Bash commands I use to manage files, permissions and users, and how to filter and join data with SQL.

## Table of contents

1. [Operating systems](#1-operating-systems)
2. [How a computer boots](#2-how-a-computer-boots)
3. [How the OS completes a task](#3-how-the-os-completes-a-task)
4. [Virtual machines](#4-virtual-machines)
5. [GUI vs CLI](#5-gui-vs-cli)
6. [What Linux is](#6-what-linux-is)
7. [Linux architecture](#7-linux-architecture)
8. [Linux distributions](#8-linux-distributions)
9. [Package managers](#9-package-managers)
10. [The shell](#10-the-shell)
11. [Linux file system and file paths](#11-linux-file-system-and-file-paths)
12. [Navigate and read files](#12-navigate-and-read-files)
13. [Filter with grep, pipe and find](#13-filter-with-grep-pipe-and-find)
14. [Manage files and directories](#14-manage-files-and-directories)
15. [File permissions](#15-file-permissions)
16. [Change permissions with chmod](#16-change-permissions-with-chmod)
17. [Manage users with sudo](#17-manage-users-with-sudo)
18. [Get help in Linux](#18-get-help-in-linux)
19. [Databases](#19-databases)
20. [SQL basics](#20-sql-basics)
21. [Filter with WHERE and LIKE](#21-filter-with-where-and-like)
22. [Filter numbers and dates](#22-filter-numbers-and-dates)
23. [AND, OR and NOT](#23-and-or-and-not)
24. [Joins](#24-joins)
25. [Aggregate functions](#25-aggregate-functions)
26. [Quick reference](#26-quick-reference)

---

## 1. Operating systems

An **operating system (OS)** sits between the hardware and the user. It runs many programs at once, talks to devices like printers and keyboards, and turns what I do into instructions the hardware can run. Behind the scenes it also manages the CPU, memory, storage and running processes.

**Hardware** is the physical part of a computer: CPU, memory, disks, keyboard, mouse.

| OS | Released | Source code | Common use |
| --- | --- | --- | --- |
| Windows | 1985 | Closed | Personal and business computers |
| macOS | 1984 | Partly open | Personal and business computers |
| Linux | 1991 | Fully open | Servers and security work |
| ChromeOS | 2011 | Partly open | Schools |
| Android | 2008 | Open | Phones and tablets |
| iOS | 2007 | Partly open | Phones and tablets |

**Legacy OS:** an old OS that is still in use, often because some software only runs on it. It no longer gets updates, so new threats can hit it. Keeping every OS updated is one of the simplest ways to stay secure.

Where to check known OS vulnerabilities:

- Microsoft Security Response Center (MSRC)
- Apple Security Updates
- Ubuntu CVE (Common Vulnerabilities and Exposures) reports
- Google Cloud Security Bulletin

## 2. How a computer boots

```
Power on → BIOS or UEFI → Bootloader → Operating system
```

- **BIOS** (Basic Input/Output System): firmware with the startup instructions, used on older computers.
- **UEFI** (Unified Extensible Firmware Interface): the modern replacement for BIOS, with better security such as Secure Boot.
- **Bootloader:** the program that starts the OS.

Security point: antivirus often does not scan the BIOS, so the boot process can be a target for malware.

## 3. How the OS completes a task

```
User → Application → OS → Hardware → (result goes back the same way)
```

Example: I type a sum in a calculator app. The app sends it to the OS, the OS sends it to the CPU, and the answer comes back to the app.

The OS also **allocates resources** (CPU, memory, storage, input/output) between programs. Task Manager shows this. If a machine is slow, malware may be using its resources.

Knowing this flow helps me trace back where a security event happened.

## 4. Virtual machines

A **virtual machine (VM)** is a computer made in software. It has a virtual CPU, memory and storage, and its own OS. One physical machine can run many VMs.

| Benefit | Why it matters |
| --- | --- |
| Isolation | Each VM is separated from the host and other VMs, so I can open suspicious files or study malware safely (a sandbox) |
| Efficiency | Many VMs on one machine; easy to switch between them |

- A **hypervisor** is the software that creates and manages VMs and shares the host's resources between them.
- **KVM** (Kernel-based Virtual Machine) is an open-source hypervisor built into the Linux kernel.
- Malware can sometimes escape a VM, so I never fully trust a virtual environment.

## 5. GUI vs CLI

| | GUI (Graphical User Interface) | CLI (Command-Line Interface) |
| --- | --- | --- |
| Looks like | Icons and windows | Text only |
| Strength | Easy for beginners | One command can act on many files at once |
| Record of actions | Usually none | Linux keeps a history file of commands |

The history file helps me check that I ran every step of a playbook correctly, and can show what an attacker did on a system.

## 6. What Linux is

**Linux** is an open-source OS. Linus Torvalds wrote the Linux kernel in the early 1990s, and Richard Stallman's GNU project gave the free tools around it. Linux is shared under the GNU General Public License (GPL), so anyone can use, change and share it. There are more than 600 Linux distributions.

As an analyst I use Linux to read logs, check access and permissions, and run security-focused distributions for forensics and pen testing.

## 7. Linux architecture

```
User → Applications → Shell → FHS → Kernel → Hardware
```

| Part | What it does |
| --- | --- |
| User | Starts tasks. Linux lets many users work at the same time |
| Applications | Programs for specific jobs, usually installed with a package manager |
| Shell | The command-line interpreter that passes my commands to the kernel |
| FHS (Filesystem Hierarchy Standard) | The standard that decides where data and directories live |
| Kernel | The core that manages processes, memory and devices, and talks to the hardware |
| Hardware | Physical parts of the machine |

| Hardware type | Examples |
| --- | --- |
| Peripheral (can be added or removed) | Monitor, printer, keyboard, mouse |
| Internal (needed to run) | CPU, RAM (short-term memory), hard drive (long-term storage) |

## 8. Linux distributions

A **distribution (distro)** is a version of Linux: the kernel plus tools, a package manager and an installer.

| Family | Distros |
| --- | --- |
| Debian | Ubuntu, Kali Linux, Parrot |
| Red Hat | Red Hat Enterprise Linux (RHEL), CentOS, AlmaLinux |
| Slackware | SUSE |

| Distro | Key points |
| --- | --- |
| Kali Linux | Debian-based, made for pen testing and digital forensics; best run in a VM |
| Ubuntu | Debian-based, beginner friendly, very common in the cloud |
| Parrot | Debian-based, security tools like Kali, easy GUI |
| RHEL | Paid subscription, built for businesses, comes with support |
| CentOS / AlmaLinux | CentOS was a free RHEL-like distro and has ended; AlmaLinux (and Rocky Linux) replace it |

Common tools in Kali:

| Tool | Use |
| --- | --- |
| Metasploit | Find and exploit vulnerabilities |
| Burp Suite | Test web applications |
| John the Ripper | Guess passwords |
| tcpdump | Capture network traffic from the command line |
| Wireshark | Analyze live or captured traffic with a GUI |
| Autopsy | Forensic analysis of hard drives and phones |

- **Pen test:** a planned, simulated attack to find weaknesses.
- **Digital forensics:** collecting and analyzing data to find out what happened after an attack.

## 9. Package managers

A **package** is software (plus the files it depends on) that installs an application. A **package manager** installs, updates and removes packages. I always prefer the latest version because it has the newest security fixes.

| Family | Package manager | File type | Easier tool |
| --- | --- | --- | --- |
| Debian | dpkg | .deb | APT (Advanced Package Tool) |
| Red Hat | RPM (Red Hat Package Manager) | .rpm | YUM (newer systems use DNF) |

## 10. The shell

The shell reads my commands and sends them to the kernel. Common shells: bash, csh, ksh, tcsh and zsh. **Bash** is the default on most distros and the most used in security. A normal user's prompt is `$` (zsh uses `%`) and the root user's prompt is `#`.

Every command can produce three things:

| Stream | Meaning | Number |
| --- | --- | --- |
| Standard input | What goes into the command (keyboard, file or pipe) | 0 |
| Standard output | The result | 1 |
| Standard error | The error message, for example from a misspelled command | 2 |

```bash
echo hello      # prints: hello
```

## 11. Linux file system and file paths

Everything starts from the root directory `/`.

```
/
├── home    each user's home directory
├── bin     programs (binaries)
├── etc     configuration files
├── tmp     temporary files (anyone can write here, so attackers like it)
└── mnt     mounted drives such as USB sticks
```

| Path type | Starts from | Example |
| --- | --- | --- |
| Absolute | Root `/` | `/home/analyst/projects` |
| Relative | Current directory | `../projects` |

- `~` = my home directory (`~/logs` = `/home/analyst/logs`)
- `.` = current directory, `..` = one level up
- Commands, options and file names are case-sensitive.
- An **argument** is the extra information a command needs (like a file name). An **option** changes how a command behaves and usually starts with `-`.

## 12. Navigate and read files

| Command | What it does |
| --- | --- |
| `pwd` | Shows the directory I am in |
| `whoami` | Shows my username |
| `ls` | Lists files and directories |
| `cd projects` / `cd ..` | Moves into a directory / one level up |
| `cat file` | Shows the whole file |
| `head file` | First 10 lines (`head -n 5 file` for 5 lines) |
| `tail file` | Last 10 lines, handy for the newest log entries |
| `less file` | One page at a time (Space = next page, b = back, q = quit) |

## 13. Filter with grep, pipe and find

```bash
grep error time_logs.txt                       # lines in the file that contain "error"
ls /home/analyst/reports | grep users          # names that contain "users"
find /home/analyst/projects -name "*log*"      # names with "log" (case-sensitive)
find /home/analyst/projects -iname "*log*"     # same, ignoring case
find /home/analyst/projects -mtime -3          # changed in the last 3 days
find /home/analyst/projects -mmin -60          # changed in the last 60 minutes
```

- `grep` searches the **lines inside** a file.
- The pipe `|` sends one command's output into the next command.
- `find` searches for **files and directories** by name, size or time. `*` matches any characters.

## 14. Manage files and directories

| Command | What it does |
| --- | --- |
| `mkdir name` | Makes a directory |
| `rmdir name` | Removes an empty directory |
| `touch file` | Makes an empty file |
| `rm file` | Deletes a file (hard to recover) |
| `mv file place` | Moves a file, or renames it (`mv old.txt new.txt`) |
| `cp file place` | Copies a file and keeps the original |
| `nano file` | Opens a simple text editor (Ctrl+O save, Ctrl+X exit) |

```bash
echo "time" > notes.txt           # > replaces the whole file
echo "updated" >> notes.txt       # >> adds to the end
```

Both `>` and `>>` create the file if it does not exist.

## 15. File permissions

| Permission | On a file | On a directory |
| --- | --- | --- |
| r (read) | Read the content | List what is inside |
| w (write) | Change the content | Create, delete or rename files inside |
| x (execute) | Run it as a program | Enter the directory |

Permissions are set for three owner types: **user** (the owner), **group** and **other** (everyone else).

```
-  rw-  r--  r--
│   │    │    └── other
│   │    └─────── group
│   └──────────── user
└──────────────── type: d = directory, - = file
```

| Command | Shows |
| --- | --- |
| `ls -l` | Permissions, owner, group, size, date |
| `ls -a` | Hidden files too (names starting with `.`) |
| `ls -la` | Both |

A file that user, group and other can all write to is **world-writable**, and that is a big risk.

## 16. Change permissions with chmod

| Part | Meaning |
| --- | --- |
| `u` `g` `o` | user, group, other |
| `+` `-` `=` | add, remove, set exactly |
| `r` `w` `x` | read, write, execute |

```bash
chmod g+w,o-r access.txt        # give group write, take read from other
chmod u=r,g=r,o=r report.txt    # everyone gets only read
chmod g-rw bonuses.txt          # least privilege: only the owner keeps access
chmod 640 file.txt              # number form: r=4, w=2, x=1 → rw-r-----
```

No spaces after the commas. The **principle of least privilege** means giving only the access a person needs for their job.

## 17. Manage users with sudo

The **root user** can do anything on the system. Working as root is risky:

1. Attackers target the root account.
2. One wrong command can cause damage that cannot be undone.
3. Nobody can tell which person ran a command.

`sudo` runs one command with higher rights, using my own password. Only users listed in the **sudoers** file can use it.

| Command | What it does |
| --- | --- |
| `sudo useradd fgarcia` | Adds a user |
| `sudo useradd -g security fgarcia` | Sets the primary group |
| `sudo useradd -G finance,admin fgarcia` | Adds to extra (supplemental) groups |
| `sudo usermod -a -G marketing fgarcia` | Adds an existing user to another group (without `-a`, old groups are replaced) |
| `sudo usermod -L fgarcia` | Locks the account |
| `sudo userdel -r fgarcia` | Deletes the user and their home files |
| `sudo chown fgarcia access.txt` | Changes the file owner |
| `sudo chown :security access.txt` | Changes the group owner |

Authentication checks **who** a user is. Authorization decides **what** they can access.

## 18. Get help in Linux

| Command | Use |
| --- | --- |
| `man chown` | Full manual page for a command |
| `whatis tail` | One-line description |
| `apropos password` | Searches manual descriptions for a word |
| `apropos -a change password` | Results that contain all the words |

The Unix & Linux Stack Exchange is a good place for community answers.

## 19. Databases

A **relational database** stores data in tables that link to each other. Columns are fields, rows are records. Many people can use it at the same time and it handles far more data than a spreadsheet.

| | Primary key | Foreign key |
| --- | --- | --- |
| Meaning | Unique ID for each row | A column that is the primary key of another table |
| Duplicates or empty values | Not allowed | Allowed |
| Per table | Only one | Many |
| Job | Identify a row | Link two tables |

## 20. SQL basics

**SQL** (Structured Query Language) is the language for asking a database for data. A **query** is one such request. Logs often live in databases, and one query can search millions of rows in seconds.

```sql
SELECT employee_id, device_id
FROM employees;

SELECT *
FROM customers
ORDER BY city DESC;
```

- `SELECT` picks columns (`*` = all), `FROM` picks the table, `;` ends the query.
- `ORDER BY` sorts ascending by default; add `DESC` for descending.
- Keywords are not case-sensitive; I write them in capitals so queries are easy to read.

| | Linux filtering | SQL filtering |
| --- | --- | --- |
| Works on | Files and directories | Tables in a database |
| Output | Plain lines of text | Neat columns |
| Join data | No | Yes |
| Best for | Text files and logs | Structured data |

## 21. Filter with WHERE and LIKE

```sql
SELECT *
FROM log_in_attempts
WHERE country = 'USA';

SELECT *
FROM employees
WHERE office LIKE 'East%';
```

| Wildcard | Matches | Example pattern | Matches |
| --- | --- | --- | --- |
| `%` | Any number of characters | `'East%'` | East-170, East-320 |
| `_` | Exactly one character | `'N_'` | NY, NV |

Use `LIKE` (not `=`) with wildcards.

## 22. Filter numbers and dates

| Operator | Meaning |
| --- | --- |
| `=` | equal |
| `<>` or `!=` | not equal |
| `>` `<` | greater / less than (does not include the value) |
| `>=` `<=` | greater / less than or equal (includes the value) |
| `BETWEEN ... AND ...` | a range, both ends included |

```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00';

SELECT firstname, lastname, hiredate
FROM employees
WHERE hiredate BETWEEN '2002-01-01' AND '2003-01-01';
```

Text, dates and times go in quotes. Numbers do not.

## 23. AND, OR and NOT

| Operator | Returns rows where |
| --- | --- |
| `AND` | Both conditions are true |
| `OR` | At least one condition is true |
| `NOT` | The condition is false |

```sql
SELECT *
FROM machines
WHERE operating_system = 'OS 1' AND email_client = 'Email Client 1';

SELECT *
FROM customers
WHERE country = 'Canada' OR country = 'USA';

SELECT *
FROM customers
WHERE NOT country = 'Canada' AND NOT country = 'USA';
```

- With `OR` on one column, write the full condition both times.
- `NOT` goes right after `WHERE`.

## 24. Joins

```sql
SELECT username, office, operating_system
FROM employees
INNER JOIN machines ON employees.employee_id = machines.employee_id;
```

| Join | Returns |
| --- | --- |
| `INNER JOIN` | Only rows that match in both tables |
| `LEFT JOIN` | All rows from the left (FROM) table + matches from the right |
| `RIGHT JOIN` | All rows from the right (JOIN) table + matches from the left |
| `FULL OUTER JOIN` | All rows from both tables |

- Write `table.column` when both tables have a column with the same name.
- Missing values show as `NULL`.
- MySQL and MariaDB do not support `FULL OUTER JOIN` directly; combine a LEFT and a RIGHT join with `UNION`.

## 25. Aggregate functions

```sql
SELECT COUNT(firstname)
FROM customers
WHERE country = 'USA';
```

| Function | Returns |
| --- | --- |
| `COUNT` | Number of rows (`COUNT(column)` skips NULL, `COUNT(*)` counts every row) |
| `AVG` | Average of a number column |
| `SUM` | Total of a number column |

## 26. Quick reference

| Task | Linux | SQL |
| --- | --- | --- |
| Find text | `grep "word" file` | `WHERE column LIKE '%word%'` |
| Pattern / wildcard | `*` | `%` and `_` |
| Combine data | pipe `\|` | `JOIN` |
