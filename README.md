# Palo Alto Site-to-Site VPN Project - harsh-networksecurity

## 🧩 Topology

Client PC → Palo Alto Firewall 1 → ISP Router → Palo Alto Firewall 2 → Linux Router (Server)

Inshort over-view of what we are going to configure >>>

## 🌐 IP Addressing

| Device/Interface         | IP Address        |
|--------------------------|-------------------|
| Client PC e0             | 192.168.1.1/24    |
| Palo Alto 1 eth1/2       | 192.168.1.100/24  |
| Palo Alto 1 eth1/1       | 1.1.1.1/24        |
| ISP Router g0/0          | 1.1.1.2/24        |
| ISP Router g0/1          | 2.2.2.1/24        |
| Palo Alto 2 eth1/1       | 2.2.2.2/24        |
| Palo Alto 2 eth1/2       | 192.168.2.100/24  |
| Linux Server g0/0        | 192.168.2.1/24    |
| Tunnel.1 - PA1           | 172.16.1.1/24     |
| Tunnel.1 - PA2           | 172.16.1.2/24     |
------------------------------------------------
## 🔐 VPN Configuration

### IKEv2 Crypto Profile
- DH Group: 20
- Encryption: AES-128-GCM
- Authentication: None (GCM includes auth)

### IPsec Crypto Profile
- Encryption: AES-128-GCM
- Authentication: None
- DH Group: 20

### IKE Gateway
- Local IP: 1.1.1.1 / 2.2.2.2
- Peer IP: 2.2.2.2 / 1.1.1.1
- Pre-shared Key: `12345678`
- Version: IKEv2

### Tunnel Interface
- Tunnel.1 on both firewalls
- Tunnel IP: 172.16.1.1 and 172.16.1.2

## 🛣️ Static Routes

| Name         | Destination     | Interface | Next Hop       |
|--------------|------------------|------------|----------------|
| default-route| 0.0.0.0/0       | eth1/1    | ISP Router IP  |
| VPN-route    | Peer LAN subnet | tunnel.1  | Tunnel IP      |

## 🔐 Security Policies

- Allow traffic from LAN to VPN tunnel
- Allow web-browsing, SSH, Telnet between sites
- Apply zone-based security

## 🔎 Test Cases

- ✅ Ping from Client PC to Linux Server
- ✅ Access SSH, Telnet, and HTTP from PC
- ✅ VPN tunnel UP status check in GUI

---

## ⚙️ Tools Used
- EVE-NG
- Palo Alto VM Firewall
- Cisco IOS (for ISP router)
- Cisco IOS router as Linux  (with services - telnet , ssh , http , https)

---

## 🔗 Author
Harsh Bakale 
📧 harsh.s.bakale@gmail.com
💼 https://www.linkedin.com/in/harsh-bakale-996746282/ 

