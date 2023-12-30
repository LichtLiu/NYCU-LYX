---
title: "Computer Security Principles and Practice"
permalink: /Computer-Security-Principles-and-Practice/9-Firewalls-and-Intrusion-Prevention-Systems/
layout: default
---
# 9-Firewalls and Intrusion Prevention Systems

[https://www.youtube.com/watch?v=NEtHcWE3Ki0&t=2s](https://www.youtube.com/watch?v=NEtHcWE3Ki0&t=2s)

# **9.1  The Need for Firewalls**

*   Internet connectivity is essential
    *   Threats: enabling the outside world to reach and interact with local network assets
*   Why not just equip each workstation/server with strong security features?
    *   Not sufficient; Not cost-effective
    *   e.g., a security flaw is discovered: each potentially affected system must be upgraded
        *   The network may contain various OSes
        *   Needs: scalable configuration management and aggressive patching
*   A single choke point（一定經過） between the protected network and the Internet
    *   Complement to host-based security services （互補 host-based security services）
    *   Imposing security and auditing against Internet-based attacks
    *   A single computer system or a set of two or more systems working together

# **9.2  Firewall Characteristics and Access Policy**

*   Design goals
    *   All traffic from inside to outside, and vice versa, must pass through the firewall
    *   Only authorized traffic, as defined by the local security policy, will be allowed to pass
    *   The firewall itself is immune to penetration
*   Firewall Access Policy
    *   A critical component in the planning and implementation: specifying a **suitable access policy**
        *   網頁服務或IC design的網路，policy需求不同
        *   Listing the types of traffic authorized
        *   Being developed from the organization’s information security risk assessment and policy

### Characteristics for Control Access

*   IP address and protocol values
    *   Used by: packet filter and stateful inspection firewalls
    *   Limiting access to specific services
*   Application protocol
    *   Used by: an app-level gateway
    *   Relaying and monitoring the exchange of information for specific app protocols
        *   e.g., checking SMTP email for spam
*   User identity
    *   Identifying inside users using secure authentication technology, e.g., IPSec
*   Network activity
    *   Considering time or request, e.g., only in business hours
    *   Rate of requests or other activity patterns, e.g., detecting scanning attempts



**What to expect from a firewall:**

*   **Single choke point****:** Firewalls define a single point of entry to the protected network, making it easier to control traffic and prevent unauthorized access.
*   **Security monitoring****:** Firewalls provide a centralized location for monitoring security-related events, allowing administrators to detect and respond to potential threats.
*   **Non-security functions****:** Firewalls can serve as platforms for various network functions, such as network address translation (NAT) and network management.
*   **IPSec support****:** Firewalls can be used to implement virtual private networks (VPNs) using the [IPSec protocol](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4662?block=block-c08219f6-edb1-4be5-9cb7-21d790678e92).

**Firewall limitations:**

*   **Bypassing the firewall****:** Attacks can penetrate the network through means other than the firewall, such as direct connections or wired or mobile broadband connections.
*   **Internal threats****:** Firewalls are not effective against threats originating from within the network, such as disgruntled employees or social engineering attacks.
*   **Wireless LAN vulnerabilities****:** Unsecured wireless LANs can be accessed from outside the organization, bypassing the firewall.
*   **Portable devices****:** Infected laptops, PDAs, or portable storage devices can be brought into the network and spread malware.

###   

# **9.3  Types of Firewalls**

*   General model

![](https://t3764800.p.clickup-attachments.com/t3764800/f78d5cde-a0d1-43c6-875f-ea650aecce9d/Screen%20Shot%202023-12-03%20at%206.54.27%20PM.png)

*   Four major types
    *   [Packet filtering firewall](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4862?block=block-69dc7730-687d-44c3-80fd-40a6f9af1432)
    *   [Stateful inspection firewall](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4862?block=block-4f7167ce-b14e-47e8-880b-d01987fe4d59)
        *   檢查連線狀態，封包跟封包的關西
    *   [Application proxy firewall](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4862?block=block-e607e1d1-73cd-410f-9f5b-72b17dda0266)
    *   [Circuit-level proxy firewall](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4862?block=block-6363c221-fce2-4b57-9367-14029f12b063)

![](https://t3764800.p.clickup-attachments.com/t3764800/1df25bb8-b28b-4006-ba18-8b4aefc1debd/Screen%20Shot%202023-12-03%20at%206.55.19%20PM.png)



## Packet Filtering Firewall

![](https://t3764800.p.clickup-attachments.com/t3764800/2494607d-9eff-4661-9373-1788416d7d25/Screenshot_20231209_134659_Chrome.jpg)

*   Applying a set of rules to each incoming and outgoing IP packet
    *   Rules based on matches in the IP or TCP header for packets in both directions
    *   Matches: determining whether to forward or discard the packet
    *   No match: a default action is taken
        *   Discard: prohibit unless expressly permitted➔More conservative, controlled, visible to users (白名單)
        *   Forward: permit unless expressly prohibited➔Easier to manage and use but less secure (黑名單)



Filtering rules are based on information contained in a network packet:

*   **Source IP address****:** The IP address of the system that originated the IP packet (e.g., 192.178.1.1).
*   **Destination IP address****:** The IP address of the system the IP packet is trying to reach (e.g., 192.168.1.2).
*   **Source and destination transport-level address****:** The transport-level (e.g., TCP or UDP) port number, which defines applications such as SNMP or HTTP.
*   **IP protocol field****:** Defines the transport protocol.
*   **Interface****:** For a firewall with three or more ports, which interface of the fire- wall the packet came from or for which interface of the firewall the packet is destined.

### Packet Filtering Example

*   Goal: allowing inbound and outbound email traffic but to block all other traffic
1. Inbound mail from an external source is allowed(port 25 is for SMTP incoming).
2. This rule is intended to allow a response to an inbound SMTP connection.
3. Outbound mail to an external source is allowed.
4. This rule is intended to allow a response to an outbound SMTP connection.
5. This is an explicit statement of the default policy. All rule sets include this rule implicitly as the last rule.



*   Problem 1: Rule 4 allows external traffic to any destination port above 1023(從外面大於1023的port都能進來，要限制source port 25, dest >1023 )
*   Problem 2: New Rule 4 allows an outside machine to send packets with source port 25 to internal machines attacker could gain access to internal machines by sending packets with a TCP source port number of 25) (加ACK flag)![](https://t3764800.p.clickup-attachments.com/t3764800/e5c1fb85-3525-4221-adb3-3f07f2a13415/Screenshot_20231209_135406_Adobe%20Acrobat.jpg)

> To counter this threat, we can add an ACK flag field to each row. For rule 4, the field would indicate that the ACK flag must be set on the incoming packet.

*   Rules 3 and 4: any inside host can send mail to the outside

![](https://t3764800.p.clickup-attachments.com/t3764800/34ee82ac-4c85-4070-baf1-06f453caec06/image.png)

> 1024以上的port大都是random source port

### Packet Filtering: Pros and Cons

*   Pros
    *   Simplicity
    *   Transparent to users and are very fast
*   Cons
    *   Cannot prevent attacks that employ app specific vulnerabilities or functions(cannot block specific application commands)
    *   Limited logging functionality
    *   Don’t support advanced user authentication, due to the lack of upper-layer functionality
    *   Vulnerable to attacks on TCP/IP protocol issues
    *   Susceptible（易受影響的） to security breaches（違規） caused by improper configurations (rule沒設好)

### Packet Filtering: Possible Attacks

*   IP address spoofing
    *   Attacker transmits packets from the outside with a source IP address of an internal host (假造內部IP)
    *   Countermeasure: discarding incoming packets with an inside source address(外部進來的內部IP封包要丟掉)（通常在防火牆外部的路由器上實施）
*   Source routing attacks（源路由攻擊）
    *   Attacker specifies the route that a packet should take
    *   Countermeasure: discarding all packets that use this option
*   Tiny fragment attacks
    *   Attacker uses the IP fragmentation option to create extremely small fragments and force the
    *   TCP header info into a separate packet fragment
        *   Circumventing filtering rules that depend on TCP header information
    *   Countermeasure: enforcing the first fragment of a packet to contain a predefined minimum amount of the transport header (IP and TCP header)

### Traditional Packet Filtering: Weakness

*   Making decisions on an individual packet basis
    *   Doesn’t take into consideration any higher-layer context
*   Must permit inbound network traffic on all the ports (≧ 1024) for TCP-based traffic
    *   Server port: < 1024 (well-known)
    *   Client port: 1024 ~ 65535 <-- a vulnerability



## Stateful Inspection Firewalls

![](https://t3764800.p.clickup-attachments.com/t3764800/1c0a1891-3dc5-4bf4-b31d-a85442770ad7/Screenshot_20231209_143440_Chrome.jpg)

狀態檢查防火牆 (stateful inspection firewall)，又稱動態封包過濾，是一種防火牆技術，它通過跟踪活躍連接的狀態來確定哪些網路數據包可以通過防火牆。狀態檢查防火牆比僅僅檢查數據包頭部的傳統包過濾防火牆更具防禦性，因為它可以阻止許多常見的攻擊，例如 IP 地址欺騙和源路由攻擊。

狀態檢查防火牆的工作原理如下：

1. 防火牆會跟踪每個連接的狀態，包括連接的源和目的 IP 地址、端口號和協議類型。
2. 當防火牆收到一個數據包時，它會首先檢查該數據包是否符合已建立連接的狀態。
3. 如果數據包符合已建立連接的狀態，則防火牆將允許該數據包通過。
4. 如果數據包不符合已建立連接的狀態，則防火牆將拒絕該數據包。

狀態檢查防火牆可以提供以下優點：

*   可以阻止許多常見的攻擊，例如 IP 地址欺騙和源路由攻擊。
*   可以提供更細粒度的控制，允許管理員根據連接的狀態來定義過濾規則。
*   可以提供更高的性能，因為它只需要檢查數據包的頭部部分。

狀態檢查防火牆也有一些缺點：

*   可能會增加延遲，因為防火牆需要跟踪每個連接的狀態。
*   可能會增加複雜性，因為管理員需要定義複雜的過濾規則。

![](https://t3764800.p.clickup-attachments.com/t3764800/f386ec16-24d4-4da3-918b-6f789ce8e6ad/Screenshot_20231209_143417_Adobe%20Acrobat.jpg)

*   Tightening rules for TCP traffic by creating a directory of outbound TCP connections
    *   An entry for each currently established connection
    *   Allowing incoming traffic to high numbered ports only for those entries
    *   Keeping track of TCP sequence numbers
        *   Preventing session hijacking attacks
*   Some even inspect other protocols(FTP, SIPS, et.)

## Application Proxy Firewall

![](https://t3764800.p.clickup-attachments.com/t3764800/05fcbb80-efaa-404c-a0e0-a6b1b36da03d/Screenshot_20231209_144012_Chrome.jpg)

應用層閘道 (Application-level Gateway, ALG)，也稱為應用層代理 (Application-level proxy)、應用層網關 (Application gateway) 或應用層中繼 (Application proxy)，是網路安全中的一項技術，用於增強防火牆或網路地址轉譯 (NAT) 的功能。它可以分析應用層的網路流量，並根據需要對其進行修改或控制。



*   A relay of app-level traffic: an app proxy
    *   User contacts it using a TCP/IP app (e.g., Telnet or FTP)（用戶使用 TCP/IP 應用程序（例如 Telnet 或 FTP）連接到代理）
    *   It contacts app on remote host and relays TCP segments between two ends（代理連接到遠端主機上的應用程序）
        *   Two spliced connections（代理在兩個端點之間中繼 TCP 分段，就像兩個連接被拼接在一起一樣）
    *   Must have proxy codes for specific apps
    *   May restrict supported app features
*   Pros: more secure than packet filters (可限制每個application的運作)
    *   Doesn’t rely on possible combinations at the TCP and IP level
*   Cons: additional processing overhead on each connection (要將封包拆開)

## Circuit-Level Proxy Firewall

![](https://t3764800.p.clickup-attachments.com/t3764800/519480f4-724f-4f10-92ea-bc0a11f6e9fd/Screenshot_20231209_144020_Chrome.jpg)

電路層閘道是一種防火牆，它在會話層 (OSI 模型的第四層) 運作，監視 TCP 握手以確定請求的會話是否合法。但是，它不會檢查封包內的資料內容，只檢查封包來源。不過這種作法無法保證安全性，因為惡意程式仍可能隱藏在封包中。

電路層閘道具有以下特點：

*   **較少的運算需求:** 電路層閘道僅需檢查封包的標頭，因此需要的運算能力較少，可提供較高的性能。
*   **較簡單的配置:** 電路層閘道僅需配置允許或拒絕的連接，因此配置較為簡單。
*   **較低的延遲:** 電路層閘道僅需檢查封包的標頭，因此延遲較低。

電路層閘道也有一些缺點：

*   **無法阻止應用層攻擊:** 電路層閘道無法檢查封包內的資料內容，因此無法阻止應用層攻擊。
*   **無法提供細粒度的控制:** 電路層閘道僅能允許或拒絕連接，無法提供更細粒度的控制，例如僅允許特定的應用程式或埠號。

電路層閘道通常用於提供基本的防火牆保護，例如防止非法連接。它們也常用於提供較高的性能，例如在需要處理大量網路流量的環境中。



*   Splitting a TCP connection
    *   Two TCP connections （不允許端到端TCP連接）
        *   One between itself and a TCP insider
        *   One between itself and a TCP outsider
    *   Relaying TCP segments from one connection to the other
    *   Doesn’t examine the contents
*   Security: determining which connections are allowed
    *   Typically used when inside users are trusted (可限制connection在什麼時間是允許的或不允許的)
*   To reduce the overhead of the app-level proxy firewall
    *   Inbound: app-level proxy firewall（外部人員：限制外面連進來的連線行為）, outbound: circuit-level proxy (內部人員不限制connection行為，但限制連線時間) (兩個搭配減少overhead)

### SOCKS: Circuit-level Gateway

*   The protocol is conceptually a “shim-layer” between the application layer and the transport layer, and as such does not provide network-layer gateway services, such as forwarding of ICMP messages.(應用層和傳輸層之間的“墊片層”，因此不提供網路層網關服務，例如 ICMP 訊息轉發)
*   A framework for client-server apps in TCP/UDP domains to conveniently and securely use the services of a network firewall
    *   Client app contacts SOCKS server, authenticates, and sends a relay request
    *   SOCKs server evaluates the request
        *   Either establishes a connection or denies it
*   Three components
    *   SOCKS server: often running on a UNIX-based firewall; also on Windows
    *   SOCKS client library: running on internal hosts protected by the firewall
    *   SOCKS-ified versions of programs (e.g., FTP, TELNET)
    *   SOCKS port 1080

# **9.4  Firewall Basing**



**bastion host**

**堡壘主機**是一種專門用於保護網路安全的伺服器。它通常位於網路邊緣，用於隔離內部網路和外部網路。堡壘主機通常運行多種安全功能，例如防火牆、入侵防禦系統和應用程式閘道。



**host-based firewall**

**主機型防火牆**是一種安裝在個人電腦或伺服器上的防火牆軟體或硬體。它用於保護單一主機免受網路攻擊。主機型防火牆通常會根據連接的來源和目的地 IP 地址、端口號和協議類型來過濾網路流量。



**personal firewall**

**個人防火牆**是一種安裝在個人電腦上的防火牆軟體。它用於保護個人電腦免受網路攻擊。個人防火牆通常會根據連接的來源和目的地 IP 地址、端口號和協議類型來過濾網路流量。



堡壘主機提供了最強大的安全性，但也最昂貴和最複雜。

主機型防火牆提供中等的安全性，兼顧了成本和複雜性。

個人防火牆提供最低的安全性，但也最容易使用。



## Bastion Host(堡壘主機)

**堡壘主機**是一種專門用於保護網路安全的伺服器。它通常位於網路邊緣，用於隔離內部網路和外部網路。堡壘主機通常運行多種安全功能，例如防火牆、入侵防禦系統和應用程式閘道。

*   A system identified by the firewall administrator as a critical strong point in the network’s security
    *   Serving as a platform for an app-level or circuit-level gateway

![](https://t3764800.p.clickup-attachments.com/t3764800/42f94f1c-eaf4-423e-8431-612dc42cb990/Screenshot_20231209_151607_Microsoft%20365%20(Office).jpg)

### Bastion Hosts: Common Characteristics

*   Running secure OS (僅剩最小功能支援firewall), only essential services ➔ a hardened system
*   May require user authentication to access proxy or host
*   Each proxy
    *   Can restrict features, hosts accessed
    *   Small, simple, checked for security
    *   Independent(沒有其他功能), non-privileged （被入侵對系統沒傷害）
    *   Limited disk use, hence read-only code

## Host-Based (Server-base) Firewalls

*   Software modules: used to secure an individual host
    *   Available in many OSes: add-on packages
    *   Filtering and restricting the flow of packets
    *   Common location: a server
*   Pros
    *   Filtering rules can be tailored to the host environment
    *   Protection is provided independent of topology
    *   Providing an additional layer of protection
        *   Used in conjunction with stand-alone firewalls

## Personal Firewall

*   Software modules on the personal computers
    *   For both home and corporate uses
    *   Can be housed in a router that connects all of the home computers
    *   Much less complex than server-based and stand-alone firewalls
*   Primary role: to deny unauthorized remote access
    *   Can also monitor outgoing activity ➔ worms and other malware
*   Practice
    *   Linux: the netfilter package
    *   Mac OS X: the pf package
    *   All inbound connections are denied except for those the user explicitly permits
    *   Outbound connections are usually allowed

# **9.5  Firewall Location and Configurations**

## DMZ Networks

![](https://t3764800.p.clickup-attachments.com/t3764800/f6a55bfb-177f-4a76-bf60-3f73baab7cd9/Screenshot_20231209_153959_Microsoft%20365%20(Office).jpg)

*   DMZ (Demilitarized Zone):
    *   A small network isolated from the private network.
*   Systems (e.g., a Web site) located on DMZ networks:
    *   externally accessible but need some protec**tions**

## **Virtual Private Networks(VPN)**

![](https://t3764800.p.clickup-attachments.com/t3764800/d3c383d7-5219-4834-8ea1-5ff7bb4828ba/Screenshot_20231209_154420_Microsoft%20365%20(Office).jpg)

*   Containing a set of computers
    *   Interconnecting by means of a relatively unsecure network
    *   Making use of encryption and special protocols to provide security
*   Using encryption and authentication in the lower protocol layers to provide a secure connection through an insecure network
    *   Most common protocol at the IP level: IPSec (Internet Protocol Security)

## Distributed Firewalls

*   Local protection: against internal attacks
    *   Tailored to specific machines and apps
    *   Host-based firewalls on hundreds of servers and workstation
    *   Personal firewalls on local and remote user systems
*   Global protection: against internal and external attacks
    *   Stand-alone firewalls

![](https://t3764800.p.clickup-attachments.com/t3764800/9f33cf36-f13a-4977-9e6f-204cf1311090/image.png)

*   May use both an internal and external DMZ
*   External DMZ: less protection
    *   e.g., Web servers
        *   Have less critical information
        *   Protected by host-based firewalls
*   Security monitoring is also needed
    *   log aggregation and analysis, firewall statistics, etc.

## Summary of Firewall Locations and Topologies

![](https://t3764800.p.clickup-attachments.com/t3764800/0c3656c5-d312-45ff-ae18-5f769b70102c/image.png)

# **9.6  Intrusion Prevention Systems**

*   An extension of an IDS: block or prevent detected malicious activity
*   Like an IDS
    *   Types: [host-based](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4862?block=block-92e18656-55e3-4be5-aa0d-39a7a56199d3), [network-based](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4862?block=block-35c5ad64-5ec2-4f5d-ad99-b74c3aea18f2), or [distributed/hybrid](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4862?block=block-966d8e27-e973-4310-8de6-774274e6f175)
    *   Approaches: anomaly detection, or signature/heuristic detection

## Host-Based IPS (HIPS)

*   Anomaly detection(不規則)
    *   Behavior patterns that indicate malware
    *   Or, not that of legitimate users
*   Signature/heuristic detection (啟發式偵測)
    *   Specific content of app network traffic, sequences of system calls, etc.
    *   Patterns that have been identified as malicious
*   Examples of the types of malicious behavior addressed by a HIPS
    *   Modification of system resources: Rootkits, Trojan horses, and backdoors
    *   Privilege-escalation exploits
    *   Buffer-overflow exploits
    *   Access to e-mail contact list: many worms spread by mailing a copy of themselves
    *   Directory traversal: hackers traverse directory and access files against Web servers3
*   Capability can be tailored to the specific platform (可以設計用於特定平台)
    *   General-purpose tools for a desktop or server system
    *   Protection for specific types of servers: e.g., Web and database servers
*   Alternative solution: a sandbox approach
    *   Suited to mobile code, e.g., Java applets and scripting languages
    *   Quarantining such code in an isolated system area (將code隔離在被隔離的系統區域)
*   Areas for desktop protection
    *   System calls, file system access, system registry settings, host input/output

### The Role of HIPS

*   The main target for hackers and criminals: enterprise point
    *   Including desktop and laptop systems (當跳板)
    *   More popular than network devices to be attacked
*   Security vendors focus more on the endpoint security products
    *   An integrated, single-product suit of functions
        *   E.g., antivirus, antispyware, antispam, and personal firewalls
*   Pros: various tools work closely together
    *   Threat prevention is more comprehensive
    *   Management is easier

If HIPS is sophisticated enough, can we get rid of network-level devices?

### Security Practice: Defense in Depth (DiD)

*   A series of defensive mechanisms are layered to protect valuable data and information
    *   Multi-layered approach with intentional redundancies
    *   If one mechanism fails, another steps up immediately to thwart an attack
*   Using HIPS as one element in a DiD strategy
    *   Together with network-level devices, e.g., firewalls and network-based IPS



## Network-Based IPS

*   Inline with NIDS: modifying or discarding packets and tearing down TCP connections
    *   Approaches: anomaly detection, or signature/heuristic(啟發式) detection
*   Typical methods used by a NIPS device to identify malicious packets
    *   Pattern matching: e.g., specific byte sequences (the signature)
    *   Stateful matching: attack signatures in the context of a traffic stream
    *   Protocol anomaly: deviation(偏誤) from standards set in RFCs
    *   Traffic anomaly
    *   Statistical anomaly

## Distributed or Hybrid IPS

*   Example system: worms detection

![](https://t3764800.p.clickup-attachments.com/t3764800/9394f8bb-e574-457a-8daa-f2d035f1b21f/Screen%20Shot%202023-12-10%20at%207.54.18%20PM.png)

### Example: Unified Threat Management Appliance

![](https://t3764800.p.clickup-attachments.com/t3764800/12964877-f1d0-4bb4-ada1-2c83c7ee223e/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/326e73bf-7000-4d16-9f58-186a5b264e73/Screen%20Shot%202023-12-10%20at%207.59.46%20PM.png)

### Sidewinder G2 Security Appliance Attack Protections Summary – Transport Level Examples

![](https://t3764800.p.clickup-attachments.com/t3764800/e45c89f8-4d1f-4d60-a572-43669ed5693d/Screen%20Shot%202023-12-10%20at%208.00.43%20PM.png)

### Sidewinder G2 Security Appliance Attack Protections Summary – Application Level Examples

![](https://t3764800.p.clickup-attachments.com/t3764800/b9e74e1e-95bf-4cf5-9f37-ec24d9c763f5/Screen%20Shot%202023-12-10%20at%208.01.03%20PM.png)

### Sidewinder G2 Security Appliance Attack Protections Summary – Application Level Examples (Cont.)

![](https://t3764800.p.clickup-attachments.com/t3764800/3537b7ce-9f0e-4c26-8a0c-41311342b8cc/Screen%20Shot%202023-12-10%20at%208.01.21%20PM.png)

###   

## Snort Inline

# **9.7  Example: Unified Threat Management Products**

# **9.8  Key Terms, Review Questions, and Problems**
