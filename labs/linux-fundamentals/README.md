Lab: Linux Fundamentals (Hack The Box Academy)

Objective
Establish core Linux system administration, user privilege auditing, network service enumeration, and command-line text parsing skills on a live target.

- Target Host: 10.129.182.231 (ACADEMY-NIXFUND)
- Environment: Kali Linux / HTB Pwnbox via OpenVPN

---

Lab Challenges & Solutions

1. External Socket Discovery
- Task: Identify the number of services listening on all external interfaces (IPv4 only, excluding localhost).
- Command:
  netstat -ln4 | grep LISTEN | grep -v 127 | wc -l
- Methodology:
  1. netstat -ln4 retrieves listening IPv4 sockets.
  2. grep -v 127 filters out local-only loopback adapters (127.0.0.1 and 127.0.0.53).
  3. wc -l counts the remaining listening lines.
- Result: 7 active services.

---

2. Service User Enumeration
- Task: Determine the specific system user running the ProFTPd service daemon.
- Command:
  ps aux | grep proftpd
- Analysis:
  Process list inspection revealed /usr/sbin/proftpd running under its dedicated service account.
- Result: proftpd

---

3. Web Path Extraction & Regex Filtering
- Task: Retrieve the web source code for https://www.inlanefreight.com and filter all unique directory paths.
- Command:
  curl -s https://www.inlanefreight.com | grep -Po 'https://www.inlanefreight.com[^"'\'' ]*' | sort -u | wc -l
- Methodology:
  1. curl -s fetches raw website HTML silently.
  2. grep -Po extracts exact URL matches based on regular expressions.
  3. sort -u alphabetizes the list and filters out duplicate endpoints.
  4. wc -l outputs the count of unique web directories.
- Result: 34 unique paths.

---

Key Takeaways
- Invert-matching (grep -v) is critical during host enumeration to filter noise.
- System daemons should consistently execute under dedicated service accounts rather than root to enforce least privilege.
- Combining pipes (|), regex (grep -Po), and sorting utilities accelerates reconnaissance and data extraction workflows.