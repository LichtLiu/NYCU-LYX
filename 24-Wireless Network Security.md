---
title: "Computer Security Principles and Practice"
permalink: /Computer-Security-Principles-and-Practice/24-Wireless-Network-Security/
layout: default
---
# 24-Wireless Network Security

# **24.1  Wireless Security**

*   Key factors: contributing to higher security risks (v.s. wired networks)
    *   Channel
        *   Broadcast communications: more susceptible to eavesdropping and jamming
        *   Vulnerabilities in communication protocols
    *   Mobility
        *   More portable and mobile
    *   Resources
        *   Smartphones/tablets: sophisticated OS but limited memory and processing resources
    *   Accessibility
        *   Sensors/robots: may be left unattended in remote and/or hostile locations



wireless environment consists of three components that provide point of attack:

1. wireless client
    1. mobile phone, a Wi-Fi enabled laptop or tablet, a wireless sensor, a Bluetooth device
2. wireless access point
    1. mobile phone towers, Wi-Fi hot spots, and wireless access points to wired local or wide-area networks
3. transmission medium
    1. carries the radio waves for data transfer

![](https://t3764800.p.clickup-attachments.com/t3764800/ad31e7a7-8e6e-4b1f-ba09-caa004d9a419/Screen%20Shot%202023-11-12%20at%203.41.38%20PM.png)

## Wireless Network Threats

**Accidental association:**

*   Users may unintentionally connect to a neighboring wireless network, exposing resources to the accidental user.

**Malicious association:**

*   Attackers can set up fake wireless access points to steal passwords and gain access to wired networks.

**Ad hoc networks:**

*   Lack of central control makes ad hoc networks vulnerable to security threats.

**Nontraditional networks:**

*   Personal network Bluetooth devices, barcode readers, and handheld PDAs pose security risks due to eavesdropping and spoofing.

**Identity theft (MAC spoofing):**

*   Attackers can eavesdrop on network traffic and identify MAC addresses of computers with network privileges.

**Man-in-the-middle attacks:**

*   Attackers can intercept communication between a user and an access point.

**Denial-of-service (DoS):**

*   Attackers can bombard wireless access points with various protocol messages to consume system resources.

**Network injection:**

*   Attackers can target wireless access points exposed to non-filtered network traffic to disrupt network performance.



## Wireless Security Measures

### Securing wireless transmissions

*   Principal threats: eavesdropping, altering, or inserting messages, and disruption
    *   Countermeasures for eavesdropping
        *   Signal-hiding techniques
            *   Organizations can make it more difficult for attackers to locate their wireless access points by:
                *   Turning off SSID broadcasting
                *   Assigning cryptic names to SSIDs
                *   Reducing signal strength
                *   Locating access points in the interior of buildings
            *   Greater security can be achieved by using directional antennas and signal-shielding techniques.
        *   Encryption
            *   Encryption of all wireless transmission is effective against eavesdropping(偷聽) to the extent that the encryption keys are secured.
    *   For altering and inserting
        *   Encryption and authentication protocols
    *   For disruption
        *   Detection

### Securing Wireless access Points

*   threat: unauthorized access to the network
*   countermeasure:
    *   IEEE 802.1X standard for port-based network access control
        *   Provide an authentication mechanism
        *   prevent rogue access points and other unauthorized devices from becoming insecure backdoors

![](https://t3764800.p.clickup-attachments.com/t3764800/b46d6261-213e-47d2-afc6-a7f7d9ed4b13/Screen%20Shot%202023-11-12%20at%203.59.50%20PM.png)

### Securing Wireless Networks

techniques for wireless network security:

1. **Use encryption****. Wireless routers are typically equipped with built-in encryption mechanisms for router-to-router traffic.**
2. **Use anti-virus and anti-spyware software, and a firewall****. These facilities should be enabled on all wireless network endpoints.**
3. **Turn off identifier broadcasting****. Wireless routers are typically configured to broadcast an identifying signal so that any device within range can learn of the router’s existence. If a network is configured so authorized devices know the iden- tity of routers, this capability can be disabled to thwart attackers.**
4. **Change the identifier on your router from the default****. Again, this measure thwarts attackers who will attempt to gain access to a wireless network using default router identifiers.**
5. **Change your router’s pre-set password for administration****. This is another prudent step.**
6. **Allow only specific computers to access your wireless network****. A router can be configured to only communicate with approved MAC addresses. Of course, MAC addresses can be spoofed, so this is just one element of a security strategy.**

# **24.2  Mobile Device Security**

*   An organization’s networks must accommodate
    *   Growing use of new devices
        *   Significant growth in employee’s use of mobile devices
    *   Cloud-based apps
        *   Apps no longer run solely on physical servers
    *   de-**perimeterization(**去邊界化**)**
        *   A multitude of network perimeters around devices, apps, user, and data
    *   External business requirements
        *   Provide guests, third-party contractors, and business partners network access

## Security Threats

*   **Lack of physical security controls****:** Mobile devices are often outside the organization's control, making them vulnerable to theft and tampering.
*   **Use of untrusted mobile devices****:** Employees may use personal smartphones and/or tablets, which may not be trustworthy.
*   **Use of untrusted networks****:** Mobile devices may connect to untrusted networks, making them susceptible to eavesdropping or man-in-the-middle attacks.
*   **Use of untrusted applications****:** Mobile devices can easily install third-party applications, which may be malicious.
*   **Interaction with other systems****:** Mobile devices may synchronize data with other computing devices and cloud-based storage, which may be insecure.
*   **Use of untrusted content****:** Mobile devices may access and use untrusted content, such as malicious QR codes.
*   **Use of location services****:** The GPS capability on mobile devices can be used to track the device's location, which may be a security risk.

## Mobile Device Security Strategy

![](https://t3764800.p.clickup-attachments.com/t3764800/71a46bc0-5c86-4907-b1f5-8d967748a646/Screen%20Shot%202023-11-12%20at%204.10.37%20PM.png)

*   Device security
    *   Supply mobile devices for employee use and pre-configure those devices
    *   or bring-your-own-device (BYOD) policy
        *   Configuration guidelines for OS and apps (e.g., rooted is not allowed)
*   Traffic security
    *   based on encryption and authentication
    *   via a VPN
*   Barrier security
    *   Firewall policies specific to mobile device traffic

# **24.3  IEEE 802.11 Wireless LAN Overview**

1. IEEE 802 ➝ LANs
2. IEEE 802.11 ➝ wireless LANs (WLANs)

**Table 24.1 IEEE 802.11 Terminology**

| Access point (AP) | Any entity that has station functionality and provides access to the distribution system via the wireless medium for associated stations |
| ---| --- |
| Basic service set (BSS) | A set of stations controlled by a single coordination function |
| Coordination function | The logical function that determines when a station operating within a BSS is permitted to transmit and may be able to receive PDUs |
| Distribution system (DS) | A system used to interconnect a set of BSSs and integrated LANs to create an ESS |
| Extended service set (ESS) | A set of one or more interconnected BSSs and integrated LANs that appear as a single BSS to the LLC layer at any station associated with one of these BSSs |
| MAC protocol data unit (MPDU) | The unit of data exchanged between two peer MAC entities using the services of the physical layer |
| MAC service data unit (MSDU) | Information that is delivered as a unit between MAC users |
| Station | Any device that contains an IEEE 802.11 conformant MAC and physical layer |

## The Wi-Fi Alliance

*   802.11b
    *   First 802.11 standard to gain broad industry acceptance
*   Wireless Ethernet Compatibility Alliance (WECA)
    *   Industry consortium(聯合) formed in 1999: interoperation between vendors
*   Term used for certified 802.11b products: Wi-Fi
*   Wi-Fi Protected Access (WPA)
    *   Certification procedures for IEEE802.11 security standards
    *   Most recent version: WPA2
        *   incorporates all of the features of the IEEE 802.11i WLAN security specification

## IEEE 802 Protocol Architecture

### Physical Layer

*   The lowest layer of the IEEE 802 reference model
    *   encoding/decoding of signals and bit transmission/reception
    *   specification of the transmission medium

### Medium Access Control **(MAC)**

*   controlling access orderly and efficient use of that capacity
*   receives data from a higher-layer protocol (logical link control (LLC))➝ known as **MAC service data unit (MSDU)**
    *   On transmission, assemble data into a frame, known as a **MAC protocol data unit (MPDU)** with address and error-detection fields.
    *   On reception, disassemble frame, and perform address recognition and error detection.
    *   Govern access to the LAN transmission medium.

MPDU format

![](https://t3764800.p.clickup-attachments.com/t3764800/6aeca9a2-9872-4d5c-8d45-61949f15f666/Screen%20Shot%202023-11-12%20at%204.30.25%20PM.png)

*   MAC Control field: contains protocol control information for the MAC protocol functions like priority.
*   Destination MAC Address field: specifies the destination physical address on the LAN for the MPDU frame.
*   Source MAC Address field: The source physical address on the LAN for this MPDU.
*   *   MAC Service Data Unit field: contains the data passed down from the higher layer.
*   CRC (Frame Check Sequence) field(幀檢查序列): contains the cyclic redundancy check/error detecting code calculated over the entire frame contents. It is used by the receiver to detect any errors in the frame.(包含對整個幀內容計算的循環冗餘檢查/錯誤檢測代碼。接收器使用它來檢測幀中的任何錯誤。)



### Logical Link Control

1. MAC layer
    1. responsible for detecting errors and discarding any frames that contain errors.
2. LLC layer
    1. optionally keeps track of which frames have been successfully received and retransmits unsuccessful frames.

## IEEE 802.11 Network Components and Architectural Model

1. **basic service set (BSS) :** smallest building block of a wireless LAN
2. **distribution system (DS) :** backbone
3. BSS ➝ **access point (AP) ➝ DS**

![](https://t3764800.p.clickup-attachments.com/t3764800/9f1a2ee1-7f9b-4af1-900f-bfd4acc22ddf/Screen%20Shot%202023-11-12%20at%204.38.20%20PM.png)

*   Independent Basic Service Set (IBSS)
    *   wireless network communicate directly with each (without AP)
    *   ad hoc
    *   it is formed spontaneously as stations come into range of each other
*   Extended Service Set (ESS)
    *   a collection of two or more basic service sets (BSS) that are interconnected by a distribution system
    *   roam freely between different BSSs within the ESS
    *   possible for two BSSs to overlap geographically ➝ single station could participate in more than one BSS



## IEEE 802.11 Services

two ways of categorizing IEEE 802.11 services

1. The service provider can be either the station or the DS.
2. Three of the services ➝ used to control IEEE 802.11 LAN access and confidentiality

Six of the services ➝ used to support delivery of MSDUs between stations

**Table 24.2 IEEE 802.11 Services**

| **Service** | **Provider** | **Used to support** |
| ---| ---| --- |
| Association | Distribution system | MSDU delivery |
| Authentication | Station | LAN access and security |
| Deauthentication | Station | LAN access and security |
| Disassociation | Distribution system | MSDU delivery |
| Distribution | Distribution system | MSDU delivery |
| Integration | Distribution system | MSDU delivery |
| MSDU delivery | Station | MSDU delivery |
| Privacy | Station | LAN access and security |
| Reassociation | Distribution system | MSDU delivery |

### Distribution of messages within a DS

*   **Distribution**
    *   Exchange MPDUs between two BSS
*   **Integration**
    *   Data transfer between a Wi-Fi station and an LAN station on an integrated IEEE 802x LAN

### Associated-Related Services

*   Transition types, based on mobility:
    *   No transition
        *   Move only within a single BSS
    *   BSS transition
        *   Move between two BSS
    *   ESS transition
        *   Move from a BSS in one ESS to a BSS within another ESS

#### Distribution Service

*   Association
    *   Establishes an initial association between a station and an AP
*   Reassociation
    *   Enables an established association to be transferred from one AP to another
*   Disassociation
    *   A notification from either a station or an AP that an existing association is terminated

# **24.4  IEEE 802.11i Wireless LAN Security**

*   Wired Equivalent Privacy (WEP) algorithm
    *   802.11 privacy
*   Wi-Fi Protected Access (WPA)
    *   Set of security mechanisms: eliminates most 802.11 security issues
    *   Based on the current state of the 802.11i standard
*   Robust Security Network (RSN)
    *   Final form of the 802.11i standard
*   Wi-Fi Alliance certifies vendors in compliance with the full 802.11i (WPA2)

## IEEE 802.11i Services

The 802.11i RSN security specification defines the following services:

*   **Authentication:**A protocol is used to define an exchange between a user and an AS (authentication server)
    *   provides mutual authentication and generates temporary keys to be used between the client and the AP over the wireless link.
*   **Access control:** authentication
    *   routes the messages properly, and facilitates key exchange. It can work with a variety of authentication protocols.
*   **Privacy with message integrity:** MAC-level data (e.g., an LLC PDU) are encrypted along with a message integrity code that ensures that the data have not been altered.



Figure 24.6a indicates the security protocols used to support these services

![](https://t3764800.p.clickup-attachments.com/t3764800/c0062e08-2a8a-4e84-bac0-aeea261665c4/Screen%20Shot%202023-11-12%20at%205.01.28%20PM.png)Figure 24.6b lists the cryptographic algorithms used for these services

![](https://t3764800.p.clickup-attachments.com/t3764800/ccb0c936-19bf-4be6-8497-0960fc391400/Screen%20Shot%202023-11-12%20at%205.01.58%20PM.png)

## IEEE 802.11i Phases of Operation

IEEE 802.11i security is concerned only with secure communication between the STA and its AP

five distinct phases of IEEE 802.11i RSN:

*   Two wireless stations in the same BSS communicating via the access point for that BSS. (在同一 BSS 中的兩個無線電台通過該 BSS 的接入點進行通信)
    *   secure communication is assured if each STA establishes secure communications with the AP.
*   Two wireless stations (STAs) in the same ad hoc IBSS communicating directly with each other. (在同一 ad hoc IBSS 中的兩個無線電台（STA）直接相互通信)
    *   with the AP functionality residing in the STA.
*   **Two wireless stations in different BSSs communicating via their respective APs across a distribution system. (**不同 BSS 中的兩個無線電台通過各自的 AP 跨分發系統進行通信**)**
    *   distribution system at the level of IEEE 802.11, but only within each BSS. End-to-end security (if required) must be provided at a higher layer
*   **A wireless station communicating with an end station on a wired network via its AP and the distribution system. (**無線電台通過其 AP 和 DS 與有線網絡上的終端站通信**)**
    *   security is only provided between the STA and its AP

![](https://t3764800.p.clickup-attachments.com/t3764800/e6d3f720-97a5-4303-bf92-9b3bb40feb89/Screen%20Shot%202023-11-12%20at%205.04.51%20PM.png)

### Five Phases of Operation for an RSN

Sure, here is a summary of each key point of the listed paragraph:

**Discovery**

*   APs advertise their security policies using Beacons and Probe Responses.
*   STAs use this information to select an AP to associate with.
*   The AP and STA agree on a cipher suite and authentication mechanism.

**Authentication**

*   The STA and AS prove their identities to each other.
*   Non-authentication traffic is blocked until authentication is successful.
*   The AP does not participate in the authentication transaction other than forwarding traffic.

**Key Management**

*   Cryptographic keys are generated and placed on the AP and STA.
*   Frames are exchanged only between the AP and STA.

**Protected data transfer**

*   Frames are exchanged between the STA and end station through the AP.
*   Secure data transfer occurs only between the STA and AP; security is not provided end-to-end.

**Connection termination**

*   The AP and STA exchange frames to tear down the secure connection.
*   The connection is restored to its original state.

![](https://t3764800.p.clickup-attachments.com/t3764800/383aa7a1-608c-4ed5-9322-769ec03b29be/Screen%20Shot%202023-11-12%20at%205.13.30%20PM.png)

## Discovery Phase

*   STA and an AP to recognize each other

### Security capabilities

*   STA and AP decide on specific techniques in the following areas
    *   Confidentiality and MPDU integrity protocols (only unicast)
    *   Authentication method
    *   Cryptography key
        *   management approach
*   protecting multicast/broadcast traffic are dictated by the AP
    *   Cipher suite (Confidentiality/integrity)
        *   WEP, TKIP, CCMP, vendor- specific
        *   AKM: Authentication and Key Management
        *   IEEE 802.1x, pre-shared key, vendor-specific

### MPDU Exchange

**Network and security capability discovery:**

*   STAs discover the existence of a network with which to communicate.
*   APs broadcast their security capabilities through Beacon frames or Probe Response frames.
*   Wireless stations can discover available access points by passively monitoring Beacon frames or actively probing every channel.

**Open system authentication:**

*   This frame sequence provides no security but maintains backward compatibility with existing IEEE 802.11 hardware.
*   The STA and AP simply exchange identifiers.

**Association:**

*   The STA and AP agree on a set of security capabilities to be used.
*   The STA sends an Association Request frame to the AP, specifying one set of matching capabilities.
*   If there is no match in capabilities, the AP refuses the Association Request.
*   The STA blocks it too, in case it has associated with a rogue AP or someone is inserting frames illicitly on its channel.

![](https://t3764800.p.clickup-attachments.com/t3764800/8c3e7698-1da6-4ed6-9d2d-2e22af037f4f/Screen%20Shot%202023-11-12%20at%205.22.28%20PM.png)



## Authentication Phase

*   IEEE 802.11X AC
    *   802.1X Control channel is unblocked
    *   802.11 data channel is blocked
*   Three phases
    *   Connect to AS
        *   The STA sends a request to its AP
    *   EAP exchange
        *   exchange authenticates the STA and AS to each other
    *   Secure key delivery
        *   Once authentication is established, the AS generates a master session key (MSK), also known as the Authentication, Authorization, and Accounting (AAA) key, and sends it to the STA.

![](https://t3764800.p.clickup-attachments.com/t3764800/04625534-f97f-476e-8d68-079b46669763/Screen%20Shot%202023-11-12%20at%205.21.49%20PM.png)

### EAP Authentication Protocol

*   An Authentication framework, but not a specific mechanism
    *   Providing some common functions
    *   Negotiating authentication methods: EAP methods (more than 40)
*   Important notes
    *   EAP authentication is initiated by the server (authenticator)
    *   Authentication is mutual between the client and authentication server

![](https://t3764800.p.clickup-attachments.com/t3764800/5fd804d6-e763-4684-8a21-2418d03b5a68/Screen%20Shot%202023-11-12%20at%205.28.55%20PM.png)

### Popular EAP Methods

*   Cisco LEAP (Lightweight EAP)
    *   A proprietary method developed by Cisco
    *   User credentials are not strongly protected: _complex passwords are required_
*   EAP-FAST (EAP-Flexible Authentication via Secure Tunneling)
    *   A replacement for LEAP, but non-proprietary
    *   _No need of strong password or any certificate_
    *   Using a PAC (Protected Access Credential) to establish a TLS tunnel
*   EAP-TLS (EAP-Transport Layer Security)
    *   (RFC 5216) original, standard wireless LAN EAP authentication protocol
    *   Using PKI: both client and AS need a certificate (X.509 certificates)
    *   One of the most secure EAP standards available
    *   Universally supported by all manufacturers of wireless LAN hardware/software
*   PEAP (Protected EAP)
    *   Encapsulating EAP within a potentially encrypted and authenticated TLS tunnel
    *   Only the server authentication is performed using PKI certificate
    *   Client is authenticated using either EAP-GTC or EAP-MSCHAPv2 within the tunnel
        *   AP-GTC (Generic Token Card)
        *   EAP-MSCHAPv2 (Microsoft’s Challenge Handshake Authentication Protocol)

![](https://t3764800.p.clickup-attachments.com/t3764800/075f6a62-f99a-49e2-ba01-abd2f2c813eb/Screen%20Shot%202023-11-12%20at%205.32.36%20PM.png)

## Key Management Phase

*   Pairwise keys: for communication between an STA and an AP
    *   Pre-shared key (PSK)
    *   Master session key (MSK)
    *   Pairwise master key (PMK)
        *   PSK or derived from MSK
    *   Pairwise transient key (PTK)
*   Group keys: for multicast communication
    *   Group master key (GMK)
    *   Group temporal key (GTK)

![](https://t3764800.p.clickup-attachments.com/t3764800/6c3ea04e-204a-4dae-9119-1f1ef92f886d/Screen%20Shot%202023-11-12%20at%205.34.32%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/236c50cf-5f54-4eaa-a84a-0c8111301d91/Screen%20Shot%202023-11-12%20at%205.34.40%20PM.png)

### **4-way handshake**

*   **AP ➝ STA:** Message includes the MAC address of the AP and a nonce (Anonce)
*   **STA ➝AP:** The STA generates its own nonce (Snonce) and uses both nonces and both MAC addresses, plus the PMK, to generate a PTK. The STA then sends a message containing its MAC address and Snonce, enabling the AP to generate the same PTK. This message includes a message integrity code (MIC)2 using HMAC-MD5 or HMAC-SHA-1-128. The key used with the MIC is KCK.
*   **AP ➝ STA:** The AP is now able to generate the PTK. The AP then sends a message to the STA, containing the same information as in the first message, but this time including a MIC.
*   **STA ➝ AP:** This is merely an acknowledgment message, again protected by a MIC.

![](https://t3764800.p.clickup-attachments.com/t3764800/c85514b9-3056-406d-b544-6f5664e1743f/Screen%20Shot%202023-11-12%20at%205.36.58%20PM.png)

###   

## Protected Data Transfer Phase

*   Temporal Key Integrity Protocol (TKIP)
    *   Only software changes are required to old WEP
    *   Message integrity
        *   Message Integrity Code (MIC): by an algorithm, called Michael
        *   64-bit: source/destination MAC addresses + data field + key material
    *   Data confidentiality
        *   Encrypting MPDU + MIC using RC4
    *   256-bit TK
        *   Two 64-bit keys for MIC: one key for each direction
        *   128 bits: generate the RC4 key for encryption
    *   TKIP sequence counter (TSC): monotonically increasing
        *   Included with each MPCU and protected by MIC➔against replay attack
        *   Combined with session TK➔dynamic encryption key
*   Counter Mode-CBC MAC Protocol (CCMP)
    *   Hardware support is needed
    *   Message integrity
        *   Cipher block chaining message authentication code (CBC-MAC)
    *   Data confidentiality
        *   CTR block cipher mode of operation with AES
    *   Same 128-bit AES key for both
    *   A 48-bit packet number: a nonce to prevent replay attacks

## The IEEE 802.11i Pseudorandom Function

*   A pseudorandom bit stream: HMAC-SHA-1
    *   A message and a key (at least 160 bits)➔160-bit hash value
*   SHA-1 property: change of a single bit➔a new hash value with no apparent connection



PTK = PRF(PMK, “Pairwise key expansion,” min(AP-Addr, STA-Addr) } ||

max (AP-Addr, STA-Addr) || min(Anonce, Snonce) || max(Anonce, Snonce), 384)

> _K_ \= PMK
>
> _A_ \= the text string “Pairwise key expansion”
>
> _B_ \= a sequence of bytes formed by concatenating the two MAC addresses and the two nonces
>
> _Len_ \= 384 bits
>
> Similarly, a nonce is generated by
>
> Nonce = PRF(Random Number, “Init Counter,” MAC } Time, 256)

GTK = PRF(GMK, _“_Group key expansion,” MAC || Gnonce, 256)



![](https://t3764800.p.clickup-attachments.com/t3764800/3539fa9c-0f8c-4c61-82ad-126b24cae8b7/Screen%20Shot%202023-11-12%20at%205.40.09%20PM.png)





# **24.5  Key Terms, Review Questions, and Problems**

**24.1 What is the basic building block of an 802.11 WLAN?**

The basic building block of an 802.11 WLAN is the Basic Service Set (BSS). A BSS is a wireless network that consists of two or more stations that communicate directly with each other without the need for an access point (AP). Ad hoc



**24.2 Define an extended service set.**

An Extended Service Set (ESS) is a collection of two or more BSSs that are interconnected by a distribution system. This allows stations to roam freely between different BSSs within the ESS, as if they were all part of a single logical LAN.



**24.3 List and briefly define IEEE 802.11 services.**

The IEEE 802.11 standard defines a number of services, including:

*   **Data:** This service provides for the transfer of data frames between stations.
*   **Management:** This service provides for the exchange of management frames, which are used to control and manage the BSS.
*   **Control:** This service provides for the exchange of control frames, which are used to coordinate the transmission of data frames.



**24.4 Which assumptions form the basis of security policy for mobile devices?**

The following assumptions form the basis of security policy for mobile devices:

*   **Mobile devices are often outside the organization's control.**
*   **Mobile devices may be used on untrusted networks.**
*   **Mobile devices may be used to access untrusted content.**
*   **Mobile devices may be infected with malware.**



**24.5 List the seven major security concerns for mobile devices.**

The seven major security concerns for mobile devices are:

*   **Theft and tampering:** Mobile devices are often outside the organization's control and may be stolen or tampered with.
*   **Unauthorized access:** Mobile devices may be accessed by unauthorized users.
*   **Data loss:** Mobile devices may be lost or damaged, resulting in the loss of data.
*   **Malware:** Mobile devices may be infected with malware, which can steal data, compromise systems, or disrupt operations.
*   **Network attacks:** Mobile devices may be attacked when they are connected to untrusted networks.
*   **Content security:** Mobile devices may be used to access untrusted content, such as malicious websites or apps.
*   **Physical security:** Mobile devices may be lost or damaged due to physical accidents.



**24.6 Briefly describe the pseudorandom stream generation of the IEEE 802.11i scheme and list some uses of the pseudorandom function.**

The pseudorandom stream generation of the IEEE 802.11i scheme is based on the Counter Mode with Cipher Block Chaining Message Authentication Code (CCM) algorithm. The CCM algorithm uses a pseudorandom function (PRF) to generate a keystream, which is then used to encrypt and authenticate data frames. The PRF is also used to generate other cryptographic keys, such as the pairwise master key (PMK) and the transient key (TK).



**24.7 Briefly describe the four IEEE 802.11i phases of operation.**

The four IEEE 802.11i phases of operation are:

*   **Discovery:** The STA discovers the existence of a network with which to communicate.
*   **Authentication:** The STA and AP prove their identities to each other.
*   **Key Management:** The AP and STA perform several operations that cause cryptographic keys to be generated and placed on the AP and STA.
*   **Protected data transfer:** Frames are exchanged between the STA and the end station through the AP.
*   **Connection termination**



**24.8 What is the difference between TKIP and CCMP?**

TKIP (Temporal Key Integrity Protocol) and CCMP (Counter Mode with Cipher Block Chaining Message Authentication Code) are two encryption algorithms used in IEEE 802.11i. TKIP is a legacy algorithm that is less secure than CCMP. CCMP is the preferred algorithm for new deployments.
