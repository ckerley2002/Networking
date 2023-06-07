# Fundamentals
#Numbers to represent data  
#Singles bit is either on or off  
#Nibble is 4 Bits can represent one hex digit  
1. Base 2 Lowest level format
2. Base 10 Basis for numbering systems by humans
3. Base 16 Used by computers and humans to express larger decimal numbers or lng strings of binary to make more manageable
4. Base 64 Like HEX allows of up to 6 buts of binary A-Za-z0-9

# Encapsulation and Decapsulation
1. Layer 4 TCP Segment 
2. Layer 3 IP Packet
3. Layer 2 Ethernet Frame
4. Layer 1 Bit

# OSI Model

## Layer 1 Application
1. Radio Waves used by smart phones 
2. Twisted Pair / Fiber / Coax
3. Serial
4. Phone (Dial up)

## Layer 2 Session and Presintation Layer (Data Link)
1. MAC (Media access control)
2. LLC (Logical Link Control)
3. ARP (Address resolution Protocol) - IP to MAC Address
4. RARP (Reverse ARP) - Mac Address to IP
#Switches communicate at this level
#VLAN
#MAC is layer 12 down to layer 1
#LLC is layer 2 up to level 3
### Ethernet Header
1. 7 Byte Preamble 
2. 1 byte Delimiter
3. 64 to 1518 byte eithernet frame
1. 14 Byte Destination MAC
2. 14 Byte Source MAC 
3. 4 Byte Ethertype - 0800 IPv4 - 0806 ARP - 86DD IPv6 - 8100 VLAN tagging
4. 46 - 1500 byte Payload
5. 4 byte CRC/FCS  
#MACs can be spoofed  

### 802.11Q Header

1. 64 to 1518 byte eithernet frame
2. 4 byte VLAN Tag
3. 14 Byte Destination MAC
4. 14 Byte Source MAC
5. 4 Byte Ethertype - 0800 IPv4 - 0806 ARP - 86DD IPv6 - 8100 VLAN tagging
6. 46 - 1500 byte Payload

### ARP Header
Preceded by the Ethernet Header  
Byte 0 - 3 Hardware Type / Protocol Type  
Byte 4 - 7 Hardware Address Length / Protocol Address Length / Operation  
Byte 8 - 13 Sender Hardware Address  
Byte 14 - 17 Sender Protocol Address   
Byte 18 - 23 Target Hardware Address  
Byte 24 - 27 Target Protcol Address  

#### ARP Attacks
Both are MITM Attacks  


```bash
arp -a #Demos arp cache of a linux host 
ip neighbor
ip neigh
ip n 
#all check arp for your network
```
Brodcast Storm Switches will constantly circle broadcast traffic between eachother if not configured correctly   

### Switch Operation
Fast Forward - Only Destination MAC  
Fragment Free - First 64 bytes  
Store and Forward - Entire Frame and FCS

### Cam Tables
Learn - Examining the source MAC
Forward - Examining the destination MAC
**If Cam Table is full the trans,mission will be sent out on all ports allowing access to the information from attackers**

### VLAN

**VLANs can be inside one another headers will wither have multiple VLAN Tags and/or will have 9100 or 88A8 as the VLAN tag**

### Spanning Tree Protocol (STP)

