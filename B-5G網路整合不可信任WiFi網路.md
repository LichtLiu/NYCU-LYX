---
title: "Computer Security Principles and Practice"
permalink: /Computer-Security-Principles-and-Practice/B-5G網路整合不可信任WiFi網路/
layout: default
---
# B-5G網路整合不可信任WiFi網路

[https://www.youtube.com/watch?v=zUSBRX\_JBVw&t=7s](https://www.youtube.com/watch?v=zUSBRX_JBVw&t=7s)

# Non-3GPP access networks

*   Untrusted non-3GPP access networks
    *   e.g., UE connects to the 5G core via public WiFi and Internet
*   Trusted non-3GPP access networks
    *   e.g., UE connects to the CHT WiFi AP



## Trusted and Untrusted Non-3GPP Access

*   A non-3GPP access network shall be connected to 5G core network via
    *   Untrusted: Non-3GPP InterWorking Function (N3IWF)
        *   access network is considered **untrusted**
        *   It acts as a gateway and security barrier between the untrusted network and the 5G core network.
        *   security checks, data transformation, and protocol conversion to ensure secure and seamless communication
    *   Trusted: Trusted Non-3GPP Gateway Function (TNGF)
        *   access network is considered **trusted**
        *   provides a more direct and efficient connection between the non-3GPP network and the 5G core network.
        *   less strict constraints compared to the N3IWF(security checks and protocol conversion)
*   Both N3IWF and TNGF interface with 5G Core Network CP and UP functions via N2 and N3 interfaces, respectively
    *   **N2 interface****:** Connects to the Control Plane (CP) functions of the 5G core network, handling signaling and control messages.
    *   **N3 interface****:** Connects to the User Plane (UP) functions of the 5G core network, handling data traffic.
*   A Non-3GPP access network may advertise(通知) the Public Land Mobile Networks (PLMNs) for which it supports trusted connectivity and the type of supported trusted connectivity (e.g., 5G connectivity)
    *   helps mobile devices choose the appropriate connection path depending on the available networks and security requirements.
    *   **the choice between N3IWF and TNGF depends on the level of trust placed on the non-3GPP access network**
        *   Trusted networks: faster and more efficient connections
        *   untrusted networks: stricter security measures
*   When UE decides to use untrusted non-3GPP access
    *   Selects and connects with a non-3GPP access network
    *   Selects a PLMN and an N3IWF in this PLMN
*   When UE decides to use trusted non-3GPP access
    *   Selects a PLMN
    *   Selects a non-3GPP access network (a TNAN) that supports trusted connectivity to the selected PLMN
*   A UE shall establish an IPsec tunnel with the N3IWF or with the TNGF to register with the 5G Core Network over non-3GPP access



> PLMN 是指由政府或其批准的運營商為公眾提供陸地移動通信業務而建立、經營的網路。PLMN 由 MCC 和 MNC 兩個部分組成  
> **MCC：移動國家代碼 (Mobile Country Code)**。MCC 由三個數字組成，用於識別不同的國家或地區。例如，中國的 MCC 是 460。  
> **MNC：移動網絡代碼 (Mobile Network Code)**。MNC 由兩個或三個數字組成，用於識別不同的移動網絡營運商。例如，中國移動的 MNC 是 00，中國聯通的 MNC 是 01，中國電信的 MNC 是 02。

# Untrusted Non-3GPP Access Network with 5G Core

*   Non-3GPP interworking function (N3IWF)
    *   Interworking of untrusted non-3GPP networks and 5G core
    *   Acting as a gateway for the 5G core with support for N2 and N3 interfaces
    *   Secure IPsec connection over non-3GPP access network between UE and N3IWF
*   Why is needed?
    *   Using untrusted WLANs, which are not controlled by operator
    *   Including public hotspots, home Wi-Fi, corporate Wi-Fi, etc.

## Benefits

*   Can supplement the 3GPP access networks for
    *   Avoiding data congestion and reducing backhaul costs with increased capacity
    *   Providing better coverage and connectivity in high-density/indoor environments
    *   Enabling new business opportunities with value added services
    *   Reducing operator capital and operational costs with unified management
    *   Delivering enhanced services to customer in a cost-efficient manner

## Evolution of Architecture: Prior to 5G

## ![](https://t3764800.p.clickup-attachments.com/t3764800/db4ed60b-1a52-452d-a080-e8d8f106e10e/image.png)

## Architecture in 5G

![](https://t3764800.p.clickup-attachments.com/t3764800/c3b1c994-409f-4062-9954-d87062b9a5c5/image.png)

## 3GPP Access & 5G Core

### ![](https://t3764800.p.clickup-attachments.com/t3764800/dc10cfda-3d1c-4000-9ed2-32cfc79b5eac/image.png)

## Protocol Stacks

*   Control plane (CP) protocol stacks
    *   Involving UE, WLAN, N3IWF, and AMF
    *   Initial registration and authentication
    *   NAS mobility and session management
    *   Establishing UP between N3IWF and UE
*   User plane (UP) protocol stack
    *   Involving UE, WLAN, N3IWF, and UPF
    *   Transferring the UP traffic between UE and data network
    *   IPsec tunnel mode is employed to protect the data transfer

### Protocol Stack for Initial Registration and Auth.

*   Control plane before signaling IPsec SA
    *   Selecting N3IWF and initiating IKEv2 SA establishment procedure
    *   N3IWF starts the EAP-5G procedure with UE
    *   UE initiates registration and authentication procedure using NAS protocol with AMF
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/91bd7382-eef5-4c92-b33e-9aaa92dca4df/image.png)

### Protocol Stack for NAS Mobility and Session Mgmt.

*   Control plane after signaling IPsec SA
    *   A signaling IPsec SA is established between UE and N3IWF
    *   A TCP connection is further established for transport of NAS mobility and session mgmt.
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/39656278-1cb6-4f23-8f90-36aa42bb5393/image.png)

