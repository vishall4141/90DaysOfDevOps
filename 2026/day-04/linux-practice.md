task-1  Check running processes

Use: show all running processes, but only the first 8 lines.

How it works:

ps = "process status". It takes a snapshot of processes (one time, not live).
a = processes of all users, u = show user-friendly columns, x = include processes without a terminal.
| (pipe) = send the output of the left command into the right command.
head -n 8 = keep only the first 8 lines (otherwise you get hundreds).

vish@DESKTOP-05GB0:~$ ps aux | head -n 5
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.2  0.1  21896 13280 ?        Ss   08:59   0:01 /sbin/init
root           2  0.0  0.0   3180  2204 hvc0     Sl+  08:59   0:00 /init
root           7  0.0  0.0   3196  2124 hvc0     Sl+  08:59   0:00 plan9 --control-socket 7 --log-level 4 --server-fd 8 --pipe-fd 10 --log-truncate
root          56  0.0  0.2  50460 16276 ?        S<s  08:59   0:00 /usr/lib/systemd/systemd-journald

ps aux lists every process. PID 1 is the first process the kernel starts. Names in [brackets] are kernel threads.

vish@DESKTOP-05GB0:~$ ps aux | grep nginx
root         277  0.0  0.0  11172  1808 ?        Ss   08:59   0:00 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
www-data     279  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     280  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     281  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     282  0.0  0.0  12896  4484 ?        S    08:59   0:00 nginx: worker process
www-data     283  0.0  0.0  12896  4492 ?        S    08:59   0:00 nginx: worker process
www-data     284  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     285  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     290  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     293  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     294  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     295  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     296  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     297  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     299  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     301  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     302  0.0  0.0  12896  4452 ?        S    08:59   0:00 nginx: worker process
vishal       825  0.0  0.0   4100  2092 pts/0    S+   09:03   0:00 grep --color=auto nginx

In the context of checking processes, grep acts as a text filter that strips away everything except the specific process you are looking for

Command 2: top -b -n 1 | head -n 12

Use: see CPU, memory and the busiest processes.

How it works:

top normally is a live screen that refreshes every few seconds.
-b = batch mode (plain text, so it can be saved or piped).
-n 1 = run only 1 time, then exit.
head -n 12 = show only the first 12 lines.

vish@DESKTOP-05GB0:~/script$ top -b -n 1 | head -n 12
top - 09:50:09 up 24 min,  1 user,  load average: 0.00, 0.00, 0.00
Tasks:  48 total,   1 running,  47 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.6 sy,  0.0 ni, 98.8 id,  0.6 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   7645.7 total,   6487.0 free,    597.7 used,    713.2 buff/cache
MiB Swap:   2048.0 total,   2048.0 free,      0.0 used.   7047.9 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
      1 root      20   0   21928  13292   9792 S   0.0   0.2   0:02.01 systemd
      2 root      20   0    3180   2212   2072 S   0.0   0.0   0:00.03 init-sy+
      7 root      20   0    3196   2128   2008 S   0.0   0.0   0:00.01 init
     62 root      19  -1   66852  19604  18404 S   0.0   0.3   0:00.77 systemd+
    112 root      20   0   25548   6868   5152 S   0.0   0.1   0:01.15 systemd+

Reading it: 54 tasks, almost all sleeping. id = idle CPU, about 91% idle, so the system is quiet. load average is how busy the system has been over 1, 5 and 15 minutes.

Real-life use: server feels slow -> run top and see which process eats CPU or memory.

Command 3: pgrep -a sleep and ps -o pid,ppid,stat,etime,cmd -C sleep

First I started a test process: sleep 300 & (sleep 300 waits 300 seconds, & runs it in the background).

Use: find a process by name and inspect it.

How it works:

pgrep sleep = search processes whose name matches "sleep" and print the PID. -a = also show the full command.
ps -o ... = choose your own columns: pid (process ID), ppid (parent PID), stat (state), etime (time since start), cmd (command).
-C sleep = only processes with the command name "sleep".

