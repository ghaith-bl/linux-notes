# 2. File System Management

## 2.1 Creating Files & Directories

- **Concept:** Adding new items to the filesystem.
- **Create Empty File / Update Timestamp (`touch`):** `touch <filename>`
  - Example: `touch report.txt`
- **Create Directory (`mkdir`):** `mkdir <dirname>`
  - Example: `mkdir project_files`
  - `mkdir -p <path/to/nested/dir>` : Create parent directories as needed.

## 2.2 Viewing & Reading Files

- **Concept:** Displaying the content of text files.
- **Concatenate (`cat`):** `cat <filename>` (Displays the entire file content to the terminal).
- **Pagers (`less`, `more`):**
  - `less <filename>` : Interactive viewer (scroll up/down, search `/`, quit `q`). Preferred.
  - `more <filename>` : Older, less interactive pager (spacebar for next page, `q` to quit).
- **Show Beginning (`head`):** `head <filename>` (Shows first 10 lines by default).
  - Example: `head -n 20 <filename>` (Shows first 20 lines).
- **Show End (`tail`):** `tail <filename>` (Shows last 10 lines by default).
  - Example: `tail -n 20 <filename>` (Shows last 20 lines).
  - `tail -f <logfile>` : Follow mode - continuously displays new lines added to the file (useful for logs).

## 2.3 Editing Files

- **Concept:** Modifying the content of text files.
- **Nano (`nano`):** Simple, beginner-friendly terminal text editor. Commands shown at the bottom (e.g., `Ctrl+O` Save, `Ctrl+X` Exit).
- **Vim (`vim`):** Powerful, modal text editor (steeper learning curve). Modes: Normal (commands), Insert (typing), Visual (selection).

## 2.4 Copying Files & Directories (`cp`)

- **Concept:** Duplicating files and directories.
- **Copy File:** `cp <source_file> <destination_file>` or `cp <source_file> <destination_directory/>`.
- **Copy Directory (Recursive):** `cp -r <source_directory> <destination_directory>`.
- **Options:** `i` (interactive prompt before overwrite), `v` (verbose output).

## 2.5 Moving & Renaming Files & Directories (`mv`)

- **Concept:** Relocating or renaming filesystem objects.
- **Move:** `mv <source> <destination_directory/>`.
- **Rename:** `mv <old_name> <new_name>` (if source and destination are in the same directory).
- **Options:** `i` (interactive prompt before overwrite), `v` (verbose output).

## 2.6 Deleting Files & Directories (`rm`, `rmdir`)

- **Concept:** Removing items from the filesystem.
- **Remove File (`rm`):** `rm <filename>`.
  - Options: `i` (interactive), `f` (force, suppress prompts - **use with extreme caution!**), `r` (recursive for directories).
- **Remove Empty Directory (`rmdir`):** `rmdir <directory_name>` (Only works if the directory is empty).
- **Remove Directory Recursively (`rm -r`):** `rm -r <directory_name>` (Deletes the directory and ALL its contents. **Irreversible! Be careful!**).

## 2.7 Filesystem Types

- **EXT4 (Extended File System family version 4)**
  - Supports large files up to 1000 TB.
  - Faster than previous versions.
  - Use Case: Modern Linux systems (default for many distributions), general-purpose usage.

- **NTFS (New Technology File System)**
  - Support for large files and volumes.
  - File-level encryption (EFS).
  - Use Case: Windows operating systems, external drives shared between Windows and Linux.

- **ISO 9660**
  - File system for optical media (CDs and DVDs).
  - Use Case: Optical discs (CDs, DVDs), often used for bootable media.

- **NFS (Network File System)**
  - Allows file access over a network.
  - Commonly used in enterprise and server environments.

- **SMB/CIFS (Server Message Block/Common Internet File System)**
  - Protocol for network file sharing, primarily between Windows and other systems.
  - Allows remote file access, printing, and more over a network.
