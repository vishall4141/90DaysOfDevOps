# Linux Under the Hood Notes

1. Core Components of Linux

- Kernel:The heart of Linux. It manages hardware, memory, CPU, processes, and devices.
- User Space: The environment where applications and commands run, such as Bash, Python, and Nginx.
- Init/Systemd: The first process started during boot (PID 1). It initializes the system and manages services.

2. How Processes Are Created and Managed

 process is a running program with its own Process ID (PID).
- `fork()` creates a new process.
- `exec()` replaces a process with a new program.
- The kernel schedules processes and allocates CPU and memory resources.
- Processes can run in the foreground or background.

3. Process States

- Running (R):Currently running or ready to use the CPU.
- Sleeping (S):Waiting for an event or resource.
- Disk Sleep (D): Waiting for certain I/O operations; usually cannot be interrupted.
- Stopped (T): Temporarily paused.
- Zombie (Z): Finished execution, but its parent has not collected its exit status.

  4. What Does systemd Do?

- Starts and manages services during boot and runtime.
- Handles service dependencies and automatic restarts.
- Collects system and service logs using `journald`.
- Helps troubleshoot services and system failures.

Why it matters: systemd keeps services organized and makes Linux troubleshooting easier.

  5. Five Linux Commands Used Daily

1. `ps aux` – View running processes.
2. `top` – Monitor CPU, memory, and processes in real time.
3. `systemctl status nginx` – Check a service's status.
4. `journalctl -xe` – Inspect recent system logs and errors.
5. `kill <PID>` – Send a signal to a process, commonly to stop it.

DevOps takeaway: Understanding the kernel, processes, and systemd helps you diagnose service failures, resource issues, and application problems faster.

DevOps takeaway: systemctl stop controls a service; systemctl daemon-reload reloads systemd's unit definitions. They serve different purposes.