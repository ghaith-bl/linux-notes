# 23. Task Scheduling: cron & at

## 23.1 cron (Recurring Tasks)

```bash
crontab -e      # Edit the current user's crontab
crontab -l      # List the current user's crontab
crontab -r      # Remove the current user's crontab
```

**Format:**
```
minute hour day month weekday   command
*      *    *   *     *         /path/to/script.sh
```

Example — run a backup script every day at 2:30 AM:
```
30 2 * * * /home/user/backup.sh
```

**System-wide locations:**
- `/etc/crontab`
- `/etc/cron.d/`
- `/etc/cron.daily/`, `/etc/cron.hourly/`, `/etc/cron.weekly/`, `/etc/cron.monthly/`

## 23.2 at (One-Time Future Tasks)

```bash
at 10:00 tomorrow
# then type the command(s), finish with Ctrl+D

atq                 # List queued 'at' jobs
atrm <job_number>   # Remove a queued job
```

## 23.3 systemd Timers (Modern Alternative)

- A `.timer` unit paired with a `.service` unit — more flexible logging/dependency handling than cron.
```bash
systemctl list-timers   # List all active timers
```
