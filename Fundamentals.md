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




