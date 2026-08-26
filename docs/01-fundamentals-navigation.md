# 1. Linux Fundamentals & Navigation

## 1.1 Core Concepts & Terminal Basics

- **Concept:** Understanding the Linux environment, the role of the terminal, and basic interaction.
- **Terminal Prompt:** Typically shows `username@hostname:current_directory$` (e.g., `kali@kali:~$`).
  - `~` represents the user's home directory.
  - `$` indicates a regular user, `#` indicates the root user.
- **GUI vs. CLI:** Linux supports both (Graphical User Interface vs. Command Line Interface), but proficiency in the CLI/terminal is crucial for administration and security tasks.

## 1.2 Filesystem Hierarchy Standard (FHS)

- **Concept:** A standardized layout for Linux directories.
- **Key Directories:**
  - `/` : Root directory, the base of the filesystem.
  - `/bin` : Essential user binaries (commands).
  - `/sbin` : Essential system binaries (admin commands).
  - `/etc` : System configuration files.
  - `/home` : User home directories (e.g., `/home/kali`).
  - `/root` : Home directory for the root user.
  - `/var` : Variable files (logs, spool files, etc.).
  - `/tmp` : Temporary files.
  - `/usr` : User programs and data (binaries, libraries, docs).
  - `/dev` : Device files.
  - `/proc`, `/sys` : Virtual filesystems providing kernel/system information.

## 1.3 Navigation

- **Concept:** Moving around the filesystem using the terminal.
- **Print Working Directory (`pwd`):** Shows the full path of the current directory.
- **Change Directory (`cd`):**
  - `cd <path>` : Move to the specified directory (e.g., `cd /etc`, `cd Documents`).
  - `cd ..` : Move one level up.
  - `cd ~` or `cd` : Move to the current user's home directory.
  - `cd -` : Move to the previous directory.
- **Paths:**
  - Absolute Path: Starts from the root directory (`/`) (e.g., `/home/kali/Documents`).
  - Relative Path: Starts from the current directory (e.g., `../Pictures`, `scripts/run.sh`).
- **Tab Completion:** Pressing `Tab` auto-completes directory/file names or shows possible completions.

## 1.4 Listing Files (`ls`)

- **Concept:** Viewing the contents of directories.
- **Basic Usage:** `ls` (lists non-hidden files/dirs in the current directory).
- **Common Options:**
  - `l` : Long listing format (shows permissions, owner, group, size, modification date, name).
  - `a` : All files, including hidden files (those starting with `.`).
  - `h` : Human-readable file sizes (e.g., KB, MB, GB).
  - `R` : Recursive listing (shows contents of subdirectories).
  - Combined: `ls -lah` is very common.
- **Hidden Files:** Files/directories starting with `.` are hidden by default (e.g., `.bashrc`, `.config`). Use `ls -a` to see them.

## 1.5 Who's Logged In

To know who is logged in to your server:

```bash
who
last
w
users
```
