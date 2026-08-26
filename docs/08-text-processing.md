# 8. Text Processing & Manipulation

## 8.1 Searching Text (`grep`)

- **Concept:** Finding lines that match a specific pattern within files or input streams.
- **Stands for:** Global Regular Expression Print.
- **Basic Usage:** `grep <pattern> <filename(s)>` (e.g., `grep "error" /var/log/syslog`).
- **Piping Input:** Can take input from other commands (e.g., `ls -l | grep "myfile"`).
- **Common Options:**
  - `i` : Case-insensitive search.
  - `v` : Invert match (show lines *not* matching the pattern).
  - `r` or `R` : Recursive search through directories.
  - `n` : Show line numbers with matches.
  - `E` : Use Extended Regular Expressions (more powerful patterns).
  - `c` : Count matching lines.
  - `w` : Match whole words only.

## 8.2 Stream Editing (`sed`)

- **Concept:** Performing basic text transformations on an input stream or file (non-interactively).
- **Common Use: Substitution:** `sed 's/old_pattern/new_string/g' <filename>`
  - `s` : Substitute command.
  - `/` : Delimiter (can be other chars like `#` or `|`).
  - `old_pattern` : Text or regex to find.
  - `new_string` : Replacement text.
  - `g` : Global flag (replace all occurrences on a line, not just the first).
- **Other Uses:** Deleting lines (`sed '/pattern/d'`), printing specific lines (`sed -n '/pattern/p'`).

## 8.3 Pattern Scanning & Processing (`awk`)

- **Concept:** Powerful language for processing text files, especially structured/columnar data.
- **Basic Structure:** `awk 'pattern { action }' <filename>`.
- **Field Separator:** Defaults to whitespace. Fields accessed as `$1`, `$2`, etc. `$0` is the whole line.
- Example: `awk -F':' '{print $1}' /etc/passwd` (Uses `:` as delimiter, prints the first field - usernames).
- **Capabilities:** Can perform calculations, use variables, conditional logic, loops within the `action` block.

## 8.4 Extracting Sections (`cut`)

- **Concept:** Removing sections (columns/fields) from each line of a file.
- **Options:**
  - `-d <delimiter>` : Specify the field delimiter (default is Tab).
  - `-f <field_list>` : Specify which fields to extract (e.g., `-f 1,3`, `-f 1-3`).
- Example: `cut -d':' -f1,6 /etc/passwd` (Extract username and home directory).

## 8.5 Sorting Lines (`sort`)

- **Concept:** Arranging lines of text files alphabetically or numerically.
- **Basic Usage:** `sort <filename>`.
- **Common Options:**
  - `n` : Numeric sort.
  - `r` : Reverse the result.
  - `k <field_number>` : Sort based on a specific field.
  - `t <delimiter>` : Specify field delimiter (used with `k`).
  - `u` : Unique - output only the first of an equal sequence.

## 8.6 Filtering Duplicates (`uniq`)

- **Concept:** Reporting or filtering repeated **adjacent** lines (often used after `sort`).
- **Basic Usage:** `uniq <filename>` (Prints unique adjacent lines).
- **Common Options:**
  - `c` : Count occurrences of each line.
  - `d` : Only print duplicate lines.
  - `u` : Only print unique lines.
- **Typical Use:** `sort <filename> | uniq -c`.

## 8.7 Translating Characters (`tr`)

- **Concept:** Translating or deleting characters from standard input.
- Examples:
  - `cat file | tr 'a-z' 'A-Z'` : Convert to uppercase.
  - `cat file | tr -d '\r'` : Delete carriage return characters.
