| Problem | Answer |
|---|---|
| 6 | access-list 6 permit 192.168.3.192 0.0.0.15 |
| 7 | access-list 7 permit 192.168.3.64 0.0.0.31 |
| 8 | access-list 8 permit 172.20.1.192 0.0.0.63 |
| 9 | access-list 9 permit 172.20.200.0 0.0.3.255 |
| 10 | access-list 10 permit 172.20.203.0 0.0.0.127 |
| 11 | access-list 11 permit 192.168.9.99 0.0.0.3 |
| 12 | access-list 12 permit 192.168.99.0 0.0.0.15 |
| 13 | access-list 13 permit 172.28.28.0 0.0.1.255 |
| 14 | access-list 14 permit 172.28.28.0 0.0.3.255 |
| 15 | access-list 15 permit 172.28.28.0 0.0.0.255 |

# Answers: Reverse Engineering from ACL to Address Range

Table D-4 lists the answers to the problems listed in Table D-2.

Table D-4 — Address Ranges for Problems in Table D-2: Answers

| Problem | Address Range |
|---|---|
| 1 | One address; 192.168.4.5 |
| 2 | 192.168.4.128 – 192.168.4.131 |
| 3 | 192.168.4.128 – 192.168.4.255 |
| 4 | 172.25.96.0 – 172.25.96.255 |
| 5 | 192.168.4.128 – 192.168.4.159 |
| 6 | 192.168.4.128 – 192.168.4.135 |
| 7 | 172.25.96.0 – 172.25.103.255 |
| 8 | 172.25.96.0 – 172.25.96.63 |
| 9 | 10.10.16.0 – 10.10.23.255 |
| 10 | 10.10.16.0 – 10.10.16.127 |
| 11 | 192.168.17.112 – 192.168.17.119 |
| 12 | 192.168.17.112 – 192.168.17.127 |
| 13 | 172.19.200.0 – 172.19.200.63 |
| 14 | 172.19.200.0 – 172.19.201.255 |
| 15 | 10.1.0.0 – 10.1.255.255 |