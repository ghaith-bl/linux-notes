# 13. Combined Linux Command Reference Table

This table provides a quick reference to common Linux commands, grouped by category.

| Category | Command | Description | Example / Common Options |
|---|---|---|---|
| Navigation | `pwd` | Print Working Directory (show current location) | `pwd` |
| Navigation | `cd` | Change Directory | `cd /etc`, `cd ..`, `cd ~`, `cd -` |
| File System | `ls` | List directory contents | `ls -l`, `ls -a`, `ls -h`, `ls -la`, `ls -R` (recursive) |
| File System | `mkdir` | Make Directory | `mkdir new_dir`, `mkdir -p path/to/nested/dir` |
| File System | `rmdir` | Remove Empty Directory | `rmdir empty_dir` |
| File System | `touch` | Create empty file or update modification timestamp | `touch new_file.txt` |
| File System | `cp` | Copy files or directories | `cp file1 file2`, `cp -r dir1 dir2`, `cp -i` (interactive) |
| File System | `mv` | Move or rename files or directories | `mv old new`, `mv file dir/`, `mv -i` (interactive) |
| File System | `rm` | Remove files or directories | `rm file.txt`, `rm -r dir/` (recursive), `rm -f` (force) |
| File Viewing | `cat` | Concatenate and display file content | `cat file.txt` |
| File Viewing | `less` | Interactive file pager (scroll, search) | `less file.log` (use `/` to search, `q` to quit) |
| File Viewing | `more` | Basic file pager | `more file.txt` (use spacebar, `q` to quit) |
| File Viewing | `head` | Output the first part of files | `head file.txt`, `head -n 20 file.txt` (first 20 lines) |
| File Viewing | `tail` | Output the last part of files | `tail file.txt`, `tail -n 20 file.txt`, `tail -f log.txt` |
| File Editing | `nano` | Simple terminal text editor | `nano file.txt` (Ctrl+O Save, Ctrl+X Exit) |
| File Editing | `vim` | Powerful modal text editor | `vim file.txt` (i=insert, Esc=normal, :wq=save&quit) |
| Permissions | `chmod` | Change file mode bits (permissions) | `chmod 755 file`, `chmod u+x file`, `chmod go-w file` |
| Permissions | `chown` | Change file owner and group | `sudo chown user:group file`, `sudo chown -R user dir/` |
| Permissions | `chgrp` | Change group ownership | `sudo chgrp group file`, `sudo chgrp -R group dir/` |
| Permissions | `chattr` | Change extended file attributes | `chattr +i file`, `chattr +a file`, `chattr +A file` |
| User/Group Mgmt | `whoami` | Print effective user ID | `whoami` |
| User/Group Mgmt | `id` | List user information (UID, GID, groups) | `id username` |
| User/Group Mgmt | `useradd` | Create a new user | `sudo useradd -m -s /bin/bash newuser` |
| User/Group Mgmt | `groupadd` | Create a new group | `sudo groupadd newgroup` |
| User/Group Mgmt | `usermod` | Modify a user account | `sudo usermod -aG group user` (add to group) |
| User/Group Mgmt | `passwd` | Update user's password / lock-unlock account | `passwd`, `sudo passwd username`, `passwd -l`, `passwd -u` |
| User/Group Mgmt | `userdel` | Delete a user account | `sudo userdel -r username` |
| User/Group Mgmt | `groupdel` | Delete a group | `sudo groupdel groupname` |
| User/Group Mgmt | `groupmod` | Rename group / change GID | `groupmod old -n new`, `groupmod -g 2000 group` |
| User/Group Mgmt | `gpasswd` | Remove user from group / set group password | `sudo gpasswd -d username groupname` |
| User/Group Mgmt | `chage` | Manage password aging policy | `chage -l username`, `chage -M 90 username` |
| User/Group Mgmt | `groups` | Show groups a user belongs to | `groups username` |
| User/Group Mgmt | `getent` | Get entries from administrative databases | `getent group groupname` |
| User/Group Mgmt | `who` / `last` / `w` / `users` | Show who is logged in to the server | `who`, `last`, `w`, `users` |
| Privilege Escalation | `sudo` | Execute a command as another user (root by default) | `sudo apt update`, `sudo -i` or `sudo su -` (root shell) |
| Privilege Escalation | `visudo` | Edit the `/etc/sudoers` file safely | `sudo visudo` |
| Process Mgmt | `ps` | Report a snapshot of current processes | `ps`, `ps aux`, `ps -ef` |
| Process Mgmt | `top` | Display Linux processes (interactive) | `top` (q=quit) |
| Process Mgmt | `htop` | Interactive process viewer (enhanced) | `htop` (q=quit, F9=kill) |
| Process Mgmt | `kill` | Send signal to a process (terminate by default) | `kill <PID>`, `kill -9 <PID>` (force), `kill -l` (list signals) |
| Process Mgmt | `pkill` | Send signal to processes based on name | `pkill firefox`, `pkill -9 nginx` |
| Networking | `ip` | Show / manipulate routing, devices, policy routing | `ip a` (addr), `ip r` (route), `ip link` |
| Networking | `ifconfig` | Configure network interface parameters (older) | `ifconfig` (may need `net-tools`) |
| Networking | `ping` | Send ICMP ECHO_REQUEST to network hosts | `ping google.com`, `ping -c 4 8.8.8.8` (4 packets) |
| Networking | `netstat` | Print network connections, routing tables, etc. (older) | `netstat -tulnp` (listening ports) (may need `net-tools`) |
| Networking | `ss` | Socket statistics (modern replacement for netstat) | `ss -tulnp` (listening ports) |
| Networking | `curl` | Transfer data from or to a server | `curl http://example.com`, `curl -O <url>` (save) |
| Networking | `wget` | Non-interactive network downloader | `wget http://example.com/file.zip` |
| Networking | `dig` | DNS lookup utility (detailed) | `dig example.com`, `dig @8.8.8.8 example.com` |
| Networking | `host` | DNS lookup utility (simple) | `host google.com` |
| Package Mgmt | `apt` | APT package handling utility (Debian/Ubuntu) | `sudo apt update`, `sudo apt install pkg`, `sudo apt remove pkg` |
| Package Mgmt | `apt-get` | Older APT package handling utility | `sudo apt-get update`, `sudo apt-get install pkg` |
| Package Mgmt | `dpkg` | Package manager for Debian (lower-level) | `sudo dpkg -i pkg.deb`, `dpkg -l` (list) |
| Package Mgmt | `dnf` | DNF package manager (Fedora, newer RHEL/CentOS) | `sudo dnf update`, `sudo dnf install pkg`, `sudo dnf remove pkg` |
| Package Mgmt | `yum` | YUM package manager (older RHEL/CentOS) | `sudo yum update`, `sudo yum install pkg`, `sudo yum remove pkg` |
| Package Mgmt | `rpm` | RPM Package Manager (lower-level) | `sudo rpm -ivh pkg.rpm`, `rpm -qa` (list) |
| Service Mgmt | `systemctl` | Control the systemd system and service manager | `sudo systemctl status sshd`, `start`, `stop`, `restart`, `enable`, `disable` |
| Text Processing | `grep` | Print lines matching a pattern | `grep "pattern" file`, `grep -i`, `grep -v`, `grep -r`, `grep -E` |
| Text Processing | `sed` | Stream editor for filtering and transforming text | `sed 's/old/new/g' file`, `sed '/pattern/d' file` |
| Text Processing | `awk` | Pattern scanning and processing language | `awk '{print $1}' file`, `awk -F':' '{print $1}' /etc/passwd` |
| Text Processing | `cut` | Remove sections from each line of files | `cut -d':' -f1 /etc/passwd`, `cut -c 1-10 file` |
| Text Processing | `sort` | Sort lines of text files | `sort file`, `sort -n` (numeric), `sort -r` (reverse), `sort -u` |
| Text Processing | `uniq` | Report or omit repeated adjacent lines | `sort file \| uniq -c` |
| Text Processing | `tr` | Translate or delete characters | `cat file \| tr 'a-z' 'A-Z'` |
| Bash Scripting | `read` | Read from standard input into shell variables | `read var`, `read -p "Prompt: " var`, `read -s` (silent) |
| Bash Scripting | `echo` | Display a line of text | `echo "Hello $USER"`, `echo -e "Line1\nLine2"` |
| Bash Scripting | `printf` | Format and print data | `printf "Name: %s\nID: %d\n" "User" 123` |
| Bash Scripting | `test` or `[` | Check file types and compare values (older) | `[ -f file ]`, `[ "$a" = "$b" ]` |
| Bash Scripting | `[[` | Check file types and compare values (newer, Bash) | `[[ -f file ]]`, `[[ "$a" == "$b" ]]`, `[[ $n -gt 5 ]]` |
| Bash Scripting | `let` | Perform arithmetic on shell variables | `let COUNT++`, `let SUM=a+b` |
| Bash Scripting | `$(( ))` | Arithmetic expansion | `echo $((5 + 3))`, `SUM=$((a + b))` |
| Bash Scripting | `date` | Print or set the system date and time | `date`, `date +%Y-%m-%d`, `date +%s` (timestamp) |
| Bash Scripting | `sleep` | Delay for a specified amount of time | `sleep 5` (seconds), `sleep 1m` (minute) |
| Bash Scripting | `exit` | Cause the shell or script to exit | `exit 0` (success), `exit 1` (failure) |
| Archiving | `tar` | Tape Archiver utility (bundle files) | `tar -cvf a.tar dir/`, `tar -xvf a.tar`, `tar -czvf a.tgz dir/` |
| Archiving | `gzip` | Compress or expand files (GNU Zip) | `gzip file` (creates file.gz) |
| Archiving | `gunzip` | Decompress files compressed by gzip | `gunzip file.gz` |
| Archiving | `zip` | Package and compress (archive) files | `zip archive.zip file1 dir/`, `zip -r archive.zip dir/` |
| Archiving | `unzip` | List, test and extract compressed files in a ZIP archive | `unzip archive.zip` |
| Help | `man` | Display manual pages for commands | `man ls`, `man 5 passwd` |
| Help | `--help` | Display help message for a command | `ls --help`, `grep --help` |
