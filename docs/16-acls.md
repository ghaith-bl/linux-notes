# 16. Access Control Lists (ACLs)

## 16.1 Concept

- Extends the standard `rwx` owner/group/others permission model to allow fine-grained permissions for **specific additional users or groups** on a file/directory.
- When a file has ACLs, `ls -l` shows a `+` at the end of the permission string (e.g., `rwxrw-r--+`).

## 16.2 Viewing ACLs

```bash
getfacl file.txt
```

## 16.3 Setting ACLs

```bash
setfacl -m u:alice:rwx file.txt      # Grant user alice rwx
setfacl -m g:devteam:rx file.txt     # Grant group devteam r-x
setfacl -R -m u:alice:rwx dir/       # Apply recursively to a directory
```

## 16.4 Default ACLs (Inheritance for Directories)

```bash
setfacl -d -m u:alice:rwx /shared/   # New files/dirs created inside inherit this ACL
```

## 16.5 Removing ACLs

```bash
setfacl -x u:alice file.txt   # Remove a specific ACL entry
setfacl -b file.txt           # Remove ALL ACL entries
```