![image](https://github.com/ckerley2002/Networking/assets/131701398/8e2d0be8-26b2-4518-bb08-4691f7922b34)

**Root Decision Process**
1. Elect root Bridge
2. Identify the Root ports on non-root bridge
3. Identify the Designated port for each segment
4. Set alternate ports to blocking state  

Used for connecting switches together in a mesh type configuration allowing for redundency  
Root Bridge (Switch) this is the switch connected to the router  

### Layer 2 Discovery Protocols

CDP (Cisco Discovery Protocol)  
FDP (Foundry Discovery Protocol)  
LLDP (Link Layer Discovery Protocol)  
-Open Source   
-Will send out data units to eachother declaring information about the switch  

#### Dynamic Trunking Protocol (DTP)

![image](https://github.com/ckerley2002/Networking/assets/131701398/f86c4a9b-f4ac-487f-83ca-2b984e0450c2)  

Trunk ports are for ports that know they are reciving a vlan  
Access Ports will be on a VLAN but host does not know its on a VLAN  
Access and Trunk port cannot talk to eachother  

#### VLAN Trunking Protocol

![image](https://github.com/ckerley2002/Networking/assets/131701398/23e6b6ec-316d-4f44-bdb7-82c88d11ab64)  

Whatever switch has the newest revision number is the VTP Server  

#### Port Security
1. Shutdown
2. Restrict
3. Protect


## Layer 3 Transport Layer (Network)


### IPv4 Header
Byte 0 Nibble 1 - Version - IPv4 is 4  
Byte 0 Nibble 2 - IHL (Internet Header Length) - Number of 32 bit words in Header (4 Bytes)      
Byte 1 DSCP / ECN - Values 5 - 15 - each number multiplied by 4 to get number of bytes  
Byte 2-3 Total Length  
Byte 4-5 Identification (Frag Packets)  
Byte 6-7 bit 1 Flags followed by Fragmentation Offset - Flag detemines if more data is coming or not     
Byte 8 TTL  
Byte 9 Protocol  
Byte 10-11 Header Checksum - if not correct could be signs of tampering   
Byte 12-15 Source IP Address  
Byte 16-19 Destination IP Address  
Byte 20-23 Options if IHL > 5  (If larger than 20 bytes)

### Fragmentation Process
**Only for ipv4**  
1500 Total Bytes  
IHL x 4 is header size not always 20  
1480 byte actually avaible for data  
ofset feild x 8 1480  
offset feild increment by 185 until flag turns off and no more data is left to be shared  

### IPv6 Header
Byte 0 nibble 1 Version  
Byte 0 Nibble 2 and Byte 1 Nibble 1 Traffic Class  
Byte 1 Nibble 2 - Byte 3 Flow Label  
Byte 4-5 Payload Length  
Byte 6 Next Header  
Byte 7 Hop Limit  
Byte 8-23 Source IPv6 Address  
Byte 24-39 Destination IPv6 Address   

### Fingerprinting
![image](https://github.com/ckerley2002/Networking/assets/131701398/12517a17-979d-4b9f-a244-9c98a0ad994c)  

**Differnt OS's have different TTL's can be helpful in determining was OS is being used**  

### ICMP Header
-Used for ping and trace route  
-ICMPv4 and ICMPv6 
-Example TTL Exceded  

Byte 0 Type  
Byte 1 Code  
Byte 2-3 Checksum  
Byte 4-32 ICMP Specific Message (Variable Length)  

### Zero Configuration
**IPv4**
Uses APIPA  
RFC 3927  

### Layer Three Routing Teachnologies

#### Routing

![image](https://github.com/ckerley2002/Networking/assets/131701398/f463670f-fdaf-46ba-acbc-b529abaf2953)  

#### Routing Table 

![image](https://github.com/ckerley2002/Networking/assets/131701398/5f66710f-180a-4928-bd35-324493ad3578)  

#### Routing vs. Routed

![image](https://github.com/ckerley2002/Networking/assets/131701398/6f2b3704-f9e4-480f-a204-6c85bf3bd744)  

#### First Hop Redundancy Protocol

![image](https://github.com/ckerley2002/Networking/assets/131701398/77333415-a2bc-450e-ac5e-d63fdea6d3da)  

#### Administrative Distance 

![image](https://github.com/ckerley2002/Networking/assets/131701398/e709076c-9432-4e2a-99a4-8acc5643c32f)  

![image](https://github.com/ckerley2002/Networking/assets/131701398/5408c134-d09f-45c8-af27-f7263901688d)  

##### Metrics 
1. Hop
2. Bandwidth
3. Delay
4. Load
5. MTU
6. Reliability
7. Cost
8. Policy

#### Dynamic Routing Protocols

![image](https://github.com/ckerley2002/Networking/assets/131701398/3c326cc1-9709-4dc8-a356-7e23143a11f4)  


## Layer 4 Transport 
Transfer of data 

### TCP Header
Byte 0-1 Source Port  
Byte 2-3 Destination Port  
Byte 4-7 Sequence Number  
Byte 8-11 Ack Number    
Byte 12 Nibble 1 Offset   
Byte 12 Nibble 2 Resvered  
Byte 13 TCP Flags  
Byte 14-15 Window  
Byte 16-17 Checksum  
Byte 18-19 Urgent Pointer  
Byte 20-23 TCP Options (variable length, optional)  

### TCP Flags 

CWR   ECE  URG   ACK   PSH   RST   SYN   FIN  
Collection of Exceptionally Unskilled Attackers Pester Read Security Folks  

### UDP Header

Byte 0-1 Source Port  
Byte 2-3 Destination Port  
Byte 4-5 Length of header and data  
Byte 6-7 Checksum      


## Layer 5 Session

### Protocols

- Socks - Indicated Connections through a proxy - TCP 1080  
- NetBIOS  
- PPTP - OBSOLETE - method to create VPN Tunnels - TCP 1723  
- L2TP - Orgins from L2F and PPTP does not provide encryption - relies on other means of encryption - TCP 1701  
- SMB / CIFS - Allowed to establish connections to other devices to share files, printers, etc. - SMB Rides over NetBIOS allowing applications to communicate over LAN using a NetBIOS name - Deprecated due to DNS - TCP 139/445 - UDP 137/138  
- RPC - Resquest and Response Protocol - Sends request for information in exter Server - Recives said Information - Displays data to user - Ex. SOAP,XML,JSON,NFS - Any port can be used  

## Layer 6 Presentation

### Responsibilities
**This layer deals with Translating, Formating, Encryption, and Compression**

## Layer 7 Application

### Protocols

#### FTP
- File Transfer Protocol  
- TCP 20/21  
- Meaasges - FTP Commands, FTP Reply Codes   
- Modes  
  - Active  
    - Client Initiates data transfer  
    - Port 21  
    - Issues  
      - Doesnt work well through SSH  
  - Passive  
    - Reverses Coversation  
    - Client initates both the command and date connections  

#### Telnet  
- TCP 23  
- Meaasges:  
  - Commands  
  - Options  
- Compared to ssh it is secure  
- **Cannot tunnel with telnet**  
- No Encryption Can see whta is happening on both sides  

#### SMTP  
- Simple Mail Transfer Protocol  
- For transfer between mail servers  
- TCP 25  

#### TACACS
- Network Authenitication Protocol  
- TCP 49  
- Created by CISCO  
  - Generally for networking equiptment  

#### HTTP(S)
- TCP 80 TCP 443  
- GET / HEAD / POST / PUT  
- HTTP Status Codes  
  - 100,200,300,400  

#### POP / IMAP  
- TCP 110  
- Mail Protocols for Clients to connect to the mail servers to retreive mail  
- POP TCP 110  
- IMAP TCP 143  

#### RDP  
- TCP 3389  
- Compression or Encryption support  
- Desktop Size and color depth  
- Remote System Control  
- Keyboard Mapping   

#### DNS (Query and Response)  
- Servers communication between oneanother to get name service identification  
- TCP and UDP 53   

#### DHCP   
- UDP 67/68  
- Gets IPs  
- Client from 68  
- Server from 67    

#### TFTP
- UDP 69
- Total File Transfer Protocol  
- No Threeway Hand Shake  
- Used For Pixie Booting  
- Good for routing configs for routers obv   

#### NTP  
- UDP 123  
- Network Time Protocol  
- Used for Syncrization across systems so they actually work  

#### SNMP  
- Simple network management protocol  
- UDP 161/162  

#### Radius  
- UDP 1645/1646 and 1812/1813  

#### RTP  
- Real Time   
- UDP Above 1023  

#### SSH
- TCP 22
- Secure Shell (Remote)
- Asymmetric or PKI for key exchange 
- Symmetric for session 
- User Authentication
- Data Stream Channeling
- A progam on the Client 

##### SSH Architecture
- Known Host Database - Collection of Host Keys the the client and server use for mutual authenication 
- Agent - Stores keys as a convenience for users
- Signer - A program thay signs the host based authenication packets
- Configuration File - Settings that exist on a Client or Servier that dictate funct for SSH or SSHD

##### SSH Conserns
- Using password authenication only
- Key rotation
- Key management

```bash
sudo tcpdump -D
#Shows interfaces avaiable
sudo tcpdump -i eth0
#Only listens on interface eth0 
sudo tcpdump -i eth0 -X
#Displays data in only ASCII and HEX
sudo tcpdump -i eth0 -X
#Same but includes ethernet portion of Frame
sudo tcpdump -i eth0 -w test.pcap
#writes tcpdump to test.pcap
sudo tcpdump -r test.pcap
#reads from pcap file
sudo tcpdump -i eth0 -XXvv
#verbose (mroe information)
sudo tcpdump -i eth0 -XXvvn
#Shows numbers instead of names
sudo tcpdump -i eth0 -XXvvn port 22
#only port 22
sudo tcpdump -i eth0 -XXvvn host 10.10.0.40
#Only Host 10.10.0.40
sudo tcpdump -i eth0 -XXvvn host 10.10.0.40 and portrange 20-100 or host 10.1.0.3 and dst net 10.2.0.0/24
&& = and
|| = or
!= not


```

### Berkeley Packet Filters

```bash



```










