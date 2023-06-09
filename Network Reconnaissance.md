- Active
- Passive
- Internal
- External


- **Ports to SCAN**
  - 21
  - 22
  - 23
  - 80


![image](https://github.com/ckerley2002/Networking/assets/131701398/e95ac7e5-e309-4673-af13-27925c9433bd)  

# Network Scanning
- Remote to Local
- Local to Remote
- Local to local
- Remote to Remote

- Scanning approaches
  - Aim
    - Wide range traget scan
    - Target Specific Scan
  - Method
    - Single Source scan
    - Distributed Scan
- Braodcast Ping and Ping sweep
```bash
for i in {1..254}; do ping -c 1 -W 1 10.1.1.$i | grep 'from'; done
nmap -sn <network/CIDR>

```
- Arp Scan
```bash
ip neighbor #Gets ARP Cache
ip n | grep -v FAILED
```
- SYN Scan
```bash
nmap -sS <ipaddr>
```
- Full Connect Scan
  - Gets version information
  - Gets full threeway handshake
```bash
sudo nmap -sT 172.16.1.15 -p 21,22,23,80 -vvvv
sudo nmap -sT -sV 172.16.1.15 -p 21,22,23,80 -vvvv #Gives Versions
```
- Null Scan
```bash
sudo nmap -sN 172.16.1.15 -p 21,22,23,80 -vvvv

```
- FIN Scan
```bash
sudo nmap -sF 172.16.1.15 -p 21,22,23,80 -vvvv

```
- XMAS Tree Scan
```bash
sudo nmap -sX172.16.1.15 -p 21,22,23,80 -vvvv

```
- UDP Scan
  - Takes longer
  - doesnt ahve define dthreeway handshake making scanning take longer

```bash
sudo nmap -sU 172.16.1.15 -vvvv

```
- Idle Scan
```bash
sudo nmap -sI 172.16.1.15
```
- Window Scan
```bash
sudo nmap -sW 172.16.1.15 -vvvv

```
- Helpful addons
```bash
nmap -Pn #treats every address and online
namp -O #guesses OS and version
nmap -T4 #quicker but less stealthy
nmap --min-rate <#> #send packetts no slower than dont really use
nmap -A #OS detection version detection script scanning and traceroute
nmap -p- #scans all ports
```
-Netcat
  - 