Output:

105 sleep 300

  PID  PPID STAT     ELAPSED CMD
  105   104 S          00:01 sleep 300
Reading it: PID 105 was started by parent 104 (my shell), and it is sleeping (S).

Stopping it: pkill sleep sends a "please stop" signal (SIGTERM) to every process named sleep. After that, pgrep -a sleep printed nothing, so the process is gone.

3. Log checks

Logs are the history of what programs did. When something breaks, logs tell you why.

Command 8: journalctl -u cron -n 5

Use: read systemd's log for one service.

How it works: journalctl reads the systemd journal. -u cron = only the unit (service) named cron. -n 5 = last 5 entries. Handy extras: -f (follow live), --no-pager (no scrolling screen), --since "1 hour ago".

Output here:

No journal files were found.
-- No entries --

Reading it: no systemd means no journal, so nothing to read.

Command 9: ls /var/log

Use: list the log folder.

How it works: ls = list files. /var/log is where Linux keeps log files by default.

Output:

README  alternatives.log  apt  bootstrap.log  btmp  dpkg.log  faillog
fontconfig.log  journal  lastlog  private  wtmp

Reading it: plain text logs still exist even without the journal. Common ones: auth.log (logins), syslog (general), dpkg.log (package installs).

Command 10: tail -n 5 /var/log/dpkg.log

Use: see the newest lines of a log file.

How it works: tail shows the end of a file. -n 5 = last 5 lines. Add -f to keep watching new lines live (great while testing).

Output:

2026-04-18 18:13:02 status triggers-pending ca-certificates-java:all 20240118
2026-04-18 18:13:02 startup packages triggers-only
2026-04-18 18:13:02 trigproc ca-certificates-java:all 20240118 <none>
2026-04-18 18:13:02 status half-configured ca-certificates-java:all 20240118
2026-04-18 18:13:02 status installed ca-certificates-java:all 20240118

Reading it: a package going from half-configured to installed, with timestamps.

Command 11: grep -ci "error" /var/log/bootstrap.log

Use: count how many log lines contain the word "error".

How it works: grep searches text for a pattern. -i = ignore upper/lower case. -c = print only the count of matching lines. Without -c it prints the matching lines themselves.

Output:

5

Reading it: 5 lines mention "error". In a real investigation, drop -c and read them.

4. Mini troubleshooting flow (what I actually did)

Problem: systemctl status cron fails.

Run the command and read the error: "System has not been booted with systemd".
Check who is PID 1: ps -p 1 -o pid,comm -> process_api, not systemd.
Try the older tool: service --status-all -> works.
Try logs: journalctl -u cron -> no journal. Fall back to /var/log using ls, tail -n, grep.
Practice on a process: sleep 300 &, find it with pgrep -a sleep, inspect with ps -o, stop it with pkill sleep, confirm with pgrep -a sleep (no output).

Root cause: the machine isn't running systemd as init (common in containers and some VMs). Cron itself is not broken.

5. Your turn: run this on your own machine (ssh example)

Paste your real output under each command.

bash
# Processes
ps aux | grep sshd            # all processes, filtered to sshd
pgrep -a sshd                 # PID + command of sshd

# Services
systemctl status ssh          # on some distros the name is sshd
systemctl list-units --type=service --state=running | head

# Logs
journalctl -u ssh -n 50 --no-pager      # last 50 ssh service log lines
sudo tail -n 50 /var/log/auth.log       # Debian/Ubuntu (RHEL: /var/log/secure)

Mini troubleshooting idea: stop it, see the change, start it again.

bash
sudo systemctl stop ssh       # stop the service
systemctl status ssh          # should say inactive (dead)
journalctl -u ssh -n 10 --no-pager   # see the "Stopped" log entry
sudo systemctl start ssh      # start again
systemctl is-active ssh       # prints: active

Careful: if you are connected to a remote machine over ssh, stopping ssh can lock you out. Do this on your own local machine or VM.