### Protocol Stack for Establishing User Plane

*   User plane establishment via N3IWF
    *   N3IWF initiates the establishment of the IPsec child SAs with UE using IKEv2
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/447bbf55-79ab-40eb-b091-9acc7f13d069/image.png)

### Protocol Stack for User Plane

*   User plane protocol stack
    *   Transferring UP traffic between UE and data network
    *   IPsec tunnel mode is employed for the established child SAs to protect the data transfer
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/bfe8dacf-293d-43eb-a8c4-44811fbffd65/image.png)

## Control Plane Procedures

*   Access network discovery and selection
    *   Using ANDSP (Access Network Discovery and Selection Policy)
    *   ANDSP consists of WLAN Selection Policy (WLANSP) and non-3GPP access network node (N3AN) configuration information
        *   N3AN info for selecting a N3IWF
    *   Registration and authentication
    *   PDU session establishment
        *   Protocol Data Unit 通信協議中用於傳輸數據的基本單位
        *   **在物理層中，PDU 可以是 1 位、2 位、4 位等。**
        *   **在資料鏈路層中，PDU 可以是 Ethernet 幀、PPP 幀等。**
        *   **在網路層中，PDU 可以是 IP 數據包、IPv6 數據包等。**
        *   **在傳輸層中，PDU 可以是 TCP 數據段、UDP 數據段等。**

### Authentication for Untrusted Non-3GPP Access

*   Vendor-specific EAP method “EAP-5G” ➝ Authentication
    *   **primary authentication mechanism** **Between UE and N3IWF as a security gateway**
    *   for encapsulating NAS(Network Access Server) messages exchanged between the UE and the N3IWF.
    > Extensible Authentication Protocol (EAP)
*   If the UE needs to authenticated by the 3GPP home network
    *   5G-AKA or EAP-AKA’ can be used
    > 5G-AKA (5G Authentication Key Agreement)
    >
    > EAP-AKA' (Extensible Authentication Protocol - Authentication and Key Agreement')
*   The UE shall be authenticated by reusing the existing UE NAS security context in AMF

> Authentication Management Function (AMF)

# Three major technologies in non-3GPP authentication

*   [IKEv2 (Internet Key Exchange)](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-5038?block=block-e1a75801-67e7-479f-8263-b9aa9e5911e1)
    *   Performing mutual authentication between two parties
    *   Establishing an IKE security association (SA) including shared secret for IPsec
    *   IKEv2 是 Internet Key Exchange 版本 2 的縮寫，它是一種安全協議，用於在 IP 安全 (IPsec) 隧道中建立和維護安全關聯 (SA)。IKEv2 是一種雙向協議，可用於兩個實體之間建立安全連接。
*   [EAP (Extensible Authentication Protocol)](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-5038?block=block-f33578f0-4a60-4508-9efd-353f281ae4cd)
    *   Providing a secure way to send identifying information to provide network authentication
*   [IPsec (Internet Protocol Security)](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-5038?block=block-3eaa1fae-b35c-4f70-8db6-53c5dcf1e7f0)
    *   Protecting communications over IP networks



## How does IKEv2 Work?

IKEv2 的工作原理如下：

