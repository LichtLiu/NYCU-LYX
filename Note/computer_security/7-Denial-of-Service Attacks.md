---
title: "Computer Security Principles and Practice"
permalink: /Computer-Security-Principles-and-Practice/7-Denial-of-Service-Attacks/
layout: default
---
# 7-Denial-of-Service Attacks

# **7.1  Denial-of-Service Attacks**

*   Compromise availability by hindering or blocking completely the provision of some services
    *   e.g., flooding a Web server with so many spurious requests
*   Nowadays: distributed denial-of-service (DDoS) attacks
    *   Due to Internet bandwidth growth
    *   400 Mbps (2002)→100 Gbps (2010)→300 Gbps (Spamhaus in 2013)
    *   50 Gbps: power enough to exceed the bandwidth capacity of any target
*   Reason for attack:
    *   financial extortion(勒索), hacktivism, and state-sponsored attacks on opponents
*   

## The Nature of Denial-of-Service Attacks

*   NIST \[SP 800-61\] defines DoS attack:

> A denial of service (DoS) is an action that prevents or impairs the authorized use of networks, systems, or applications, by **_exhausting resources_** such as central processing units (CPU), memory, bandwidth, and disk space.

### Categories of Resources

*   Network bandwidth
    *   Relates to the capacity of the network links connecting a server to the Internet
    *   For most organizations this is their connection to their Internet Service Provider (ISP)
*   System resources
    *   Aims to overload or crash the network handling software
