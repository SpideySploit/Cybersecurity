Linux Fundamentals & Security Auditing Cheatsheet

A concise reference for system auditing, permission inspection, process enumeration, and socket analysis based on Hack The Box Academy.

---

1. Process & Service Auditing

- ps aux — Snapshot of all running processes across all users with full paths and resource metrics.
- ps aux | grep -v "^root" — Filters out root noise to isolate third-party software, custom web daemons, and application services.
- systemctl status <service> — Queries the status of a specific systemd daemon.
- systemctl enable --now <service> — Configures a service to start at system boot and immediately triggers execution.
- journalctl -u <service> -n 50 --no-pager — Views the last 50 log lines for a specific service without interactive pagination.

---

2. Network & Socket Enumeration

- ss -tulpn — Lists all listening TCP and UDP sockets with port numbers and bound process IDs (PID).
- netstat -ln4 | grep LISTEN | grep -v 127 — Enumerates all IPv4 listening services exposed to external networks (excluding 127.0.0.1 and 127.0.0.53).
- ip -c a && ip route — Shows network interface bindings, CIDR subnets, and the default gateway routing table.
- curl -I -s http://<target> — Performs an HTTP HEAD request to grab web server headers and banner versions.

---

3. Permissions & Privilege Discovery

- chmod 755 <file> — Sets read/write/execute for owner, and read/execute for group/others (rwxr-xr-x).
- find / -perm -4000 -type f 2>/dev/null — Audits the entire filesystem for binaries with the SUID bit set (runs with file owner permissions).
- find / -writable -type d 2>/dev/null — Discovers world-writable directories (e.g., /dev/shm, /tmp) suitable for staging scripts.
- getfacl <path> — Displays fine-grained Access Control Lists (ACLs) when traditional Linux file permissions look restrictive.
- cat /etc/passwd | grep -v "nologin\|false" — Filters system daemons to show human users with valid login shells.

---

4. Shell Redirection & Stream Parsing

- 2>/dev/null — Silences stderr (file descriptor 2) by routing errors directly to the bit bucket.
- cmd > file 2>&1 — Combines stdout and stderr into a single stream, writing all output to disk.
- cmd | wc -l — Passes output into word count to calculate the exact number of matching lines.
- grep -Po '<regex>' — Extracts Perl-compatible regex matches exclusively (-o flag).
- python3 -c 'import pty; pty.spawn("/bin/bash")' — Upgrades a raw reverse shell into a fully interactive pseudo-terminal (PTY).