1. 協商：IKEv2 協議由兩個階段組成：第一階段協商和第二階段協商。在第一階段協商中，兩個實體建立安全通道並交換密鑰。在第二階段協商中，兩個實體建立 IPsec SA。
2. 安全關聯：安全關聯是 IKEv2 協議中的主要概念。安全關聯定義了兩個實體之間的安全配置，包括加密算法、身份驗證方法和密鑰。
3. 身份驗證：IKEv2 使用多種身份驗證方法，包括預共享密鑰 (PSK)、數位憑證和 X.509 憑證。
4. 加密：IKEv2 使用多種加密算法，包括 AES、3DES 和 ChaCha20/Poly1305。

## ![](https://t3764800.p.clickup-attachments.com/t3764800/afe998df-9dcf-4bd1-be16-4adb5ec6d715/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/5ba755d4-6d9d-45e7-aea4-6d5352ef7280/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/ab4658fe-e0a7-488e-83a3-02ddad5ea566/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/b97df5d6-b17e-4186-898d-c8b040fbd3fc/image.png)

### IKEv2 Authentication with EAP Method

*   In addition to authentication using public key signatures and shared secrets, IKE supports EAP
*   Extensible Authentication is implemented in IKE as additional IKE\_AUTH exchanges that MUST be completed to initialize IKE\_SA
    *   These exchanges carry EAP messages between the initiator and responder to complete the chosen EAP method's authentication process.
*   For EAP methods that create a shared key as a side effect of authentication, that shared key MUST be used by both initiator and responder to generate AUTH payloads

## EAP Authentication Protocol

*   An Authentication framework, but not a specific mechanism
    *   Providing some common functions
    *   Negotiating authentication methods: EAP methods (more than 40)
*   Important notes
    *   EAP authentication is initiated by the server (authenticator)
    *   Authentication is mutual between the client and authentication server
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/bc4125d4-3315-45fe-b33a-d5ed87034183/image.png)

> Some materials from [http://what-when-how.com/ccnp-ont-exam-certification-guide/802-1x-and-eap-authentication-protocols/](http://what-when-how.com/ccnp-ont-exam-certification-guide/802-1x-and-eap-authentication-protocols/)

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
    *   Using PKI: both client and AS need a certificate (X.509 certificates)（兩方都有certificate)
    *   One of the most secure EAP standards available
    *   Universally supported by all manufacturers of wireless LAN hardware/software
*   PEAP (Protected EAP)
    *   Encapsulating EAP within a potentially encrypted and authenticated TLS tunnel
    *   Only the server authentication is performed using PKI certificate
    *   Client is authenticated using either EAP-GTC or EAP-MSCHAPv2 within the tunnel
        *   EAP-GTC (Generic Token Card)
        *   EAP-MSCHAPv2 (Microsoft’s Challenge Handshake Authentication Protocol)

### PEAP

PEAP 的工作原理如下：

1. 用戶端向接入點發送身份驗證請求。
2. 接入點使用 PEAP 隧道將身份驗證請求發送到認證伺服器。
3. 認證伺服器使用 EAP 方法對用戶進行身份驗證。
4. 認證伺服器向接入點發送身份驗證結果。
5. 接入點將身份驗證結果發送給用戶端。



