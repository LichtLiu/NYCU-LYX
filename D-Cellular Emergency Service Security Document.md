---
title: "Computer Security Principles and Practice"
permalink: /Computer-Security-Principles-and-Practice/D-Cellular-Emergency-Service-Security-Document/
layout: default
---
# D-Cellular Emergency Service Security Document

[https://youtu.be/zUSBRX\_JBVw?si=imSTFxY9VxIsFisb&t=4697](https://youtu.be/zUSBRX_JBVw?si=imSTFxY9VxIsFisb&t=4697)

# Cellular Emergency Services (911)

*   Emergency services are a vital lifeline to people in emergency conditions.
*   The globally-deployed cellular networks with ubiquitous coverage have been the most accessible channel to emergency users.

# Cellular Emergency Service Practice

*   To ensure the availability of cellular emergency services,
    *   In the U.S., Federal Communications Commission (FCC) stipulates that cellular carriers must transmit all wireless 911 calls without respect to their call validation process to a Public Safety Answering Point (PSAP).
    *   The GSM Association (GSMA) standard requires emergency services must be supported by all mobile phones even without SIM cards and be free of charge for mobile users.
    *   The 3GPP standard requires emergency services to be provided with higher priority than other cellular services.

# Priori Arts

*   Priori arts corresponding to the cellular emergency services mainly focus on:
    *   Denial-of-service (DoS) attacks against PSAPs
    *   Vulnerabilities on the UE side
*   However, the security of the cellular infrastructure supporting emergency services still remains unexplored
    *   In this work, we mainly study the insecurity of cellular emergency service infrastructure

# Our Findings

*   We found that U.S. cellular emergency services are deniable and abusable.
    *   Four insecure designs from 3GPP cellular emergency service standards were discovered.
    *   By exploiting them, not only emergency service calls can be blocked/denied, but also a variety of attacks can be launched against either mobile users or cellular infrastructure.







# 5G/4G: Network Architecture

*   5G/4G emergency services are VoIP-based ones using Session Initiation Protocol (SIP), which is mandated by IMS (IP Multimedia Subsystem)
    *   The IMS server is responsible for emergency service signaling and data traffic
    *   An emergency service request from the UE in turn traverses radio access network, core network, IMS, and PSAPs.
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/b16907ad-2a01-43bd-bbd3-2e164bf20e97/image.png)



# IMS Emergency Service Flow

*   (1) Emergency IP-CAN Session Establishment allows the UE to obtain the **emergency IP connectivity** to communicate with the IMS server.
*   (2) IMS Emergency Registration establishes a **secure communication** between the UE and the IMS server through **IPSec**.
*   (3) IMS Emergency Session Establishment allows an emergency UE to establish an IMS emergency call/text session with the PSAP through the IMS server.
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/3e4c54bf-ae2c-4070-8458-d7d561c2b547/image.png)



# Experimental Methodology

*   Two kinds of emergency UEs (i.e., COTS and SDR ones) and three U.S. major carriers (i.e., OP-I, OP-II, and OP-III) were tested.



*   All experiments were conducted in a responsive manner
    *   In all the experiments, NO emergency calls/text messages were sent to operational IMS servers or PSAPs



# Discovered Vulnerabilities and Attacks -Denial of Cellular Emergency Service

*   Vulnerabilities and attacks
    *   V1: Unverifiable emergency IP-CAN session requests
    *   V2: Improper cross-layer security binding
    *   Devised attacks: UE detaching, call cancel, call drop
*   According to FCC Title 47, U.S. carriers need to support non-service- initialized devices (denoted anonymous UE thereafter) to access emergency services.
    *   Only one emergency IP-CAN session can be established per UE.
*   The network cannot differentiate whether the second IP-CAN session establishment request is sent by a benign user or an attacker.

# V1: Unverifiable Emergency IP-CAN Session Requests

*   We conducted this experiment with all the three carriers:
*   OP-I: Accept the duplicate request but interrupt the ongoing emergency IP-CAN session
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/940522ce-ba47-4f7d-918b-2964255a3f4a/image.png)
*   OP-II and OP-III: Accept the duplicate request and keep both sessions



# Denial of Cellular Emergency Service

*   Vulnerabilities and attacks
    *   V1: Unverifiable emergency IP-CAN session requests
    *   V2: Improper cross-layer security binding
    *   Proof-of-concept attacks: UE detaching, call cancel, call drop
*   Secure communication between UE and IMS server rely on IPSec.
*   However, the IPSec ciphering and integrity keys are derived from the IMS emergency registration (SIP registration)
    *   The network-layer security (i.e., IPSec) is unnecessarily bound to the application-layer security (i.e., SIP layer security)
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/7700dcfa-5c46-4ba2-a957-ecb305c68b88/image.png)
    > What if IMS emergency registration can be skipped?

# V2: Improper Cross-layer Security Binding

*   We validate this vulnerability using anonymous UEs and make two observations:
    *   The IMS emergency registration procedure is NOT performed by UEs.
    *   The SIP INVITE messages are all sent in plain-text without confidentiality and integrity protection.
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/0e649cbe-ce5b-4e2e-8577-fcb5e8bb25b8/image.png)

# Denial of Cellular Emergency Service (DoCES) Attacks

*   Vulnerabilities and attacks
*   V1: Unverifiable emergency IP-CAN session requests
*   V2: Improper cross-layer security binding
*   Proof-of-concept attacks: UE detaching , call cancel, call drop
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/8f80e02d-de14-4bc1-8ea1-f5132da17443/image.png)



*   Phase I: Obtained IP connectivity, and call is not dialed
    *   UE detaching
        *   By sending duplicate attach (exploiting V1)
*   Phase II: Call is dialed but not answered by PSAP yet
    *   Call cancel
        *   By sending fake SIP CANCEL (exploiting V2)
*   Phase III: Call is dialed and answered
    *   Call drop
        *   By sending fake SIP BYE (exploiting V2)
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/3b471943-bf57-4f87-bb8a-2d560f5d6a59/image.png)



# Discovered Vulnerabilities and Attacks

# Hijacking Emergency IP-CAN Sessions

\-for free services, DoS, overcharging, remote scanning attacks

# ![](https://t3764800.p.clickup-attachments.com/t3764800/39378b38-bc22-41e6-928a-5bc34be74410/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/9ceed258-dbeb-4d15-a59a-2d0d28d2a7bd/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/239aa574-a462-441a-aafd-d408ea57e120/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/b3fc1fb1-196a-4a50-b12f-d0f375ed2b84/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/3702e4cb-f188-44fb-bdd8-f55826192cfd/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/49fdef89-a0a6-4f22-ac98-67922e4ecea7/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/3fcbacc3-a8bd-4f3b-b5bd-9308da54622f/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/b6671336-739c-484f-8cd9-7f73cf3ad201/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/684802f5-3763-4895-89c2-f1fd4f3a049c/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/f72e63f5-a850-4d4e-9055-a3cd087a64ec/image.png)
