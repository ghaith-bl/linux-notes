# 3. Users & Groups

## 3.1 Concept

Managing accounts and group memberships in a multi-user system.

- **User Identity:** Each user has a unique username and User ID (UID). The root user (UID 0) has ultimate privileges.
- **Group Identity:** Users belong to one primary group and potentially multiple secondary groups (Group ID - GID).
- **Identify Current User:** `whoami` command or check the terminal prompt.

## 3.2 Essential Files for Users and Groups

- `/etc/passwd` : User account info (username, UID, GID, home directory, default shell). Not passwords.
- `/etc/group` : Group definitions and memberships.
- `/etc/shadow` : Encrypted (hashed) passwords and password policy information. Only readable by root.
- `/etc/gshadow`
- `/home/{username}`
- `/etc/skel` => contains default files copied to the home directory of every new user.
- `/etc/login.defs`
- `/etc/sudoers`

Example sudoers entry:
```
kali ALL=(ALL) NOPASSWD: ALL
```

## 3.3 Adding, Deleting, Modifying User Accounts

**Add new user:**
```bash
useradd -m -s /bin/bash -G company HR
```

**Change the password:**
```bash
passwd {username}
```

**Delete user:**
```bash
userdel -r HR
```

**Modify user:**

- Change the user's home directory:
  ```bash
  usermod -d /new/directory {user}
  ```
- Change the username of a specific user:
  ```bash
  usermod -l newusername {user}
  ```
- Change the login shell:
  ```bash
  usermod -s /bin/zsh {user}
  ```
- Change the groups (removes/replaces the previous groups):
  ```bash
  usermod -G group1,group2 {user}
  ```
- Add user to a new group **without** deleting the previous groups:
  ```bash
  usermod -aG newgroup {user}
  ```

**Listing user information:**
```bash
id {username}
```

**Lock user account (prevent login):**
```bash
passwd -l {username}
```

**Unlock account (permit login again):**
```bash
passwd -u {username}
```

Other ways to lock an account:
```bash
usermod -s /sbin/nologin username   # change shell to nologin
usermod -s /bin/false username
```

## 3.4 Managing Groups

**Add new group (with optional id):**
```bash
groupadd {groupname}
groupadd {groupname} -g {GID}
```
Example:
```bash
groupadd HR -g 1111
```

**Delete group:**
```bash
groupdel {groupname}
```

**Rename group name:**
```bash
groupmod {old_name} -n {new_Group_name}
```

**Change the GID of the group:**
```bash
groupmod -g 2000 {groupname}
```

**Add a user to a group:**
```bash
usermod -aG groupname username
```

**Remove a user from a group:**
```bash
sudo gpasswd -d username groupname
```

**Know the groups that a username belongs to:**
```bash
groups username
```

**Get more information about a group:**
```bash
getent group groupname
```

**Change the primary group for a username:**
```bash
usermod -g {newgroup} {username}
```

**Set a password for the group:**
```bash
gpasswd {groupname}
```

## 3.5 Password Aging (`chage`)

**Get information about a user's password expiration:**
```bash
chage -l username
```

**Set password policy:**
```bash
chage [option] username
```

Options:
- `-m days` => set the minimum number of days before the password can be changed.
- `-M days` => set the maximum number of days before the password needs to be changed.
- `-W days` => set the number of days to warn before the password expires.
- `-I days` => Sets the number of inactive days after a password expires before the account is locked.
- `-E date` => Sets an account expiration date in the format `YYYY-MM-DD`.

**Force a user to change their password on first login:**
```bash
passwd -e username
```

### `/etc/shadow` Fields

Example line:
```
admin:$y$j9T$CbCTLnmDfJaWMDz6EaxEF0$wgVb2ruLvNfM0kvAqLglnnQb/K2VgzEDxqeRD4kRCS4:19957:0:99999:7:::
```

| Field | Meaning |
|---|---|
| 1 | user |
| 2 | user's password hash (bcrypt) |
| 3 | when the password was last changed (days since 1970-1-1) |
| 4 | minimum number of days before the password can be changed |
| 5 | maximum number of days before the password needs to be changed |
| 6 | days to warn the user before password expiration (e.g. before 7 days) |
| 7 | days after password expiration and before the account is locked |
| 8 | account expiration date (number of days since 1970) |

## 3.6 `/etc/skel` Directory

Contains the default configuration files copied into the home directory of every new user.

If you need to add a new file to every new user's home directory:
```bash
nano /etc/skel/newfile.txt
useradd -m hossamshady
```

## 3.7 Graphical User & Group Administration

- Open Settings.
- Navigate to Users.
- Now you can add, modify, and delete users.

```bash
sudo apt install gnome-system-tools gnome-system-tools
# or
sudo apt install kuser
# or
sudo apt install cockpit
sudo systemctl start cockpit
```
Access it via a web browser at `http://localhost:9090`.
