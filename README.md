# AttackDefense

## IPTABLES Cheat Sheet

### Match & Drop INPUT with printable string

```
# filter string "ls -la" on port 1234
iptables -A INPUT -p tcp -m string --algo bm --string "ls -la" --dport 1234 -j DROP
```

### Match & Drop INPUT with unprintable string

```
#filter string "\x01\x02\x03abcd" on port 1234
iptables -A INPUT -p tcp -m string --hex-string "|010203|abcd" --algo bm --dport 1234 -j DROP
```

### Match & Drop INPUT with multiports 
```
iptables -A INPUT -p tcp -m string --algo bm --match multiport --string "BBBBBB" --dports 1234,2345 -j DROP
```

### Match & Drop OUTPUT with printable string
```
iptables -A OUTPUT -p tcp -m string --algo bm --string "Hello ya" --sport 1234 -j DROP
```

### Save all rules
```
iptables-save > savedrules.txt
```

### Restore rules from files
```
iptables-restore < savedrules.txt
```
### Allow SSH connection

```
iptables -I INPUT 1 -p tcp -m tcp --dport 22 -j ACCEPT
```

### List rules with line numbers

```
sudo iptables -L --line-numbers
#or
sudo iptables -L -nv --line-number
```

### Delete a rule with line numbers

```
sudo iptables -D INPUT 3
```
### Show all rules

```
sudo iptables -L
```
### Save all rules

```
sudo /sbin/iptables-save
```

## Tshark & Dumpcap Cheat Sheet

### Dumpcap dump every minute

```
dumpcap -b duration:60 -w dump.pcap
```

### Tshark dump every minute
```
while true; do tshark -i eth0 -f "tcp or udp" -w "tshark-$(date +%F-%T).pcap"; done                                                     
```

### Tcpdump dump every minute
```
tcpdump -i eth0 -G 60 -w 'log_%d-%m_%Y__%H_%M.pcap'
```

## WinSCP Cheat Sheet

### Automatically sync local folder with remote folder

```
# Using for syncing tshark_dump folder
WinSCP > Commands > Static Custom Commands > Keep Local Directory Up To Date
```

## Wireshark Cheat Sheet

### Filter base on port
```
# filter packet on port 1234
tcp.port == 1234
udp.port == 1234
```

### Filter base on string match, search through raw bytes

```
# search for printable string
frame contains "dddd"

# search for unprintable string
frame contains "\x01\x02\x03\x04"

# search for unprintable string with NULL byte
frame contains 01:00:02:03
```

### Filter packets that contains data

```
# packets that contain data only
data.data
```


