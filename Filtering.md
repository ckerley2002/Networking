# Devices and Mechinisms
## Applications
  - Ensure only approved websites can be accessed and content is allowed in and out. 
## OSI Model
  - filters opperate at differnt levels eaching having their own implementation
## Concepts
  - Whitelist
    - Allowed traffic 
  - Blacklist 
    - Denied traffic 
  - Default Polcies and Implicit Rules/Explocit rules
  - Network Device Operation Modes
    - Routed Layer 3 
    - Transparent Layer 2 
## Windows or Linux
### Net Filter Framework
- Provides:
  - packet filtering
  - stateless firewalls 
  - network address and port translation
  - other packet manipulation
- Hooks:

# ip tables  
```bash
iptables -t [table] -A [chain] [rules] -j [action] ## create new rule

iptables -t [table] -L --line-numbers 

iptables -t [table] -I [chain] [rule num] [rules] -j [action]

iptables -t [table] -R [chain] [rule num] [rules] -j [action]

iptables -t [table] -D [chain] [rule num]

iptables -t [table] -L --line-numbers ## shows all rules in a given table with line numbers 

iptables -t [table] -P [chain] [action] ## changes default policy before flushing 

iptables -t [table] -F ## flushes iptable
```
if you are told to flush your rules you need to set the default to accept so all traffic doesnt get blocked
**policy accept then flush**

## NFTABLE
- pretty muhc combines all your tables into one callable by families
### Chain Types
- filter - to filter packets - can be used with arp, bridge, ip, ip6 
- hook flow process

```bash
nft add table [family] [table]

nft add chain [family] [table] [chain] { type [type] hook [hook] priority [priority] \; policy [policy] \; }

nft add rule [family] [table] [chain] [matches (matches)] [statement]

nft {list | flush} ruleset 

nft {delete | list | flush} table [family] [table]

nft {delete | list | flush} chain [family] [table] [chain]

nft add rule [family] [table] [chain] [position <position>] [matches (matches)] [statement]
```

## Nat 
```nash

```

## Intrustion Detection Systems and Intrustion Prevention Systems
### Common Systems 
Insert pic here  
### Snort rule header 
[action] [protocol] [s.ip] [s.port] [direction] [d.ip] [d.port] ( match conditions ;)