*   Application resources
    *   Typically involves a large number of valid requests, each of which consumes significant resources
    *   Thus limiting the ability of the server to respond to requests from other users ![](https://t3764800.p.clickup-attachments.com/t3764800/93834089-661f-4104-8fad-3a9b9a3747db/Screen%20Shot%202023-11-11%20at%206.36.01%20PM.png)

Figure 7.1, the attacker might use the large company’s Web server to target the medium-sized company with a lower-capacity network connection

> The attack might be as simple as using a flooding ping1 command directed at the Web server in the target company. This traffic can be handled by the higher-capacity links on the path between them, until the final router in the Internet cloud is reached. At this point, some packets must be discarded, with the remainder consuming most of the capacity on the link to the medium-sized company. Other valid traffic will have little chance of surviving discard as the router responds to the resulting congestion on this link.

*   **SYN spoofing** attack
    *   consume the limited resources available on the system
    *   resources: temporary buffers used to hold arriving packets, tables of open connections, and similar memory data structures
*   **poison packet**
    *   attack uses packets whose structure triggers a bug in the system’s network handling software, causing it to crash
    *   e.g. _ping of death_ and _teardrop_ attacks (directed at older Windows 9x systems )

## Classic Denial-of-Service Attacks

*   Ping flooding attack
    *   Traffic: ICMP echo request and response packets
    *   Goal: overwhelm the capacity of network connection to the target organization
    *   Traffic can be handled by higher capacity links on the path, but packets are discarded as capacity decreases
*   Two disadvantages from the attacker’s perspective
    *   Source of the attack is clearly identified
    *   Attack reflection at the source system
        *   Network performance will be noticeably affected



## Source Address Spoofing

*   Forging source addresses (偽造源地址)
    *   偽造源地址是指在 IP 數據包中修改源地址。這通常用於欺騙目標系統或網路，使其誤認為數據包來自其他來源。
    *   Usually via the _raw socket interface_ on OS
*   Consider the _Ping_ flooding attack
    *   Same congestion on the target router
    *   But, ICMP echo response packets are no longer reflected back (but reflected to forged source address)
    *   Randomly spoofed source addresses: backscatter traffic
*   Harder to identify attacking systems
    *   Why?
*   _Why Such Easy Forgery of Source Addresses is Allowed?_
    *       *   the flow of packets of some specific form through the routers along the path from the source to the target system must be identified
*   Development of TCP/IP: generally cooperative, trusting environment ( TCP/IP 開發發生在普遍協作的信任環境中)
    *   Simply does not include the ability to ensure the valid source address (TCP/IP 默認情況下根本不具備確保數據包中的源地址確實與源系統的源地址相符的能力)
*   How to address it?
    *   Impose filtering on routers to ensure it
    *   As close to the originating system as possible (e.g., borders of the ISP’s connection)
*   This has been a long-standing security recommendation (RFC 2827); however, many ISPs DO NOT implement such filtering

## SYN Spoofing

*   Goal: attacking the ability of a network server to respond to TCP conn. requests
*   How?
*   Overflowing the tables used to manage such connections

### Normal TCP Handshake

![](https://t3764800.p.clickup-attachments.com/t3764800/1511364b-7116-4ce5-90a5-6a851af959de/Screen%20Shot%202023-11-11%20at%209.27.30%20PM.png)

1. client system initiates the request for a TCP connection by sending a SYN packet to the server
    1. (client’s address, port, initial sequence number, or request for other TCP options)
2. server responds to the client with a SYN-ACK packet
    1. sequence number for the server, increments the client’s sequence number(confirm receipt of the SYN packet)
3. client receives, sends an ACK packet to the server
    1. incremented server sequence number, marks the connection as established
4. server receives this ACK packet, it also marks the connection as established

### TCP SYN spoofing

*   Generating a very large number of forged connection requests to the server
*   Legitimate users are denied access
*   Different from the basic flooding attack
    *   Actual volume of SYN traffic can be comparatively low
        *   home user, could successfully attack the large company server using a SYN spoofing attack. (不需擠爆link capacity，只要讓table overflow)
*   High enough to keep the known TCP connections table filled
*   attacker ideally wishes to use addresses that will not respond to the SYN-ACK with a RST

![](https://t3764800.p.clickup-attachments.com/t3764800/b64308b0-1011-4a6e-ae64-7b18c5037637/Screen%20Shot%202023-11-11%20at%209.39.23%20PM.png)

# **7.2  Flooding Attacks**

*   Classified based on network protocols
*   Intent: overload the network capacity on some link to a server

## ICMP Flood

*   Ping flood using ICMP echo request packets
*   Traditionally network administrators allow such packets into their networks

## UDP Flood

*   UDP is a connectionless protocol
    *   no connection established between the sender and the receiver before data is sent.
    *   easier for attackers to flood a target system with UDP traffic, as they do not need to maintain a connection to the system.
*   Uses UDP packets directed to some port number on the target system, e.g., DNS

## TCP SYN Flood

*   Sends TCP packets to the target system
*   Total volume of packets is the aim of the attack rather than the system code (造成破壞的關鍵因素是大量封包的總體量,而不是單個封包的具體內容)
*   通過製造海量TCP SYN請求封包,使目標系統忙於處理這些半開連接,耗盡其 TCP 連接資源和計算資源

### TCP SYN Flood 跟 SYN spoofing attack 差別

1. SYN Flood 攻擊
*   攻擊機制: 大量發送SYN請求封包,但不回應伺服器的SYN-ACK封包,導致伺服器大量半開連線堆積,資源耗盡。
*   不需要IP欺騙,使用真實IP即可發動攻擊。
*   主要耗盡目標伺服器TCP連線資源和計算資源。
2. SYN spoofing attack
*   攻擊機制: 使用欺騙的源IP發送SYN請求封包,導致伺服器的SYN-ACK封包發送到不存在的IP,連線打開失敗。
*   依賴IP源地址欺騙,使SYN-ACK發送到虛假IP。
*   主要耗盡目標伺服器的網路頻寬資源。

# **7.3  Distributed Denial-of-Service Attacks**

*   Using multiple systems to generate attacks
    *   Using malware to subvert the system and to install an attack agent, **zombie**
    *   Large collections of such systems under the control of one attacker: [**botnet**](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4622?block=block-8f738495-365c-4745-9b02-82136e7c9824)

![](https://t3764800.p.clickup-attachments.com/t3764800/a5321cf2-b605-4e4b-8283-8c6378f97772/Screen%20Shot%202023-11-11%20at%2010.20.49%20PM.png)

*   attacker can send a single command to a handler, which then automatically forwards it to all
*   Earliest and best-known DDoS tool: Tribe Flood Network (TFN) – Mixter
    *   Original variant from the 1990s: only exploited Sun Solaris systems
    *   Rewritten as (TFN2K): could run on UNIX, Solaris, and Windows NT
    *   Capable: ICMP flood, SYN flood, UDP flood, and ICMP amplification
    *   Hiding: (1) many compromised systems; (2) encrypted communication
*   Current DDoS tools
    *   Hiding
        *   Using IRC or HTTP servers to communicate with agents, instead of the handler
        *   Agents authentication
*   Best defense: prevent your systems from being compromised

> IRC is one of the earlier instant messaging systems developed, with a number of open source server implementations. It is a popular choice for attackers to use and modify as a handler program able to control large numbers of agents. Using the standard chat mechanisms, the attacker can send a message that is relayed to all agents connected to that channel on the server. Alternatively, the message may be directed to just one or a defined group of agents.

# **7.4  Application-Based Bandwidth Attacks**

*   Force the target to execute resource-consuming operations
*   [SIP](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4562?block=block-75d7a4aa-5b6c-43b8-bdce-ba66e62c8a48) (Session Initiation Protocol) Flood
    *   SIP: a protocol for call setup in Voice over IP (VoIP)
        *   A text-based protocol with a syntax similar to HTTP
        *   Two types: requests and responses
*   HTTP-based attacks
    *   (1) [HTTP Flood](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4562?block=block-46116c4c-e939-4c33-b7b1-41e80c24b3f9); (2) [Slowloris](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4562?block=block-2f27256e-05c6-47be-a711-194d9a159507)

## SIP Flood

SIP(Session Initiation Protocol)是一種用於建立和終止多媒體通話(例如VoIP語音通話)連接的信令協議。

SIP Flood攻擊的具體機制是:

1. 攻擊者產生大量假SIP INVITE請求,發送給VoIP伺服器。
2. VoIP伺服器啟動了為每個INVITE請求建立新的SIP會話。
3. 攻擊者並不回應伺服器的響應,導致大量半開的SIP會話積累。
4. 當累計的半開會話數達到伺服器的負載極限時,新請求就會被丟棄,從而實現DoS效果。
5. 攻擊者可以利用僞造的來源IP進行擴大式的DDoS攻擊。

SIP Flood最終導致VoIP提供商的語音服務不可用。它可以通過消耗VoIP伺服器的計算和記憶體資源來實現DoS效果。

防禦方法包括限制會話數量、檢測異常流量模式等。SYN Flood是類似的TCP連接洪水攻擊。

![](https://t3764800.p.clickup-attachments.com/t3764800/ee606f93-82d5-4721-9adf-894c1dd01966/Screen%20Shot%202023-11-11%20at%2010.50.22%20PM.png)

*   What does the SIP flood attack exploit?
    *   A single INVITE request triggers considerable resource consumption
    *   Attack I: Server resources for processing the INVITE requests
    *   Attack II: Network capacity is consumed
    *   Impact: Legitimate incoming calls are not allowed

![](https://t3764800.p.clickup-attachments.com/t3764800/2cdec377-34be-4588-9f71-87ff835d06ac/Screen%20Shot%202023-11-11%20at%2010.51.11%20PM.png)

## HTTP-Based Attacks

### Http Flood

*   bombarding Web servers with HTTP requests
    *   Consuming considerable resources. How?
*   Example I: an HTTP request to download a large file
    *   Consuming memory, processing, and transmission resources
    *   Causing the Web server to
        *   Read the file from hard disk
        *   Store it in memory
        *   Convert it into a packet stream
        *   Transmit the packets

HTTP洪水型DoS/DDoS攻擊。具體機制是:

*       *       *   攻擊者識別出目標網站上的某個大型文件,比如1GB大小的軟件安裝包。
        *   攻擊者利用程序化工具對該文件URL發動請求洪水。可以是從單個IP,也可以是從成千上萬的僞IP。
        *   網站服務器接受請求後,會啟動源文件大量讀取,佔用大量IO和頻寬資源。
        *   在海量請求同時進行下,網站的網路和計算資源被快速消耗。
        *   如果請求速率超過網站服務能力,會導致服務中斷,實現DoS。



*   Example II: Spidering
    *   Bots start from a given HTTP link and follow all links on the provided Web site in a recursive way

Spidering攻擊是一種針對網站的DoS攻擊手段,攻擊者利用自動爬蟲程序模擬搜索引擎蜘蛛的正常訪問,消耗目標網站的資源。具體特徵包括:

*       *       *   攻擊者使用自定義的爬蟲程序,設定非常高的爬取頻率和速度,每秒鐘大量訪問網站。
        *   爬取請求會模擬正常蜘蛛的user agent,使網站錯誤認為是正常搜索引擎蜘蛛。
        *   爬取請求遵循robots.txt規則,通過允許訪問的URL列表進行全站爬取。
        *   各請求之間間隔很短,不給網站任何喘息時間。
        *   攻擊可以持續很長時間,直到網站資源耗盡。
        *   有些攻擊會直接針對網站後台和管理接口。

防禦手段:

*       *       *   在Nginx等配置rate limit限制請求頻率。
        *   分析user agent,識別可疑爬蟲流量。
        *   封鎖攻擊源IP。
        *   使臨時資源縮放提高容量。



### SLOWLORIS

*   Monopolizing(壟斷) all the available request-handling threads on the Web sever
    *   Common server technique: using multiple threads to support multiple requests
    *   Major idea: sending HTTP requests that never complete
*   How? Need to understand the HTTP protocol
    *   A blank line must be used to indicate the end of the request headers and the beginning of the payload (RFC2616)
    *   Step 1: sending an incomplete request that does not have that blank line
    *   Step 2: sending additional header lines periodically to keep the connection alive
*   Not detected by signature-based solutions: legitimate HTTP traffic
*   Countermeasure:
    *   limiting the rate of incoming connections
    *   varying the timeout on connections as a function of the number of connections
    *   delayed binding



Slowloris攻擊是一種HTTP洪水型DoS攻擊,其攻擊機制如下:

1. 攻擊者建立向目標網站的多個HTTP連接,並發送初始化的HTTP請求。
2. 每個請求在頭部包含Content-Length字段指示非常大的請求內容。
3. 但是攻擊者每次只發送非常小的內容片段,遠小於Content-Length所宣稱的大小。
4. 服務器會等待完整內容到達,以完成請求,這使連接長時間保持打開狀態。
5. 攻擊者不斷重複這一過程,消耗目標網站所有的連接資源。
6. 當連接用盡時,正常用戶就無法訪問網站,達到DoS效果。

Slowloris特點是每個連接流量非常小,不易檢測,但可以長時間佔用連接。例如只發送1字節內容,但聲稱總長1GB。它消耗的主要是連接資源而不是頻寬。

> 連接資源(Connection Resources):  
> 1\. 指系統可以建立的並發TCP連接總數量。  
> 2\. 每個TCP連接會佔用服務器一定的內存和處理資源。  
> 3\. 連接資源受限制最大并發連接數决定。  
> 頻寬(Bandwidth):  
> 1\. 指網絡的資料傳輸容量,單位可以是Mbps。  
> 2\. 受限於網絡接口的物理特性,例如千兆網卡的頻寬。  
> 3\. 頻寬受流量大小影響,但多個小流量連接也可以耗盡。

![](https://t3764800.p.clickup-attachments.com/t3764800/217f3dd0-0f28-4894-b775-e44afba4aad5/Screen%20Shot%202023-11-11%20at%2011.12.24%20PM.png)

> Reference: [https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/HTTP\_Basics.html](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/HTTP_Basics.html)

# **7.5  Reflector and Amplifier Attacks**

*   Normal server systems are used as intermediaries(中間) for attacks
    *   Easier to deploy: their handling of the packets is entirely conventional
    *   Harder to trace back to the actual attacker
*   Reflection attacks
*   Amplification attacks

## Reflection Attacks

*   Sending packets to a known service on the intermediary with a spoofed source address of the victim
    *   The intermediary sends response to the victim
    *   Intermediary systems: high-capacity network servers or routers
*   Moreover, attempting to create a larger response packet
    *   Any generally accessible UDP service could be used
    *   e.g., DNS, SNMP, or ISAKMP services
*   Also for TCP services
    *   e.g., TCP SYN: SYN-ACK and RST packets
*   Fundamental issue: spoofed-source packets

![](https://t3764800.p.clickup-attachments.com/t3764800/bc495967-ff8c-4644-bf0b-a4d30a4dc151/Screen%20Shot%202023-11-11%20at%2011.33.07%20PM.png)

## Amplification Attacks

*   Directing requests to the broadcast address of a network
    *   Using a service handled by large numbers of hosts on the intermediate network
        *   e.g., ping, suitable UDP services (echo)
*   But, TCP services cannot be used for this attack. Why?
    *   TCP 協議無法被用於放大反射型DDoS攻擊的主要原因有:
        1. TCP是面向連接的協議,需要完成三次握手才能建立連接。這使其難以進行IP欺騙。
        2. TCP的應答包不會比請求包更大,所以無法實現流量放大效果。例如SYN-ACK包不會比SYN包更大。
        3. TCP有流量控制機制。如果接收方處理能力有限,可以通過窗口大小通知發送方降低發包速率。
        4. TCP需要維護状态,如SEQ/ACK。這會增加反射器的資源消耗。UDP更容易實現反射攻擊。
        5. TCP握手和重傳機制會降低反射效率。UDP單包更具攻擊優勢。
*   Defense: not allow directed broadcasts to be routed into a network from outside
*   Other defenses:
    *   Blocking spoofed source addresses
    *   limiting network services (e.g., echo and ping) from being accessed from outside

![](https://t3764800.p.clickup-attachments.com/t3764800/c64c135d-db6c-4b67-872a-0131c23dbc2f/Screen%20Shot%202023-11-11%20at%2011.33.21%20PM.png)

## DNS Amplification Attacks

*   Using packets directed at a legitimate DNS server as the intermediary
*   Amplification: converting a small request to a much larger response
    *   Contrasting with the original amplifier attacks: responses from multiple systems
    *   e.g., 60-byte UDP request→a 512-byte UDP response
*   Targeting servers that support the extended DNS features (e.g., IPv6)
    *   Much larger responses of over 4000 bytes are allowed



# **7.6  Defenses Against Denial-of-Service Attacks**

*   These attacks cannot be prevented entirely
*   High traffic volumes may be legitimate
    *   Activity on a very popular site
    *   Described as slashdotted or flash crowd
*   Usual response: provision of significant excess network bandwidth and replicated distributed servers
    *   But, high implementation cost



*   _Four lines of defense against DDoS attacks_
    *   Attack prevention and preemption
        *   Before attack
    *   Attack detection and filtering
        *   During the attack
    *   Attack source traceback and identification
        *   During and after the attack
    *   Attack reaction
        *   After the attack

# **7.7  Responding to a Denial-of-Service Attack**

*   Identify type of attack
    *   Capture and analyze packets
    *   Design filters to block attack traffic upstream
    *   Or identify and correct system/app bug
*   Ask ISP to trace packet flow back to source
    *   May be difficult and time consuming
    *   Necessary if planning legal action
*   Implement contingency plan
    *   Switch to alternate backup servers
    *   Commission new servers at a new site with new addresses
*   Update incident response plan
*   Analyze the attack and the response for future handling

# **7.8  Key Terms, Review Questions, and Problems**

**7.1 Define a denial-of-service (DoS) attack.**

A denial-of-service (DoS) attack is an attempt to make a computer resource unavailable to its intended users. This can be done by overwhelming the system with traffic, or by sending it information that triggers a crash.



**7.2 State the difference between a SYN flooding attack and a SYN spoofing attack.**

A SYN flooding attack overwhelms a target system with SYN packets, which are the first stage of a TCP connection. This can cause the target system to run out of resources and become unavailable.

A SYN spoofing attack is a type of SYN flooding attack in which the attacker spoofs the source address of the SYN packets. This makes it more difficult to trace the attack back to its source.



**7.3 What is the goal of an HTTP flood attack?**

The goal of an HTTP flood attack is to overwhelm a web server with HTTP requests, causing it to crash or become unresponsive.



**7.4 What is a poison packet attack? Give two examples of such an attack.**

A poison packet attack is an attack that sends malformed packets to a target system in an attempt to disrupt its operation. Two examples of poison packet attacks are:

*   Land attacks, which send packets to a target system with the same source and destination IP addresses. This can cause the target system to crash.
*   Teardrop attacks, which send packets to a target system with overlapping IP headers. This can cause the target system to crash or become unresponsive.
*   

**7.5 Why do many DoS attacks use packets with spoofed source addresses?**

Attackers spoof the source addresses of packets in DoS attacks to make it more difficult to trace the attacks back to their sources. This can allow the attackers to remain anonymous and avoid being caught.



**7.6 What is “backscatter traffic?” Which types of DoS attacks can it provide information on? Which types of attacks does it not provide any information on?**

Backscatter traffic is the traffic that is generated by a target system in response to a DoS attack. This traffic can be analyzed to identify the source of the attack, as well as the type of attack that was used.

Backscatter traffic can provide information on the following types of DoS attacks:

*   UDP reflection attacks, in which the attacker sends packets to a target system with the source address of the intended victim. The target system then sends a response to the intended victim, who is unaware of the attack.
*   DNS reflection attacks, in which the attacker sends packets to a DNS server with the source address of the intended victim. The DNS server then sends a response to the intended victim, who is unaware of the attack.

Backscatter traffic cannot provide information on the following types of DoS attacks:

*   SYN flooding attacks, in which the attacker sends SYN packets to the target system with spoofed source addresses.
*   HTTP flood attacks, in which the attacker sends HTTP requests to the target system with spoofed source addresses.

**7.7 What is the difference between a DDoS attack and a classic DoS attack? Why are DDoS attacks considered more potent than classic DoS attacks?**

A DDoS attack is a distributed denial-of-service attack. In a DDoS attack, the attacker uses multiple computers to launch the attack, which can overwhelm the target system more easily than a classic DoS attack.

DDoS attacks are considered more potent than classic DoS attacks because they can generate more traffic and are more difficult to trace back to their sources.



**7.8 What architecture does a DDoS attack typically use?**

A DDoS attack typically uses a botnet architecture. A botnet is a network of compromised computers that are controlled by the attacker. The attacker can use the botnet to send large amounts of traffic to the target system.



**7.9 Define an HTTP flood.**

An HTTP flood is a type of DoS attack in which the attacker sends HTTP requests to the target system with spoofed source addresses. This can overwhelm the target system and cause it to become unresponsive.



**7.10 Define a Slowloris attack.**

A Slowloris attack is a type of DoS attack in which the attacker sends a small number of HTTP requests to the target system, but keeps the connections open for a long period of time. This can overwhelm the target system and cause it to become unresponsive.



**7.11 From an attacker’s perspective, what are the drawbacks of a classic ping flood attack?**

From an attacker's perspective, the drawbacks of a classic ping flood attack are:

*   It is easy to detect and block.
*   It can be traced back to the attacker's source IP address.
*   It is not very effective against systems with large amounts of bandwidth.



**7.12 What defenses are possible against nonspoofed flooding attacks? Can such attacks be entirely prevented?**

There are a number of defenses that can be used against nonspoofed flooding attacks. These include:

*   **Rate limiting:** This involves limiting the number of packets that can be sent from a single source address in a given period of time.
*   **Access control lists (ACLs):** These can be used to block traffic from specific source addresses or networks.
*   **Intrusion detection and prevention systems (IDS/IPS):** These can be used to identify and block DoS attacks.
*   **Firewalls:** These can be used to block traffic from specific sources or networks.

It is not possible to entirely prevent nonspoofed flooding attacks, but these defenses can make it more difficult for attackers to launch successful attacks.



**7.13 What is the purpose of SYN cookies?**

SYN cookies are a technique that can be used to prevent SYN flooding attacks. In a SYN flooding attack, the attacker sends a large number of SYN packets to the target system, which can overwhelm the system and cause it to become unresponsive.

SYN cookies work by replacing the source IP address in SYN packets with a cryptographically generated hash. This means that the target system does not need to store state for each SYN packet, which can help to prevent the system from being overwhelmed.



**7.14 What defences are possible against a DNS amplification attack? Where must these be implemented? Which are unique to this form of attack?**

There are a number of defenses that can be used against a DNS amplification attack. These include:

*   **Rate limiting:** This involves limiting the number of DNS queries that can be sent from a single source address in a given period of time.
*   **Access control lists (ACLs):** These can be used to block DNS queries from specific source addresses or networks.
*   **Intrusion detection and prevention systems (IDS/IPS):** These can be used to identify and block DNS amplification attacks.
*   **Firewalls:** These can be used to block DNS queries from specific sources or networks.

In addition to these general defenses, there are a number of defenses that are unique to DNS amplification attacks. These include:

*   **Using a DNSSEC-signed zone:** This can help to prevent attackers from forging DNS responses.
*   **Implementing response rate limiting (RRL):** This can help to prevent attackers from sending a large number of DNS queries to a single DNS server.

These defenses must be implemented at the DNS servers that are being targeted by the attack.



**7.15 What defenses are possible to prevent an organization’s systems being used as inter- mediaries in a broadcast amplification attack?**

There are a number of defenses that can be used to prevent an organization's systems from being used as intermediaries in a broadcast amplification attack. These include:

*   **Filtering traffic to broadcast addresses:** This can be done using firewalls or routers.
*   **Disabling unnecessary services:** This can help to reduce the number of attack vectors that are available to attackers.
*   **Keeping software up to date:** This can help to patch security vulnerabilities that could be exploited by attackers.
*   **Educating employees about DoS attacks:** This can help to reduce the likelihood that employees will click on malicious links or open infected attachments.



**7.16 To what do the terms slashdotted and flash crowd refer to? What is the relation between these instances of legitimate network overload and the consequences of a DoS attack?**

The terms "slashdotted" and "flash crowd" refer to two legitimate instances of network overload.

*   **Slashdotted** refers to the phenomenon of a website being overwhelmed by traffic after being linked to on the popular technology news website Slashdot.
*   **Flash crowd** refers to a sudden surge in traffic to a website or service, typically caused by a news event or a popular promotion.

These instances of legitimate network overload are related to the consequences of a DoS attack in that they both can cause a website or service to become unavailable to users. However, there are some key differences between the two.

*   **DoS attacks** are intentionally malicious, whereas slashdotted and flash crowds are not.
*   **DoS attacks** are typically targeted at specific websites or services, whereas slashdotted and flash crowds can affect any website or service that is popular enough to be linked to on Slashdot or to experience a sudden surge in traffic.



**7.17 What steps should be taken when a DoS attack is detected?**

When a DoS attack is detected, it is crucial to take swift and decisive action to mitigate the damage and restore normal operations. Here's a step-by-step guide to effectively respond to a DoS attack:

1. **Identify the type of attack:** The first step is to determine the nature of the DoS attack, such as a SYN flood, UDP flood, or DNS amplification attack. This will help in implementing the appropriate defense mechanisms.
2. **Identify the source of the attack:** This involves analyzing traffic patterns, network logs, and using specialized tools to pinpoint the origin of the attack traffic. This can be challenging due to spoofed IP addresses, but it's essential for blocking the attacker and preventing future attacks.
3. **Block the source of the attack:** Once the source is identified, take steps to block the attack traffic. This can be done through firewalls, access control lists (ACLs), and routing blackholes. It may also involve coordinating with upstream internet providers to block the malicious traffic.
4. **Absorb the attack:** If blocking the source is not immediately feasible or the attack is too large, the network needs to be able to absorb the attack traffic. This may require increasing network capacity, adding more bandwidth or servers, or implementing load balancing and traffic shaping techniques.
5. **Monitor and analyze:** Continuously monitor network traffic and analyze attack logs to identify any new or recurring attacks. This allows for proactive defense measures and quick response times.
6. **Recover and assess:** Once the attack has subsided, take steps to recover from any damage caused by the attack, such as restoring lost data or repairing network infrastructure. Conduct a thorough post-mortem analysis to identify vulnerabilities, improve security measures, and prevent future attacks.



**7.18 What measures are needed to trace the source of various types of packets used in a DoS attack? Are some types of packets easier to trace back to their source than others?**

Tracing the source of packets used in a DoS attack can be challenging due to spoofed IP addresses and distributed attack techniques. However, there are several measures that can be employed to identify the attacker's origin:

1. **Traffic analysis:** Analyze network traffic patterns to identify anomalies, such as sudden spikes in traffic or unusual traffic patterns from specific sources. This can help narrow down the range of potential attackers.
2. **Network forensics:** Collect and analyze data from network devices, such as routers, firewalls, and intrusion detection/prevention systems (IDS/IPS). This data can reveal valuable information about the attack traffic, such as source IP addresses, packet headers, and timestamps.
3. **Honeytokens:** Deploy honeytokens, which are fake systems designed to attract attackers. When an attacker interacts with a honeytoken, their actions and identity can be logged, providing valuable insights into their tactics and potential location.
4. **Collaboration with ISPs:** Collaborate with internet service providers (ISPs) to track the attack traffic upstream. ISPs may have access to more detailed network data and can assist in identifying the source of the attack.

The difficulty of tracing the source depends on the type of packets used in the attack:

*   **TCP packets:** TCP packets are relatively easier to trace due to their structure, which includes source and destination IP addresses, port numbers, and sequence numbers.
*   **UDP packets:** UDP packets are more challenging to trace because they lack sequence numbers and other identifying information. Tracing them may require analyzing packet headers, timestamps, and traffic patterns.
*   **ICMP packets:** ICMP packets are particularly difficult to trace due to their inherent nature of being used for network diagnostics and control. Tracing them often requires specific tools and in-depth network analysis.

In general, tracing the source of DoS attack packets is a complex task that requires a combination of network analysis, specialized tools, and collaboration with ISPs. The difficulty of tracing depends on the type of packets used, the attacker's level of sophistication, and the availability of network data.
