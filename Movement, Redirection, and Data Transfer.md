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


