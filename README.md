# eJPT-Cheatsheet
Todos los comandos necesarios para aprobar el eJPT
# Barrido de ping - Ping sweep
## Nmap
nmap -sn 10.10.10.0/24
## fping
fping -a -g 10.10.10.0/24 2>/dev/null
# Pivoting
## Ip Route
ip route add 10.10.16.0/24 via 10.10.16.1 dev tap0
## Metasploit
run autoroute -s 10.10.16.0/24
# Password cracking
## John
john --wordlist=/usr/share/wordlists/rockyou.txt unshadowed.txt
## Online Tools
[CrackStation](https://crackstation.net/)
# Dump Hashes
## unshadow 
unshadow passwd shadow > unshadowed.txt
# Fuzzing
## Nmap
nmap --script=http-enum -p80 10.10.14.16 -oN webScan
## wfuzz
wfuzz -c --hc=404 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u https://10.10.14.15/FUZZ
wfuzz -c --hc=404 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u https://10.10.14.15/FUZZ.php
## dirb
dirb http://10.10.15.12
## gobuster
gobuster dir -u 10.10.14.12 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,html
