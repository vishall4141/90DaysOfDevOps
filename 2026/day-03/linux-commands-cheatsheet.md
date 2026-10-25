 1. Process Management

| Command | Usage |
|---|---|
| `ps aux` | List all running processes. |
| `top` | Monitor processes, CPU, and memory usage in real time. |
| `htop` | Interactively monitor processes and system resources. |
| `pgrep nginx` | Find process IDs by process name. |
| `kill <PID>` | Request a process to terminate gracefully. |
| `kill -9 <PID>` | Forcefully terminate a process as a last resort. |
| `jobs` | List jobs running in the current shell. |
| `free -h` | Display RAM and swap usage in human-readable format. |
| `uptime` | Show system uptime and load averages. |
| `systemctl status nginx` | Check the status of the Nginx service. |
| `systemctl restart nginx` | Restart the Nginx service. |
| `journalctl -u nginx` | View logs for the Nginx service. |

2. File System

| Command | Usage |
|---|---|
| `pwd` | Display the current working directory. |
| `ls -lah` | List files, including hidden files, with readable sizes. |
| `cd /path/to/dir` | Change the current directory. |
| `mkdir -p app/logs` | Create a directory and any missing parent directories. |
| `touch file.txt` | Create an empty file or update its timestamp. |
| `cp source.txt backup.txt` | Copy a file. |
| `mv old.txt new.txt` | Move or rename a file. |
| `rm -i file.txt` | Remove a file after confirmation. |
| `cat file.txt` | Display the contents of a file. |
| `less file.txt` | Read a file page by page. |
| `head -n 10 file.txt` | Display the first 10 lines of a file. |
| `tail -f app.log` | Follow new log entries in real time. |
| `grep -in "error" app.log` | Search for matching text, ignoring case and showing line numbers. |
| `find /var/log -name "*.log"` | Find log files by filename. |
| `df -h` | Check available disk space on mounted filesystems. |
| `du -sh /var/log` | Show the total size of a directory. |
| `chmod 640 file.txt` | Change file permissions. |
| `chown user:group file.txt` | Change file ownership and group. |

3. Networking Troubleshooting

| Command | Usage |
|---|---|
| `ip addr` | Display network interfaces and their IP addresses. |
| `ip route` | Display the routing table and default gateway. |
| `ping -c 4 google.com` | Test network reachability with four ICMP requests. |
| `dig google.com` | Query DNS records and troubleshoot name resolution. |
| `curl -I https://google.com` | Check HTTP response headers from a website. |
| `ss -tulpn` | Display listening TCP/UDP ports and processes where permitted. |
| `traceroute google.com` | Trace the network path to a destination. |
| `getent hosts google.com` | Check hostname resolution using system-configured lookup sources. |
    "nslookup"===nslookup (Name Server Lookup), a command-line tool used to query the Domain Name System (DNS) to obtain domain name or IP address mappings. 

4. Quick Troubleshooting Workflows

High CPU Usage
1. Run `top` to identify processes consuming CPU.
2. Run `ps aux` to inspect running processes.
3. Investigate the process before stopping it.

High Memory Usage
1. Run `free -h` to check available memory.
2. Run `top` to identify processes using the most memory.

Disk Space Issues
1. Run `df -h` to identify full filesystems.
2. Run `du -sh /var/log` to check directory size.
3. Investigate large files before deleting anything.

Service Failure
1. Run `systemctl status nginx` to check service status.
2. Run `journalctl -u nginx` to inspect service logs.
3. Restart the service only after understanding the issue.

 Website or Network Failure
1. Run `ip addr` to verify network interfaces and IP addresses.
2. Run `ip route` to inspect routing.
3. Run `dig google.com` to test DNS resolution. look-up tool for the internet we can check if our website is moved from old ip to new or not
4. Run `curl -I https://google.com` to inspect the HTTP response.

5. Important Safety Notes

- Use `kill -9` only when graceful termination fails.
- Double-check paths before using `rm`, especially with `sudo`.
- Some commands, such as `htop`, `dig`, and `traceroute`, may require installation.
- A failed `ping` does not always mean a server is down; ICMP traffic may be blocked.
- Use `sudo` only when necessary and when you have permission.

6. New commands I find I will put here

   - python3 | Execute the Python 3 interpreter or run Python scripts. | this is used to run code file in linux terminal for python