![](https://t3764800.p.clickup-attachments.com/t3764800/0dee878d-9ade-4b27-bac7-75e435221b88/image.png)

### EAP-5G



*   In non-3GPP registration, EAP-5G is adopted for authentication with some minor changes
    *   e.g., N3IWF does not send EAP-Identity request since UE includes its identity in the first IKE\_AUTH
*   EAP-5G is utilized only to encapsulate NAS messages, but not to authentication UE
*   N3IWF and UE exchange EAP-5G messages within IKE\_AUTH

![](https://t3764800.p.clickup-attachments.com/t3764800/f432a10d-88d3-4bed-bddf-739869a73f67/image.png)

### NAS Messages

*   NAS (Non-Access Stratum), a functional layer supporting traffic and signaling messages between CN and UE
*   Two message types: 5GMM (Mobility Management) and 5GSM (Session Management)
    *   5GMM: supporting mobility of UE including procedures like authentication, identification, UE configuration update, and security mode control
        *   Interactions between UE and AMF
    *   5GSM: supporting session management to establish and maintain data connectivity between UE and data network
        *   Interactions between UE and SMF through AMF

### 5G-NAS over EAP

![](https://t3764800.p.clickup-attachments.com/t3764800/8d4aec34-6627-4324-93ea-b7a51faf5f30/image.png)

## IPsec

*   Two main functions
    *   Encapsulating Security Payload (ESP): a combined authentication/encryption function
    *   A key exchange function: Internet Key Exchange standard (IKEv2)
*   VPN: both authentication and encryption are generally desired
*   Authentication Header (AH): authentication-only function (deprecated)

### Security Associations

*   A key concept of IPsec
    *   One-way relationship between a sender and a receiver
    *   Two-way secure exchange: two SAs are required
*   Uniquely identified by three parameters
    *   Security parameter index (SPI) (辨識封包是哪個security association)
    *   IP destination address
    *   Protocol identifier: AH or ESP
*   Characterized by the following parameters
    *   Sequence number counter: 32-bit
    *   Sequence counter overflow: A flag➔whether overflow➔an auditable event
    *   Anti-replay window: defining a sliding window (prevent replay attack)
    *   AH information
        *   Algorithm, keys, key lifetimes, etc.
    *   ESP information
        *   Algorithm, keys, init values, key lifetimes, etc.
    *   Lifetime of this security association
    *   IPSec protocol mode: tunnel or transport
    *   Path MTU

### Two IPsec Operation Modes

*   Transport and Tunnel modes
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/d03b84a7-3dab-4a0b-8b8f-b2f1efe2e478/image.png)

### Encapsulating Security Payload

*   Providing authentication and confidentiality services

### ![](https://t3764800.p.clickup-attachments.com/t3764800/6e9fbc81-db4e-46f1-90eb-2f7bb82b4256/image.png)

### Transport and Tunnel Modes



Transport Mode

*   Protection: the payload of an IP packet
*   Typically used for end-to-end communication between two hosts
*   ESP protects the IP payload but not the IP header



Tunnel Mode

*   Protection: the entire IP packet
*   Entire original packet travels through a tunnel from one point to another
*   Used when one or both ends of a security association are a security gateway
*   Hosts on networks behind firewalls may engage in secure communications without implementing IPsec



### IPsec: AH + ESP

*   IP AH only
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/0f9e09db-3fb1-459f-b9d9-294832c76a45/image.png)
*   IP AH + ESP
    *   Transport mode
        *   ![](https://t3764800.p.clickup-attachments.com/t3764800/843e29b2-b85b-4ed8-8897-e672b22e88f3/image.png)
    *   Tunnel mode
        *   ![](https://t3764800.p.clickup-attachments.com/t3764800/2425a415-71f9-45c3-a265-22edf1ad52de/image.png)



## Authentication Procedure for Untrusted Non-3GPP

*   Goal
    *   Enabling mutual authentication between UE and network
    *   Providing key materials that can be used between UE and network in subsequent procedures
*   Using EAP framework
    *   SEAF @ AMF: pass-through authenticator
    *   AUSF: authentication server

![](https://t3764800.p.clickup-attachments.com/t3764800/5674e051-20aa-4551-a717-9d8130e748f6/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/a86c6aed-6624-4637-a2c2-16792a0306eb/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/7ba1508d-5ebb-4d4d-968b-35e88c4be7b0/image.png)

### 5G Authentication Initialization

### ![](https://t3764800.p.clickup-attachments.com/t3764800/6b1b12a3-9d20-4b9c-b90a-b418d93002a0/image.png)

### 5G AKA

### ![](https://t3764800.p.clickup-attachments.com/t3764800/dc40a3fe-4fdb-4880-9c07-240d67d22575/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/49a93566-e750-48f9-b17f-535340452782/image.png)

### NAS Security Mode Command Procedure

![](https://t3764800.p.clickup-attachments.com/t3764800/1cccde45-18e7-4c59-bc3e-edb2f502402d/image.png)

### EAP-AKA’

### ![](https://t3764800.p.clickup-attachments.com/t3764800/50aa8e8c-f4fb-4449-9cb2-476d5f395c06/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/6233b75d-b7f4-4efa-921a-23a440da20b4/image.png)

### Difference between EAP-AKA’ and 5G-AKA

*   Role of the SEAF
    *   EAP-AKA’: transparently forwarding EAP messages
        *   EAP message exchanges are between UE and AUSF through SEAF
    *   5G-AKA: also verifying authentication response from UE
        *   May take action if the verification fails
*   Key derivation
    *   EAP-AKA’: AUSF drives KAUSF itself
    *   5G-AKA: KAUSF is computed by UDM/ARPF and sent to AUSF

### Key Hierarchy in 5G

*   Suitable for both 3GPP and non-3GPP accesses
*   Non-3GPP access generates one more key KN3IWF
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/26c5ab26-95db-4d1c-aba7-547a43704b38/image.png)

## PDU Session Establishment for Non-3GPP

### ![](https://t3764800.p.clickup-attachments.com/t3764800/a40e3628-25a9-4cea-8c3e-57502d1809f7/image.png)

### ![](https://t3764800.p.clickup-attachments.com/t3764800/59bbd775-3c4b-4d5c-aba8-85ad97ce4b57/image.png)
