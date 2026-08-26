# 5. Process Management

## 5.1 Viewing Processes

- **Concept:** Inspecting running programs and services.
- **Snapshot (`ps`):**
  - `ps` : Shows processes running in the current terminal.
  - `ps aux` or `ps -ef` : Show all processes running on the system (different syntax/output formats).
- **Interactive Monitoring (`top`, `htop`):**
  - `top` : Classic interactive process viewer (shows PID, user, CPU%, MEM%, command). Updates in real-time. Quit with `q`.
  - `htop` : Enhanced, more user-friendly interactive viewer (color, scrolling, easier sorting/killing). Often needs installation (`sudo apt install htop`). Quit with `q` or `F10`.

## 5.2 Terminating Processes (`kill`, `pkill`)

- **Concept:** Stopping running processes.
- **Process ID (PID):** Unique number identifying each process (found via `ps`, `top`, `htop`).
- **Signals:** Used to communicate with processes.
  - `SIGTERM` (15): Default signal sent by `kill`. Graceful shutdown request (allows cleanup).
  - `SIGKILL` (9): Forceful termination. Process is killed immediately by the kernel (use as last resort).
  - `SIGHUP` (1): Hangup signal (often used to reload configuration).
- **Kill by PID (`kill`):**
  ```bash
  kill <PID>              # Sends SIGTERM
  kill -9 <PID>           # Sends SIGKILL
  kill -SIGKILL <PID>     # Sends SIGKILL
  ```
- **Kill by Name (`pkill`):** `pkill <process_name>` (e.g., `pkill firefox`). Sends SIGTERM by default. Use `-9` for SIGKILL.
