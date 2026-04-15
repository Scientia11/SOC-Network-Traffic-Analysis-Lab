# TCPDump Walkthrough

## 📌 Overview

This lab provides hands-on practice with `tcpdump` commands, progressing from basic packet capture to advanced traffic analysis. Each task builds practical skills in network monitoring, filtering, and threat detection.

---

# 🟢 Level 1: Fundamentals

## Task 1: List Available Interfaces

```bash
tcpdump -D
```

## Task 2: Capture Traffic on Interface

```bash
tcpdump -i eth0
```

## Task 3: Capture 5 Packets

```bash
tcpdump -i eth0 -c 5
```

## Task 4: Disable Hostname Resolution

```bash
tcpdump -i eth0 -n
```

## Task 5: Show MAC Addresses

```bash
tcpdump -i eth0 -e
```

## Task 6: Display Packet Contents (ASCII)

```bash
tcpdump -i lo -A
```

## Task 7: Display Packet Contents (HEX + ASCII)

```bash
tcpdump -i lo -X
```

## Task 8: Verbose Output

```bash
tcpdump -i lo -v
```

---

# 🟡 Level 2: Filtering Basics

## Task 9: Capture ICMP Traffic

```bash
tcpdump -i eth0 icmp
```

## Task 10: Capture TCP Traffic

```bash
tcpdump -i eth0 tcp
```

## Task 11: Capture UDP Traffic

```bash
tcpdump -i eth0 udp
```

## Task 12: Capture Traffic from Specific Host

```bash
tcpdump -i eth0 host 8.8.8.8
```

## Task 13: Capture Traffic to Specific Host

```bash
tcpdump -i eth0 dst host 8.8.8.8
```

## Task 14: Capture Traffic from Source IP

```bash
tcpdump -i eth0 src host 8.8.8.8
```

## Task 15: Capture HTTP Traffic

```bash
tcpdump -i eth0 port 80
```

## Task 16: Capture HTTPS Traffic

```bash
tcpdump -i eth0 port 443
```

---

# 🔵 Level 3: Intermediate Filtering

## Task 17: Capture HTTP OR HTTPS Traffic

```bash
tcpdump -i eth0 port 80 or port 443
```

## Task 18: Exclude Traffic from Your IP

```bash
tcpdump -i eth0 not src <your-ip>
```

## Task 19: Capture TCP but Exclude SSH

```bash
tcpdump -i eth0 tcp and not port 22
```

## Task 20: Capture Between Two Hosts

```bash
tcpdump -i eth0 host 10.0.2.15 and host 8.8.8.8
```

## Task 21: Capture Packets Larger Than 100 Bytes

```bash
tcpdump -i eth0 greater 100
```

## Task 22: Capture Packets Smaller Than 100 Bytes

```bash
tcpdump -i eth0 less 100
```

## Task 23: Capture SYN Packets

```bash
tcpdump -i eth0 'tcp[tcpflags] & tcp-syn != 0'
```

## Task 24: Capture SYN-ACK Packets

```bash
tcpdump -i eth0 'tcp[tcpflags] & (tcp-syn|tcp-ack) != 0'
```

---

# 🔴 Level 4: File Handling & Analysis

## Task 25: Save Capture to File

```bash
tcpdump -i eth0 -w capture.pcap
```

## Task 26: Read from File

```bash
tcpdump -r capture.pcap
```

## Task 27: Read File Without DNS Resolution

```bash
tcpdump -r capture.pcap -n
```

## Task 28: Filter HTTP Traffic from File

```bash
tcpdump -r capture.pcap port 80
```

## Task 29: Quiet Output

```bash
tcpdump -r capture.pcap -q
```

## Task 30: Human-Readable Timestamps

```bash
tcpdump -tttt -r capture.pcap
```

---

# 🧠 Level 5: SOC Analyst Scenarios

## Task 31: Monitor DNS Traffic

```bash
tcpdump -i eth0 port 53
```

## Task 32: Detect Port Scanning (SYN Only)

```bash
tcpdump -i eth0 'tcp[tcpflags] == tcp-syn'
```

## Task 33: Capture HTTP Credentials (Plaintext)

```bash
tcpdump -i eth0 -A port 80
```

## Task 34: Monitor Outbound Traffic

```bash
tcpdump -i eth0 src <your-ip>
```

## Task 35: Detect Suspicious Ports (e.g., 4444)

```bash
tcpdump -i eth0 port 4444
```

