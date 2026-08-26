# 4. Permissions

## 4.1 Permissions Model

- **Concept:** Controlling who can do what with files and directories.
- **Permission Types:** Read (`r`), Write (`w`), Execute (`x`).
- **Permission Categories (Classes):** User/Owner (`u`), Group (`g`), Others (`o`).
- **Viewing Permissions (`ls -l`):** Output shows 10 characters (e.g., `rwxr-xr--`).
  - 1st char: File type (`-` file, `d` directory, `l` link).
  - Next 9 chars: `rwx` for user, `rwx` for group, `rwx` for others.

**Meaning for Files:**
- `r` : View content.
- `w` : Modify content.
- `x` : Run as a program/script.

**Meaning for Directories:**
- `r` : List contents (`ls`).
- `w` : Create, delete, rename files within the directory.
- `x` : Enter the directory (`cd`).

### Example breakdown (`ls -lah`)

```
-rwxrw-r-- 1 root root 730 Jul 28 07:39 test.txt
```
- 1st field: shows if it's a directory (`d`) or file (`-`).
- 3 fields (2nd, 3rd, 4th): related to Owner.
- 3 fields (5th, 6th, 7th): related to Group.
- 3 fields (8th, 9th, 10th): related to Others.

## 4.2 Changing Permissions (`chmod`)

- **Concept:** Modifying access rights.

**Symbolic Mode:** `chmod [ugoa][+-=][rwx] <file/dir>`
- Classes: `u` (user), `g` (group), `o` (others), `a` (all).
- Operators: `+` (add), `-` (remove), `=` (set exactly).
- Permissions: `r`, `w`, `x`.
- Examples:
  ```bash
  chmod u+x script.sh
  chmod go-w data.txt
  chmod a=r public.txt
  ```

**Octal (Numeric) Mode:** `chmod <###> <file/dir>`
- Each digit represents u, g, o respectively.
- Values: `execute(x) = 1`, `write(w) = 2`, `read(r) = 4`. Sum values for desired permissions:
  - `rwx = 4+2+1 = 7`
  - `rw- = 4+2 = 6`
  - `r-x = 4+1 = 5`
  - `r-- = 4`
- Examples:
  ```bash
  chmod 755 script.sh   # rwxr-xr-x
  chmod 644 data.txt    # rw-r--r--
  chmod 777 file.txt    # rwxrwxrwx
  ```
- Add execute for the owner only:
  ```bash
  chmod u+x file.txt
  ```

## 4.3 Changing Ownership (`chown`, `chgrp`)

- **Concept:** Transferring ownership of files/directories.
- **Change Owner & Group (`chown`):** `chown [options] owner:group <file/dir>`
  ```bash
  chown alice:admins file.txt
  ```
  Colon and group are optional.
- **Change Group Only (`chgrp`):** `chgrp <group> <file/dir>`
  ```bash
  chgrp admins file.txt
  ```
- **Recursive Option:** `-R` applies changes to directories and their contents.

## 4.4 Extended Attributes (`chattr`)

- **Prevent any modification of the file:**
  ```bash
  chattr +i filename
  ```
- **Remove the prevention:**
  ```bash
  chattr -i filename
  ```
- **Allow only append (append-only):**
  ```bash
  chattr +a filename
  ```
- **No-Access Time (A):** Prevents the file's access time from being updated.
  ```bash
  chattr +A filename
  ```
- **Restricted Deletion (d):** Prevents a file from being deleted or renamed by users who do not own the file, even if they have write permissions.
  ```bash
  chattr +d filename
  ```

## 4.5 Privilege Escalation (`sudo`)

- **Concept:** Executing commands with the privileges of another user (typically root).
- **Stands for:** Super User Do.
- **Usage:** `sudo <command_to_run>` (e.g., `sudo apt update`).
- **Password:** Prompts for *your* user password (not the root password) by default.
- **Security:** Preferred over logging in as root directly. Grants temporary elevated rights for specific commands.
- **Configuration (`/etc/sudoers`):** Defines which users/groups can run which commands as whom. Edit **ONLY** with the `visudo` command (prevents syntax errors).
- **Switching to Root Shell:** `sudo su -` or `sudo -i`. Requires root privileges or sudo configuration. Use `exit` to return to your user shell.
