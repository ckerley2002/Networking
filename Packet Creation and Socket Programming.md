# Socket types
- Stream Sockets - Connection orientented and sequenced; mathods for connection establishment and tear-down.
- Datagram Sockets - Connectionless - designed for quickly send and recive data
- Raw Socket - used in user applications

# User Space vs. Kernel Space
- User
  - Stream Sockets
  - Datagram Sockets
- Kernel
  - Raw Sockets

# User Space
- Using tcpdump or wireshark to read file
- using nmap with no switches
- using netcat to connect to a listener
- using netcat to create a listener (above well know ports 1024+
- Using /dev/tcp or /dev/udp to transmist data

# Kernel Space 
- Using tcpdump or wireshark to capture packets on wire

# Python Socket
- Python3 Socket Libary and socket.socket function
```powershell
import socket
  s = socket.socket(socket.<var>
```
 - Family 
  - AF_INET(Default) - IPv4
  - AF_INET6 - IPv6
  - AF_UNIX - Raw
- Type
  - SOCK_STREAM(Default)
  - SOCK_DGRAM
  - SOCK_RAW
- Socket Libary
- Struct Libary
- Sys Libary

```python3
import socket


#This can also be acomplished by using s = socket.socket() due to AF_INET and SOCK_STREAM being defaults
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

ipaddr = '127.0.0.1'
port = 54321

s.connect((ipaddr, port))

#To send a string as a bytes-like object, add the prefix b to the string. \n is used to go to the next line.
s.send(b'Hello\n')

#It is recommended that the buffer size used with recvfrom is a power of 2 and not a very large number
response, conn = s.recvfrom(1024)

#In order to receive a message that is sent as a bytes-like-object you must decode into utf-8

print(response.decode())
#Dont forget to close

s.close()

```
```python3
import socket 

s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

ipaddr = '127.0.0.1'
port = 54321

#To Send a string as a bytes like object add the prefix b. We are using sendto for connectionless sending
s.sendto(b'hello\n', (ipaddr,port)),

# It is recommended that the buffer size used with recvfrom is a power of 2 

response, conn = s.recvfrom(1024)

#In Order to receive a message that is sent as a bytes-like-object you must decode

print(response.decode())

```

# Raw IPv4 Sockets
- Must include IP Header and nex headers
- Requires guidence 
- Use Cases
  - Testing defence mechanisms
  - Avoding defecences
  - Obfuscating Data during transfer
  - Manually craftinng a packet with the chosen data om header fields 

```python3
#For building the socket 
import socket
#For system Level Commands
import sys
#For establishing the packet structure, this will allow direct access to the methods.
from struct import *

#Create a Raw socket 

try:
    s = socket.socket(socket.AF_INET, socket.SOCK_RAW, socket.IPPROTO_RAW)
except socket.error as msg:
    print(msg)
    sys.exit()


packet = ''

src_ip = '10.1.0.2'
dst_ip = '10.3.0.2'

#Lets add the IPv4 Headers!!!

ip_Ver_IHL = 69 #This is putting the decimal conversion of 0x45 for version aand Internet Header Length
ip_tos = 0 #This combines DSCP and ECN Fields
ip_len = 0 # The Kernel will fill in the actual length of the packet
ip_id = 12345 #This sets the IP Identification for the packet
ip_frag = 0 # No fragmentation so it is set to off
ip_ttl = 64 #This determines the TTL of the packet when leaving the machine
ip_proto = 16 #CHA0S if 6 TCP or 17 UDP
ip_check = 0 #The Kernel will fill inthe checksum for the packet 
ip_srcadd = socket.inet_aton(src_ip) # inet_atom(sting) will convert and ip addresses to a 32 bit binary number
ip_dstadd = socket.inet_aton(dst_ip)

ip_header = pack('!BBHHHBBH4s4s' , ip_Ver_IHL, ip_tos, ip_len, ip_id, ip_frag, ip_ttl, ip_proto, ip_check, ip_srcadd, ip_dstadd)
#B = 1 Byte H = 2 Bytes 4s = 4 Bytes

message = b'This is a Message'
packet = ip_header + message

#Send the Packet
s.sendto(packet, (dst_ip, 0))

```

```python3
#For building the socket 
import socket
#For system Level Commands
import sys
#For establishing the packet structure, this will allow direct access to the methods.
from struct import *
import array
#Create a Raw socket 

try:
    s = socket.socket(socket.AF_INET, socket.SOCK_RAW, socket.IPPROTO_RAW)
except socket.error as msg:
    print(msg)
    sys.exit()


packet = ''

src_ip = '10.1.0.2'
dst_ip = '10.3.0.2'

#Lets add the IPv4 Headers!!!

ip_Ver_IHL = 69 #This is putting the decimal conversion of 0x45 for version aand Internet Header Length
ip_tos = 0 #This combines DSCP and ECN Fields
ip_len = 0 # The Kernel will fill in the actual length of the packet
ip_id = 12345 #This sets the IP Identification for the packet
ip_frag = 0 # No fragmentation so it is set to off
ip_ttl = 64 #This determines the TTL of the packet when leaving the machine
ip_proto = 6 #6 TCP
ip_check = 0 #The Kernel will fill inthe checksum for the packet 
ip_srcadd = socket.inet_aton(src_ip) # inet_atom(sting) will convert and ip addresses to a 32 bit binary number
ip_dstadd = socket.inet_aton(dst_ip)

ip_header = pack('!BBHHHBBH4s4s' , ip_Ver_IHL, ip_tos, ip_len, ip_id, ip_frag, ip_ttl, ip_proto, ip_check, ip_srcadd, ip_dstadd)
#B = 1 Byte H = 2 Bytes 4s = 4 Bytes


#TCP header Fields
tcp_src = 54321 # Source Port
tcp_dst = 7777 #Dest Port
tcp_seq = 454 # sequence number
tcp_ack_seq = 0 # TCP act sequence number
tcp_data_off = 5 #Data Offset is the number multiplied by 4 so this would be 20
tcp_reserve = 0 # The 3 reserve bits + ns flag in reserve field
tcp_flags = 0 # TCP Flags field all off (null) or before I turn them on
tcp_win = 65535 # Maximum allowed window size reordered to network order 
tcp_chk = 0 # TCP checksum will be calculated later on
tcp_urg_ptr = 0 # Urgent pointer only if Urg flag is set

# Combine the left shifted 4 bit tcp offset and the reserve field
tcp_off_res = (tcp_data_off << 4) + tcp_reserve

# Lets Play with TCP FLAGS from right to left 

tcp_fin = 0 # Finished 
tcp_syn = 1 # syschronization
tcp_rst = 0
tcp_psh = 0
tcp_ack = 0
tcp_urg = 0
tcp_ece = 0 # exciplit congestion notofication echo
tcp_cwr = 0 # Congestion Window Reduced

# Combine the TCP FLAGS into a byte by byte shifting the together
tcp_flags = tcp_fin + (tcp_syn << 1) + (tcp_rst << 2) + (tcp_psh << 3) + (tcp_ack << 4) + (tcp_urg << 5) + (tcp_ece << 6) + (tcp_cwr << 7)
# THE ! in the pack format string means network order

tcp_hdr = pack('!HHLLBBHHH', tcp_src, tcp_dst, tcp_seq, tcp_ack_seq, tcp_off_res, tcp_flags, tcp_win, tcp_chk, tcp_urg_ptr)


user_data = b'This is a Message, is the HIDDEN??'

# PSUDO Header Fields
src_address = socket.inet_aton(src_ip)
dst_address = socket.inet_aton(dst_ip)
reserved = 0
protocol = socket.IPPROTO_TCP
tcp_length = len(tcp_hdr) + len(user_data)

#Pack the PSUDO header and combine with user data
ps_hdr = pack('!4s4sBBH', src_address, dst_address, reserved, protocol, tcp_length)
ps_hdr = ps_hdr + tcp_hdr + user_data

def checksum(data):
    if len(data) %2 != 0:
        data += b'\0'
    res = sum(array.array("H", data))
    res = (res >> 16) + (res & 0xffff)
    res += res >> 16
    return (~res) & 0xffff
tcp_chk = checksum(ps_hdr)
# Pack the tcp header to fill in the correct checksum - Remember cheksum is NOT in network byte order
tcp_hdr = pack('!HHLLBBH', tcp_src, tcp_dst, tcp_seq, tcp_ack_seq, tcp_off_res , tcp_flags, tcp_win) + pack('H', tcp_chk) + pack('!H', tcp_urg_ptr)

packet = ip_header + tcp_hdr + user_data

#Send the Packet
s.sendto(packet, (dst_ip, 0))

```
