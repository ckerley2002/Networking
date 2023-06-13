# Common Methods
- TFTP
- FTP
  - Active 
  - Passive
- SFTP
- SCP

## TFTP
- RFC 1350 REV 2
- UDP Transport
- Small and Light weight
- No Terminal Communication
- Insecure
- No Directory Services
- Used often for technoligies such as BOOTP and PXE

## FTP
- RFC 959
- TCP Transport
- Uses Multiple connections
- Control(21)/Connection(20)
- Authenitication through clear-text sign-in(user and pass)
- insecure by default
- diretory serviecs 
```bash
#in ftp connection
ftp <IP> 
ls 
get <file name>
#In home shell
wget -r ftp://<ip> #-r added a directory and brought all files into the same directory
```

## SFTP
- TCP port 22
- symetric and asymetric encryption
- Adds FTP to SSH

## SCP 
- TCP Port 22
- Symetric and asymetric encryption
- Authenitication through signin  or with SSH Key
- Non Interactive
```bash
#remote to local
scp <username>@<ip>:<file> <dir to save to>
#local to remote
scp <file to save> <username>@<ip>:<directory to save to>
#remote to seperate remote host
scp -P <port> <file to save> <username>@<ip>:<directory to save to>
```
### SCP Syntax W/ Alternate SSHD
```bash
scp -P <port> <user>@<ip>:<file> <directory to save to>
```

### SCP Through a tunnel
```bash
ssh <user>@<ip> -L <port>:<host>:22 -NT
scp -P <user>@<your ip>:<file> <dir to save to>>
scp -P <port> <user>@<localhost>:<dir to save to>
```

# NETCAT
- Can be used for:
  - Inbound and outbound connections TCP/UDP to or from ports
  - trouble shooting network connections
  - sending/reciving data(insecurely)
  - port scanning (similar to sT in NMAP)
## Netcat: client to listener
```bash
#Client
nc <IP> <Port> < file.txt
#Listener
nc -l -p <port> > newfile.txt
#viewing an image
eom
eog
```
# For CHALLANGEs
```bash
file pipe
fifo
mknod pipe p
nc -lp 1111 > mpipe | nc -lp 2222 < mypipe


```
# SSH
- v1 and v2
- Provides authetication, encryption and integrity
- allows remote terminal sessions
- used for tunneling
- Created as a secure replacement for Berkeley Remote Commands

## SSH Port Forwarding
- Creates Channels using SSH-CONN Protocol
- Allows for tunneling of other services through SSH
- Provides insecure services encryption

```bash

vim /.ssh/config
```

### SSH Local Forawrding
```bash
ssh -p <optimal alt port> <user>@<pivot ip> -L <port to open>:<tgt host>:<port> -NT
#or
ssh -L <local bindport>:<target ip>:<tgt port> -p <alt port> user@<pivot port> -NT
```
**always remember to put -NT at the end of SSH Port Forwarding Command**
```bash
firefox localhost 21902
wget -r localhost 21902'
telnet localhost 8675
  ehlo

```

### SSH Reverse Forwarding
```bash
ssh user@targetip -R <RHP>:localhost:<port to access> -NT
```

### SSH Dynamic Port Forwarding
tcp only
```bash
ssh [-p <alt port>] <user>@<ip> -D <port>
ssh -p 9315 john@localhost -D 9050

proxychains nmap -Pn <options> Billhost
proxychains wget -r billhost 8080
proxychains telnet billhost 25
  ehlo

proxychains nmap -Pn <options> Laurahost
#or
proxychains ./scan.sh
#or
proxychains ./stream.py

proxychains wget -r ftp://Laurahost

proxychains nmap -Pn <options> AmosHost 
proxychains telnet #**do not do**

```
