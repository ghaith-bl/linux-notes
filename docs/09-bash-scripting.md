# 9. Bash Scripting

## 9.1 Introduction & Basics

- **Concept:** Writing scripts (sequences of commands) to automate tasks in the Bash shell.
- **Shebang:** First line of a script: `#!/bin/bash` (specifies the interpreter).
- **Creating:** Write commands in a text file (e.g., `myscript.sh`).
- **Permissions:** Make the script executable: `chmod u+x myscript.sh`.
- **Running:** Execute the script: `./myscript.sh` (using relative path).
- **Comments:** Lines starting with `#` are ignored (except the shebang).

## 9.2 Variables

- **Definition:** `VARNAME="value"` (No spaces around `=`). Convention: Uppercase for environment/global, lowercase for local.
- **Usage:** `$VARNAME` or `${VARNAME}` (braces useful for clarity, e.g., `${VARNAME}_suffix`).
- **Command Substitution:** Store output of a command: `VAR=$(command)` or `` VAR=`command` `` (backticks are older style).
- **Environment Variables:** System-wide variables (e.g., `$PATH`, `$HOME`, `$USER`). View with `env` or `printenv`.
- **Local Variables:** Defined within a script or function.

## 9.3 User Input (`read`)

- **Read into Variable:** `read VARNAME`.
- **Prompt User:** `read -p "Enter your name: " USER_NAME`.
- **Silent Input (Passwords):** `read -s PASSWORD`.

## 9.4 Command Line Arguments

- **Concept:** Passing data into a script when running it.
- **Accessing Arguments:**
  - `$1`, `$2`, ... `$N` : Positional parameters (first argument, second, etc.).
  - `$0` : Name of the script itself.
  - `$#` : Number of arguments passed.
  - `$@` : All arguments as separate words (usually preferred).
  - `$*` : All arguments as a single string.

## 9.5 Arithmetic

- **Syntax:** `$((expression))` or `let expression`.
- Example: `SUM=$((VAR1 + VAR2))`, `let COUNT++`.

## 9.6 Conditional Logic

### `if` Statements

Structure:
```bash
if [[ condition ]]; then
  commands
elif [[ condition ]]; then
  commands
else
  commands
fi
```

- `[[ ... ]]` : Preferred modern test construct (handles strings better).
- `[ ... ]` : Older POSIX test construct.
- `test ...` : Equivalent to `[ ... ]`.
- **Numeric Comparisons:** `eq`, `ne`, `gt`, `ge`, `lt`, `le`.
- **String Comparisons:** `=`, `==`, `!=`, `<`, `>` (inside `[[ ]]`). Use `\<`, `\>` inside `[ ]`.
- **String Tests:** `-z` (empty), `-n` (not empty).
- **File Tests:** `-e` (exists), `-f` (file), `-d` (dir), `-r` (readable), `-w` (writable), `-x` (executable).
- **Logical Operators:** `&&` (AND), `||` (OR), `!` (NOT) (inside `[[ ]]`). Use `-a`, `-o`, `!` inside `[ ]`.

### `case` Statements

Structure:
```bash
case $VARIABLE in
  pattern1) commands ;;
  pattern2|pattern3) commands ;;
  *) default_commands ;;
esac
```

Use Case: Cleaner alternative to nested `if` for matching specific values/patterns.

## 9.7 Loops

### `for` Loops

- List Iteration: `for item in val1 val2 val3; do ... done`.
- Range Iteration: `for i in {1..5}; do ... done`.
- Command Output: `for file in $(ls *.txt); do ... done`.
- C-style: `for (( i=0; i<10; i++ )); do ... done`.

### `while` Loops

`while [[ condition ]]; do commands; done` (Loop while condition is true).

### `until` Loops

`until [[ condition ]]; do commands; done` (Loop until condition is true).

### Loop Control

`break` (exit loop), `continue` (skip to next iteration).

## 9.8 Functions

- **Definition:** `function_name() { commands; }` or `function function_name { commands; }`.
- **Calling:** `function_name arg1 arg2`.
- **Arguments:** Accessed inside function as `$1`, `$2`, `$@`, etc. (local to the function).
- **Return Values:**
  - Exit Status (0-255): `return <number>` (0=success). Check with `$?` after calling.
  - Output (Strings): Use `echo` inside function, capture with `result=$(function_name)`.
- **Local Variables:** `local VARNAME="value"` (scope limited to the function).
