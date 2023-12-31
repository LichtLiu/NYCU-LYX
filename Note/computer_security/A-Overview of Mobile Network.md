---
title: "Computer Security Principles and Practice"
permalink: /Computer-Security-Principles-and-Practice/A-Overview-of-Mobile-Network/
layout: default
---
# A-Overview of Mobile Network

# Comments on Jargons

*   Mobile networks use many jargons(行話) and abbreviations(縮寫)
    *   LTE, EPS, Node B, NR
    *   Nested acronyms are common
        *   GERAN = GPRS Evolution Radio Access Network
    *   LTE is often referred to as Evolved Packet System (EPS) in technical situations
*   Learn the jargons and acronyms gradually
    *   There is an associated glossary and cheat-sheet
    *   I do not remember many



# Evolution of mobile networks

## Mobile Internet

![](https://t3764800.p.clickup-attachments.com/t3764800/84aeb07b-2bd2-4bec-8ab9-3279734f6b8b/image.png)

## Mobile Networks

*   Largest deployed infrastructure in par with the Internet
*   Wide-area coverage and pervasive(普遍) connectivity
*   Network services: data, voice, messaging, ...
*   “Anytime, Anywhere” service

## Mobile Services are Ubiquitous

![](https://t3764800.p.clickup-attachments.com/t3764800/d170b11b-f521-4173-b545-cc90b3a0deac/image.png)

## Mobile Network Evolution

![](https://t3764800.p.clickup-attachments.com/t3764800/69b914bd-1cad-469c-a1e6-d2dc0824e471/image.png)

*   **1G**是第一代行動通訊技術，使用模擬信號傳輸語音。1G行動通訊技術在1980年代中期開始普及，代表性標準包括AMPS、NMT、TACS和cdmaOne。
*   **2G**是第二代行動通訊技術，使用數位信號傳輸語音和簡單的數據。2G行動通訊技術在1990年代開始普及，代表性標準包括GSM、GPRS和EDGE。
*   **3G**是第三代行動通訊技術，使用寬頻傳輸語音、數據和多媒體。3G行動通訊技術在2000年代開始普及，代表性標準包括WCDMA、HSPA+和CDMA2000/EVDO。
*   **4G**是第四代行動通訊技術，使用LTE技術傳輸數據。4G行動通訊技術在2010年代開始普及，代表性標準包括LTE-advanced和LTE。
*   **5G**是第五代行動通訊技術，使用NR技術傳輸數據。5G行動通訊技術在2020年代開始普及。

> 1G行動通訊技術只能用於語音通信。  
> 2G行動通訊技術增加了簡單的數據功能。  
> 3G行動通訊技術增加了多媒體功能。  
> 4G行動通訊技術增加了雲計算、物聯網等功能。  
> 5G行動通訊技術將進一步擴展功能，包括高清視頻、虛擬現實、增強現實等。



## Standards Body for Mobile Network: 3GPP

*   An international standards body
*   Evolves and standardizes GSM, UMTS, LTE among others
*   We will primarily discuss 3GPP standards

> _The 3rd Generation Partnership Project (3GPP) unites telecommunications standard development organizations (ARIB, ATIS, CCSA, ETSI, TTA, TTC), known as “Organizational Partners” and provides their members with a stable environment to produce the highly successful Reports and Specifications that define 3GPP technologies_

**What is 3GPP?**

*   **Stands Body for Mobile Network:** As the name suggests, 3GPP (3rd Generation Partnership Project) is an international organization responsible for setting the technical standards for mobile networks.
*   **An international standards body:** It's not a single entity, but rather a collaboration between seven telecommunications standard development organizations from around the world (ARIB, ATIS, CCSA, ETSI, TTA, TTC).
*   **Evolves and standardizes GSM, UMTS, LTE among others:** 3GPP has been instrumental in creating and refining key mobile network technologies like GSM (2G), UMTS (3G), and LTE (4G).

**Why is 3GPP important?**

*   **Stable environment for standards development:** 3GPP provides a platform for its member organizations to work together and ensure consistency and interoperability in mobile network technologies.
*   **Highly successful Reports and Specifications:** The technical specifications and reports produced by 3GPP are the foundation for building and implementing mobile networks globally.
*   **Driving force behind mobile network advancements:** By continuously evolving and refining existing standards and developing new ones, 3GPP plays a pivotal role in pushing the boundaries of mobile technology.

## Cellular Network Standards

![](https://t3764800.p.clickup-attachments.com/t3764800/88b3d8ce-a653-4d79-9d22-2fc9dde0ac3b/image.png)

## From 3G to 4G

![](https://t3764800.p.clickup-attachments.com/t3764800/de54ce47-0edf-4a87-8d6e-01eb691c96e4/image.png)

> _Source_: [http://www.4gamericas.org/](http://www.4gamericas.org/)(Nov 2014)

## 4G Technology

*   4G LTE: First global standard for mobile broadband
    *   More data capacity
    *   Faster speed
    *   Lower latency
    *   New service paradigm (e.g., VoLTE)
        *   allows for high-quality voice calls over the data network. This eliminates the need for switching to a separate 2G or 3G network for calls, providing a smoother and more consistent experience.
*   Key enabler: network architecture evolution
    > The transition to 4G wasn't just about new technology; it also involved significant changes in network architecture. The introduction of technologies like Orthogonal Frequency-Division Multiplexing (OFDM) and Multiple-Input Multiple-Output (MIMO) made the networks more efficient and capable of handling the increased data traffic.

## What is LTE?

*   LTE stands for “Long Term Evolution”
*   Fourth-generation (4G) cellular technology from the 3rd Generation Partnership Project (3GPP)
*   Deployed worldwide
*   All implementations must meet baseline requirements
    *   Increased speed
    *   IP-based network (All circuits are gone!!)
    *   New air interface: OFDMA (Orthogonal Frequency-Division Multiple Access), MIMO (Multiple antennas)
    *   Also includes duplexing, timing, carrier spacing, coding, ...
*   LTE is always evolving and 3GPP often has new “releases”
    *   considered as LTE-Advanced

## Network Architecture Evolution

![](https://t3764800.p.clickup-attachments.com/t3764800/a7930d49-ae37-4f39-9523-46d7a7f7b60e/image.png)

## Inter-Generation Technologies

*   CS networks need to be able to connect with PS networks and other distinct cellular networks
    *   The Internet is a good example of packet-switched (PS) network
*   GPRS (General packet radio service)
    *   2.5G packet switched technology
    *   Introduced in the late 1990s, GPRS was a stepping stone from analog 2G to packet-switched data services.
    *   It offered basic data connectivity for tasks like email and web browsing, with speeds up to 114 kbps.
    *   Imagine GPRS as a narrow dirt road, allowing basic data flow but not ideal for heavy traffic.
*   EDGE (Enhanced Data Rates for GSM Evolution)
    *   2.75G packet switched technology
    *   EDGE was a relatively minor upgrade to GPRS, offering improved data rates up to 384 kbps.
    *   Think of it as widening the dirt road slightly, enabling faster data transfer for basic applications.
*   HSPA (High Speed Packet Access)
    *   3.5/3.75 packet switched data technology
    *   There were a few quick iterations on this technology, thus “variants”
    *   HSPA marked a significant leap forward, providing high-speed data access with multiple variants like HSPA+ and HSPA++.
    *   Speeds could reach up to 168 Mbps, enabling video streaming, music downloads, and other bandwidth-intensive tasks.
    *   Imagine HSPA as a paved highway with multiple lanes, allowing for smooth and efficient data flow for various applications.



# Overview of legacy mobile network

## 2G Network Architecture (GSM)

![](https://t3764800.p.clickup-attachments.com/t3764800/b26b54b4-c3c2-408e-864f-9f26d43bc241/image.png)

### 2G is based on Circuit Switching (CS)



*   End-end resources reserved for “call”
    *   Link bandwidth, switch capacity
    *   Dedicated resources: no sharing
    *   Circuit-like (guaranteed) performance
    *   Call setup required



![](https://t3764800.p.clickup-attachments.com/t3764800/5a9048ba-1980-4eeb-ac41-c8bf84c8fb11/image.png)



### CS Signaling

*   Used to setup, maintain, and tear down VC
*   Used in 2G, as well as in 3G
*   Not used in Today’s Internet

![](https://t3764800.p.clickup-attachments.com/t3764800/07f192fe-beb7-4bfe-8126-39b3397e8a58/image.png)

### Packet Switching (PS)

*   Sequence of A & B packets does not have fixed pattern

> Packets containing data are individually addressed and routed through the network independently.
>
> *   Bandwidth shared on demand→statistical multiplexing
>
> > Instead of reserving a dedicated channel for each user, packet switching dynamically shares the available bandwidth among multiple users and applications.

*   Store-and-forward at intermediate routers

> Each router reads the address on the packet header and directs it towards its destination. This allows efficient routing and avoids congestion at any single point.

*   **Powering** the Internet

> share the same network infrastructure, enabling data transmission, video streaming, online gaming, and countless other services

![](https://t3764800.p.clickup-attachments.com/t3764800/e281efaf-6ba3-4081-b4cd-65f9bfa1abc0/image.png)

### PS Signaling

*   No call setup at network layer
*   Routers: no state about end-to-end connections
    *   No network-level concept of “connection”
*   Packets forwarded using destination host address
    *   Packets between same source-dest pair may take different paths

![](https://t3764800.p.clickup-attachments.com/t3764800/67bad6b7-2a38-4bd0-989d-147bb4062166/image.png)

## 4G Cellular Network Architecture

![](https://t3764800.p.clickup-attachments.com/t3764800/c18a8608-0aa8-4e3c-b94a-9952e75238ad/image.png)

> MME: Mobility Management Entity  
> BS: Base Station

## 3G/4G Cellular Network Architecture

## ![](https://t3764800.p.clickup-attachments.com/t3764800/e9b9ec30-1211-40f9-8da0-cb90db94e257/image.png)

## Upcoming 5G

## ![](https://t3764800.p.clickup-attachments.com/t3764800/450d43b6-6544-4f64-a783-ced96d21eed9/image.png)

## 3G/4G Network Operations

*   Two main planes in operation in parallel
    *   Data/User plane: content delivery
        *   **Function:** Delivering content and information between users and network elements.
        *   **Think of it as:** The cargo hold of the plane, carrying all the data you send and receive
    *   Control plane: signaling functions
        *   **Function:** Signaling and coordinating network resources to establish, maintain, and terminate connections.
        *   **Think of it as:** The cockpit of the plane, sending instructions to keep the data flowing efficiently.
*   There is an additional plane that works with the above two planes
    *   Management plane: configurations, monitoring
        *   **Function:** Configuring, monitoring, and optimizing network performance, security, and resource allocation.
        *   **Think of it as:** The control center of the airport, overseeing the entire operation and making adjustments as needed.



### Illustration of Data and Control Planes

*   RLC: Radio Link Control
*   MAC: Medium Access Control
*   EPS: Evolved Packet System
*   PDCP: Packet Data Convergence Protocol

![](https://t3764800.p.clickup-attachments.com/t3764800/e77d6cea-1ab0-4b5f-ae91-8c150f9f5c8a/image.png)

### Data-Plane Protocols: IP + Lower layers

### ![](https://t3764800.p.clickup-attachments.com/t3764800/393c27a1-6641-4fa3-8de4-59b733bb9a20/image.png)

*   Packet Data Convergence Protocol (PDCP) – header compression, radio encryption
*   Radio Link Control (RLC) – make packets ready to be transferred over the air interface
*   Medium Access Control (MAC) – Multiplexing, QoS



*   空中介面(air interface)由兩個部分組成：
*   物理層（physical layer）：負責無線信號的發射和接收，包括信號調製、解調、編碼和解碼等。
*   數據鏈路層（data link layer）：負責數據的傳輸協議，包括數據包的封裝、傳輸和解包等。
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/8cf03c38-8bc2-4ae3-87c5-19f4b979c7c7/image.png)



### Control Plane in 3G/4G

*   Major control utilities
    *   Radio resource control (RRC)
        *   This function allocates radio resources (channels, power) to mobile devices based on traffic demand and user needs (e.g., voice calls, video streaming).
        *   It ensures efficient utilization of the limited spectrum and prioritizes different types of traffic for optimal performance.
    *   Mobility management Entity (MME)
        *   MME tracks the location of mobile devices as they move between base stations (cell towers).
        *   It seamlessly hands over ongoing calls and data sessions without interruption to the user.
        *   In 4G, the MME plays a central role in the Evolved Packet Core (EPC), managing connections for both voice and data.
    *   Connection management(CM)
        *   This function establishes, maintains, and terminates connections between mobile devices and the network.
        *   It handles tasks like call setup/teardown, session activation/deactivation, and security authentication

![](https://t3764800.p.clickup-attachments.com/t3764800/502fb213-60b3-488b-b699-f49f5938d9c8/image.png)

*   Layered protocol stack
    *   The control plane utilizes a layered protocol stack, with each layer performing specific tasks.
    *   Lower layers handle radio transmission and basic signaling, while higher layers manage network functions like mobility and security.
    *   This modular approach facilitates efficient communication and allows for easier upgrades and adaptations
*   Domains separated for voice (CS) and data (PS)
    *   3G and 4G networks have separate domains for circuit-switched (CS) voice calls and packet-switched (PS) data traffic.
    *   This separation allows for optimized resource allocation and ensures smooth voice quality even during high data usage.
*   Hybrid 3G/4G systems
    *   As 4G technology evolved, operators deployed hybrid networks that support both 3G and 4G services simultaneously.
    *   This allowed for seamless transition and ensured continued service for users with 3G devices while gradually rolling out 4G coverage.

### Distributed Operations

*   Device, Base Station, Core Networks

### ![](https://t3764800.p.clickup-attachments.com/t3764800/c641a4bb-3beb-469b-89e1-c84a6a614935/image.png)

### Data and Control Planes Together

*   EPS: Evolved Packet System
*   PDCP: Packet Data Convergence Protocol
*   RLC: Radio Link Control
*   MAC: Medium Access Control

![](https://t3764800.p.clickup-attachments.com/t3764800/b4548585-6077-4ce9-acd1-731e1761be9b/image.png)

## How to set up data services?

### An Example: Setting Up Data Service in 4G

### ![](https://t3764800.p.clickup-attachments.com/t3764800/4e799701-1af5-47ff-b7e3-5cabe05d0715/image.png)

## 4G Security Mechanisms

## ![](https://t3764800.p.clickup-attachments.com/t3764800/a2ed6f9d-0216-4403-8265-64a1cb9931b5/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/ff8ffd9c-a5d3-45c3-8b46-d8ba0dc40253/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/fb739699-0c33-40a9-9593-1908903e2ade/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/52a7fc84-de73-4eee-91b3-f1e0ed1648da/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/60aabc68-84a6-46bd-9488-02fd62d8c4c5/image.png)

# Case Studies on 3G/4G vulnerabilities

## Case Study on 4G Vulnerabilities

*   4G VoLTE (Voice over LTE)
    *   Free data service attack
    *   Voice DoS attack
*   4G SMS (Short Message Service)
    *   SMS Spoofing attack
*   4G VoWi-Fi (Voice over Wi-Fi)
    *   Stealthy call DoS attack
    *   Concurrent ghost calls attack

### VoLTE: Carrying Voice in Packets

![](https://t3764800.p.clickup-attachments.com/t3764800/d6cb1aee-0235-4ab5-9fde-a12bb7d4b36f/image.png)

#### Free Data-Service Attack against VoLTE

*   Set up a data tunnel over VoLTE signaling bearer
    *   Free mobile-to-Internet data service![](https://t3764800.p.clickup-attachments.com/t3764800/a136ad32-376f-4110-a046-bb9e605bde28/image.png)
    *   Free mobile-to-mobile data service ![](https://t3764800.p.clickup-attachments.com/t3764800/eebcd811-6e56-4adb-86df-41c7d936366f/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/f3a6a41c-399a-4b84-826d-05a402ac3d07/image.png)



### Voice DoS Attack against VoLTE

*   Voice denial-of-service(DoS) attack
    *   Attacker: malware without root privilege
    *   Victim: mobile user
    *   Validated in two major US carriers
    *   Validated in two mobile phones Samsung and Sharp (Qualcomm modem)
*   Different from conventional call attacks
    *   Conventional: calls cannot be set up
    *   Our attack: calls can be set up, but caller and callee cannot hear each other



### SMS Spoofing Against SMS-powered Services

*   Case Study: Facebook Text Service (FTS)
    *   Maliciously manipulate victim’s FB account: update status, add friends, and add Like
    *   Victim doesn’t need to be involved

![](https://t3764800.p.clickup-attachments.com/t3764800/d55d6f2c-fe18-405b-9c95-e210c94eceac/image.png)

#### SMS Spoofing Attack Snapshots (Facebook)

*   Against Facebook Text Service

![](https://t3764800.p.clickup-attachments.com/t3764800/c3272d9a-aece-4834-95ab-d51b11bac8e3/image.png)

### ![](https://t3764800.p.clickup-attachments.com/t3764800/de749b9d-c919-4802-82d8-97adb9ba713e/image.png)Stealthy Call DoS Attack

*   Stealthy call Denial-of-Service (DoS) attack on personal phones
    *   No ring tones to victims!!
    *   97.6% DoS time without user awareness
*   Demo Scenario

## ![](https://t3764800.p.clickup-attachments.com/t3764800/eedda4d7-858b-4c35-a8bf-3a60365185fa/image.png)



### Concurrent Ghost Calls Attack

*   Ghost-call Attacks: large-scale concurrent call attempts
    *   Social engineering with missed calls
    *   DoS on multi-line telephony systems (e.g., enterprise, emergency)
*   Demo Scenario

### ![](https://t3764800.p.clickup-attachments.com/t3764800/7e4ef0cf-cd3a-4612-bcdb-04056063b8c8/image.png)

# Overview of 5G mobile network

## 5G aims: eMBB, MCC, MIoT

![](https://t3764800.p.clickup-attachments.com/t3764800/ebdd92f6-9d03-430b-a5bc-3ad9407348cf/image.png)

### 5G versus 4G

![](https://t3764800.p.clickup-attachments.com/t3764800/5770c883-08bc-4e49-a4c9-cfbf47c032cd/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/177fba5f-b983-4fd4-aee2-6ff5104db71a/image.png)

### 5G Network Architecture

### ![](https://t3764800.p.clickup-attachments.com/t3764800/5a8a4624-48de-40ac-a3eb-adc7bdd82d86/image.png)

### Enhanced Mobile Broadband (eMBB)

*   Unifying network capacity and peak data rates in the always- changing area of consumer needs and wants
*   Addressing issues in using mobile communication (from a survey result of Qualcomm and Nokia)
    *   48% of consumers don’t want to log on to public Wi-Fi again; they want lightning-fast browsing
    *   37% desire to download content 10 times faster
    *   27% desire to enjoy better quality for video calls

### How does 5G Deliver eMBB?

*   Needs: higher throughput, lower latency, greater capacity, better uniformity and complete mobility
*   Communication technologies
    *   Massive MIMO: increasing cellular coverage and capacity through the use of large numbers of antennas (觸角)
        *   Using up to 256 antenna elements in the base station: intelligent beamforming/beam-tracking
    *   Device-centric mobility: sending out periodic reference signals for the access network to monitor
        *   Network-triggered cell reselect or handover based on the uplink signal strength
    *   Spectrum sharing: unlocking more spectrum; in the higher bands, large swaths of spectrum may be shared or unlicensed
        *   5G NR is designed to support all current spectrum types with the flexibility
    *   mmWave: high-speed, high-capacity data links in the greenfield spectrum bands above 24GHz
        *   But with higher path loss, susceptibility to blockage from physical barriers
        *   Leveraging multi-connectivity with 5G sub-6 GHz and/or Gigabit LTE to improve overall link robustness
    *   Gigabit LTE: pioneering many new LTE Advance Pro technologies
        *   Carrier aggregation: achieving wider bandwidths (e.g., 80 MHz)
        *   Share and unlicensed spectrum (e.g., LAA)
        *   Higher-order modulations (e.g., 256-QAM)
        *   Many more antennas (e.g., 4x4 MIMO)

### Mission-Critical Control

*   Faster than humans can think; failure is not an option
    *   Industrial automation
    *   Smart-city infrastructure
    *   Automated guided vehicles (AGV)
    *   Robots and drones
    *   Safety-related and autonomous systems in vehicles
    *   Remote medical procedures

### How does 5G Deliver Mission-Critical Control?

*   enhanced ultra-reliable, low-latency communication (eURLLC)
    *   “six nines” of reliability or packet loss as low as 0.0001%
    *   Latencies below 1 ms
*   Communication technologies
    *   Scalable slot duration down to 125 us
    *   Efficient multiplexing of mission-critical transmissions with scheduled traffic
        *   Allowing time-sensitive transmissions to take higher priority over nominal traffic
        *   Asynchronous and can occur at any time→puncture an ongoing, scheduled transmission
        *   An additional layer of FEC coding→self-recover without excessive retransmissions
    *   Redundant links to mission-critical devices with multi-connectivity
        *   Connect across multiple 5G network nodes, or even 4G LTE or Wi-Fi depending on reliability level needed
        *   D2D communications to enable direct exchange of real-time information
    *   Spectrum sharing allows for more-predictable QoS

![](https://t3764800.p.clickup-attachments.com/t3764800/0abcf321-bc5a-4f1d-a07e-97af43db1679/image.png)

### Massive Internet of Things (IoT)

*   More efficiently connect the wide variety of IoT devices and services
*   Communication technologies
    *   Upon the foundation of NB-IoT(窄帶物聯網)
        *   Lowering device complexity, reducing power consumption, deepening coverage, and enabling higher node density deployments
    *   More efficient uplink transmission scheme for IoT with RSMA(**Resource Spread 多重存取協定**) 非同步、非正交、基於競爭的存取協定，無需事先網絡排程即可進行通信。
        *   Even higher node density at lower complexity(降低了設備複雜性，減少了功耗，提高了覆蓋範圍，並支持高密度節點部署)
        *   RSMA (Resource Spread Multiple Access): asynchronous, non-orthogonal, and contention-based access protocol→communication without prior network scheduling
    *   WAN-managed multi-hop mesh to extend network coverage
        *   Allowing out-of-coverage devices to connect (e.g., deep underground)

### 5G Revolution

*   Delivering multi-network slicing, multi-level of services and multi- connectivity network capabilities （可根據不同需求和服務級別進行配置）
    *   Required flexibility, agility and economies of scale
    *   Calling for virtualization and software-defined networking
*   Addressing many threats faced in today’s 4G/3G/2G
    *   e.g., new mutual authentication capabilities
*   However, adopting new network technologies (e.g., NFV) introduces new potential threats→increasing attack surface

### 5G Increases Attack Surfaces from All Aspects

*   Attack Surface: consist of the reachable and exploitable vulnerabilities in a system
    *   Network attack surface
        *   Network protocol vulnerabilities
        *   e.g., open ports on outward facing Web and other servers
    *   Software attack surface
        *   Vulnerabilities in application, utility, or operating system code ◼ e.g., interfaces, SQL, and web forms
    *   Human attack surface
        *   Vulnerabilities created by personnel
        *   e.g., an employee with access to sensitive info vulnerable to a social engineering attack

## 5G System Architecture

*   Service-based representation
    *   NFs within the Control Plane enables other authorized NFs to access their services
*   Reference-based representation
    *   Showing the interaction exist between NF services in the NFs
    *   Described by point-to-point reference point (e.g., N11) between any two NFs (e.g., AMF and SMF)

![](https://t3764800.p.clickup-attachments.com/t3764800/37c5138e-dbf4-47e0-9cff-cc07d19ae89e/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/84ac52fb-8295-40ba-ae5d-3436778eafda/image.png)

## 5G Security

### Secure Design Principles are Adopted

*   Use of Mutual Authentication
    *   Confirming sender and receiver have an established trust and the end-to-end relationship is secured
*   A presumed “open”(not secure) network→complete mediation
    *   Removing any assumption of safety from overlaid products or processes
*   An acknowledgement that all links could be tapped(**Interception攔截**)
    *   Mandating encryption of inter/intra-network traffic
    *   Ensuring the encrypted information is worthless when intercepted

### Subscriber and Device Protection

*   Protecting the confidentiality of the initial non-access stratum (NAS) messages between device and network
    *   Against man in the middle (MITM) and fake base station attacks
*   Home control: final device authentication to a visited network is completed after the home network has checked the auth. Status
    *   Against various roaming fraud(漫遊欺騙) types
*   Unified authentication across other access network types (e.g., WLAN)
    *   Against attacks from previously unmanaged and unsecured connections
*   User plane integrity checking
*   Privacy protection using public/private key pairs
    *   Concealing subscriber identity and deriving keys
    *   SUPI (Subscription Permanent ID)→SUCI (Subscription concealed ID)

### Network Protection

*   New IT Protocol Stack
    *   Shifting from proprietary protocols for network management to an IP-based protocol stack
        *   HTTP/2 over N32: replacing Diameter over the S6a reference point
        *   TLS for providing encrypted communication between all network functions (NF) inside a PLMN
        *   TCP as the transport layer protocol: replacing SCTP
        *   RESTful framework with OpenAPI 3.0.0 as the Interface Definition Language (IDL)
    *   Allowing interoperability with many services and technologies
    *   Leading to a short vulnerability to exploitation timeline
        *   Higher impact of vulnerabilities
    *   Expanding the potential pool of attackers

#### New Network Technologies and Threats

*   Virtualization
    *   Service-based network architecture
        *   Core network operations may be performed through functions outside the operator network
    *   Containerization: OS-level virtualization
        *   Tenancy isolation within a virtual environment is not guaranteed (e.g., Spectre and Meltdown)
        *   Containers may be escaped when run as root
    *   Management and orchestration processes (MANO)
        *   All virtualization technologies enable network segmentation and resource isolation, ensuring security and reducing the impact of successful attacks
        *   However, poor MANO may nullify them
    *   Hypervisor: brain of virtualized technologies
        *   Hypervisor may have bugs
*   Cloud services
    *   Exposing rich services through the Cloud and Restful API
    *   Secure coding practices should be followed
    *   Otherwise, data may be leaked or code may be exploited
*   Network slicing
    *   Customizing network behavior and adapting network to service specific use cases
    *   Security model for each slice should be adapted to the use case
    *   Different levels of isolation shall span from core network to radio access
*   Mobile IoT
    *   IoT needs to be securely coded, deployed and managed through its lifecycle
    *   Most IoT services share a common architecture
        *   Attacks on the devices via the apps running on the device, remote attacks from the internet and via physical attack
        *   Attacks on service platforms (i.e., the cloud)
        *   Attacks on the communications links (e.g., Cellular, WLAN, etc.)
*   embedded SIM (eSIM)
    *   Data downloaded in the form of an eSIM profile via HTTPS into a secure element (eUICC) permanently embedded into mobile device
        *   A remote SIM provisioning platform (SM-DP+) and eUICC mutually authenticate each other using PKI certificates
    *   eUICC, identified by a globally unique EID, is able to store many profiles
        *   Each profile is used to identify and authenticate the subscriber
*   Artificial intelligence
    *   AI may be used for automate threat and fraud detection
    *   However, AI-driven attacks are anticipated

## Security Comparison between 4G and 5G

| **Function** | **4G** | **5G** |
| ---| ---| --- |
| **Privacy and Integrity Cipher** | Encryption on radio path between mobile station and eNodeB<br>Control plane ciphering and integrity between UE and MME<br>128-bit algorithms supported<br> | In addition to LTE:<br>Current support of 256-bit algorithms proposed for future release<br>Integrity implemented preventing unauthorized change of user data<br> |
| **Authentication Key Agreement (AKA)**<br> | Shared key provisioned in the UICC and the AUSF (Authentication Server Function) in the network<br>Mutual authentication between the UE and the network<br> | In addition to LTE:<br>Access-agnostic authentication (EAP). 5G-AKA and EAP-AKA’ supported for both 3GPP and non-3GPP access technologies<br>Protects the confidentiality of the initial non-access stratum (NAS) messages between the device and the network<br> |
| **Security Anchor Function (SEAF) or anchor key**<br> | None<br> | Allows UE re-authentication without having to run full authentication<br>• when moving between different<br>access networks or even serving networks |
| **Subscriber Permanent Identifier (SUPI)**<br> | Identifier sent in plaintext prior to network<br>authentication | Subscription Concealed Identifier (SUCI)<br>• using home network public key to<br>encrypt MSIN (Mobile Subscriber Identification Number) part of the subscriber identifier (IMSI) for confidentiality |
| **Home Control**<br> | None<br> | HPMN (Home Public Mobile Network) can verify that UE is present and requesting service from the VPMN<br>HPMN 和 VPMN 的區別在於：<br>**HPMN 是行動用戶所訂閱的行動網路營運商的網路，而 VPMN 是訪問網路營運商的網路。**<br>• against roaming scenarios and fraud<br>prevention |
| **Security Edge Proxy Protection**<br> | None<br> | Security gateway on interconnections between home network and visited networks<br>• Protecting home network edge |
| **Network Exposure Function (NEF)** | None<br> | NF securely expose capabilities and events to 3rd party application functions (AF) via NEF<br>Enabling secure provision of information in the 3GPP network by authenticated and authorized AFs<br>Certificate based mutual authentication may be used<br>After authentication, NEF determines whether the AF is authorized to send requests for the 3GPP network entity<br> |

> Network Exposure Function (NEF) 是位於核心網路和第三方應用程式之間的功能，它負責將網路服務和功能暴露給第三方應用程式。NEF 使用 API 和其他技術來提供對網路服務的安全訪問。







#
