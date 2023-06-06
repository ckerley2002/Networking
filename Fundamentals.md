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




