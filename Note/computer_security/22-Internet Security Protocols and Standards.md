---
title: "Computer Security Principles and Practice"
permalink: /Computer-Security-Principles-and-Practice/22-Internet-Security-Protocols-and-Standards/
layout: default
---
# 22-Internet Security Protocols and Standards

[https://www.youtube.com/watch?v=PetQPBlkk\_Y](https://www.youtube.com/watch?v=PetQPBlkk_Y)

# **22.1  Secure E-mail and S/MIME**

## MIME

*   An Internet mail format: an extension to the old RFC 822 specification
    *   RFC 822 defines a simple heading with To, From, Subject
    *   Assumes ASCII text format
*   Provides new header fields
    *   Defining information about the message body
*   MIME Content Types :

![](https://t3764800.p.clickup-attachments.com/t3764800/0cce11a8-5d50-4a30-89d2-8b8dace9c263/Screen%20Shot%202023-11-12%20at%2010.22.31%20AM.png)

## S/MIME

*   Secure/Multipurpose Internet Mail Extension
*   Security enhancement to the MIME Internet e-mail format
    *   Based on technology from RSA Data Security
*   Provides the ability to sign and/or encrypt e-mail messages
*   S/MIME is defined as a set of additional MIME content types (see Table 22.1)
*   these content types support four new functions:
    *   **Enveloped data:** Consists of encrypted content of any type and encrypted-content encryption keys for one or more recipients. (**Encrypted content and associated keys**)
    *   **Signed data:** A digital signature is formed by taking the message digest of the content to be signed, then encrypting that with the private key of the signer. The content plus signature are then encoded using base64 encoding. A signed data message can only be viewed by a recipient with S/MIME capability. (**Encoded message + signed digest**)
    *   **Clear-signed data:** As with signed data, a digital signature of the content is formed. However, in this case, only the digital signature is encoded using base64. As a result, recipients without S/MIME capability can view the message content, although they cannot verify the signature. (**Cleartext message + encoded signed digest**)
    *   **Signed and enveloped data:** Signed-only and encrypted-only entities may be nested, so encrypted data may be signed, and signed data or clear-signed data may be encrypted. (**Nesting of signed and encrypted entities** )
*   S/MIME content type:

| **Type** | **Subtype** | **S/MIME Parameter** | **Description** |
| ---| ---| ---| --- |
| Multipart | Signed |  | A clear-signed message in two parts: one is the message and the other is the signature. |
| Application | pkcs7-mime | signedData | A signed S/MIME entity |
| pkcs7-mime | envelopedData | An encrypted S/MIME entity |
| pkcs7-mime | degenerate signedData | An entity containing only public-key certificates |
| pkcs7-mime | CompressedData | A compressed S/MIME entity |
| pkcs7-signature | signedData | The content type of the signature subpart of a multipart/signed message |



### MIME and S/MIME Message Examples

![](https://t3764800.p.clickup-attachments.com/t3764800/b1418d4f-4e0e-4fa9-a194-e3d7811b5630/Screen%20Shot%202023-11-12%20at%2010.16.23%20AM.png)

### Signed and Clear-Signed data

*   Signed data➔Base64(content + sig)
*   Clear-signed data➔content + Base64(sig)
*   Default algorithms used for signing messages
    *   DSS(SHA-1(Message), DSS-private-key)
    *   DSS: Digital Signature Standard; SHA: Secure Hash Algorithm
*   Alternative
    *   RSA(SHA-1/MD5(Message), RSA-private-key)
*   Radix-64/Base64: mapping content/sig into printable ASCII characters



*   S/MIME messages are signed using either RSA or DSA algorithms to create a digital signature.
*   The signature is created by taking a SHA-256 hash of the message + sender's private key to create a unique 256-bit digest.
*   The digest is encrypted with the sender's private key to create the signature.
*   The recipient can verify the signature by decrypting it with the public key and comparing the decrypted digest to a newly calculated digest.
*   This provides message integrity as alterations would change the digest.
*   The signature is binary data so it is encoded into printable ASCII characters using base64 encoding before sending.
*   Base64 mapping converts each 3 octets of binary data into 4 ASCII characters to represent it.

### enveloped data

*   Default algorithms used for encrypting S/MIME messages are AES and RSA
    *   M→AES(M)→AES(M) + RSA(K)
        *   M: message
        *   K: a pseudorandom secret key
        *   Use recipient’s public RSA key to encrypt K

![](https://t3764800.p.clickup-attachments.com/t3764800/8dc5c654-13d5-4fc8-9b75-acc146dc56e7/Screen%20Shot%202023-11-12%20at%2010.33.51%20AM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/06900c75-0c2e-4993-afc0-0ba5ee3d755e/Screen%20Shot%202023-11-12%20at%2010.44.07%20AM.png)

### public-Key Certificates

*   Using certificates that conform to the international standard X.509v3

# **22.2  DomainKeys Identified Mail**

*   A specification of cryptographically signing e-mail messages
    *   A signing domain can claim responsibility for a message
    *   RFC 4871 standard: DKIM signatures
    *   Message recipients (or agents acting in their behalf) can verify the signature by querying the signer’s domain directly to retrieve the appropriate public key and thereby can confirm that the message was attested to by a party in possession of the private key for the signing domain
*   Has been widely adopted by a range of e-mail providers
    *   e.g., gmail, yahoo, and many ISPs
*   Why DKIM?
    *   An email authentication technique that is transparent to the end user
    *   Reasons
        *   S/MIME depends on both the sending and receiving users employing S/MIME
            *   But, the bulk of incoming mail does not use S/MIME
        *   S/MIME signs only the message content
            *   Header information concerning origin can be compromised
        *   Transparent to the user; (s)he need take no action
        *   Applied to all mails from cooperating domains
    *   Preventing forgers from masquerading as good senders

## Internet Mail Architecture

*   User world: MUA(**Message User Agent**)
    *   Works on behalf of user actors and user applications
*   Transfer world(MHS, Message handling system):
    *   MSA(**Mail submission agent**)
        *   Accepts the message submitted by an MUA and enforces the policies of the hosting domain and the requirements of Internet standards.
    *   MTAs (**Message transfer agent**)
        *   Relays mail for one application-level hop
        *   MTA also adds trace information to the message header
    *   **MDA****(Mail delivery agent)**
        *   Responsible for transferring the message from the MHS to the MS.
*   **Message store (MS)**
    *   MUA retrieves messages from a remote server using
        *   POP (Post Office Protocol) or IMAP (Internet Message Access Protocol).

![](https://t3764800.p.clickup-attachments.com/t3764800/c7291e2a-300d-4d11-9cae-c7e386fcefce/Screen%20Shot%202023-11-12%20at%2010.53.29%20AM.png)

## DKIM Strategy

motivation for DKIM is based on the following reasoning:

1. **S/MIME depends on both the sending and receiving users employing S/MIME****.**
    1. **For almost all users, the bulk of incoming mail does not use S/MIME, and the bulk of the mail the user wants to send is to recipients not using S/MIME.**
2. **S/MIME signs only the message content****. Thus, RFC 5322 header information concerning origin can be compromised.**
3. **DKIM is not implemented in client programs(MUAs)****and is therefore transparent to the user; the user need take no action.**
4. **DKIM applies to all mail from cooperating domains****.**
5. **DKIM allows good senders to prove that they did send a particular message**
6. **and to prevent forgers from masquerading as good senders.**



![](https://t3764800.p.clickup-attachments.com/t3764800/46b498be-f55a-420b-8b56-37fd6d69b64a/Screen%20Shot%202023-11-12%20at%2010.58.49%20AM.png)

# **22.3  Secure Sockets Layer (SSL) and Transport Layer Security (TLS)**

## TLS Architecture

*   Secure Socket Layer (SSL)
    *   One of the most widely used security services
    *   SSL3.0, SSL2.0 (deprecated in 2015)
*   Transport Layer Security (TLS)
    *   Becoming Internet standard RFC4346
    *   General-purpose service: as a set of protocols that rely on TCP
    *   TLS1.3, TLS1.2, TLS1.1 (new standards)
    *   Two implementation choices
        *   As part of the underlying protocol suite: transparent to apps
        *   Be embedded in specific packages: e.g., most browsers come equipped with SSL



*   Record Protocol: provides basic security services to various higher-layer protocols
*   HTTP: provides the transfer service for Web client/server interaction, can operate on top of TLS
*   three higher-layer protocols are defined as part of TLS:
    *   Handshake Protocol
    *   Change Cipher Spec Protocol
    *   Alert Protocol

![](https://t3764800.p.clickup-attachments.com/t3764800/335a07d4-426e-49ec-9645-d27ffe05fb82/Screen%20Shot%202023-11-12%20at%2011.10.39%20AM.png)



*   TLS Concepts
    *   TLS Connection
        *   A transport (in the OSI layering model definition) that provides a suitable type of service
        *   Peer-to-peer relationships
        *   Transient (短暫的)
        *   Every connection is associated with one session
    *   TLS Session
        *   An association between a client and a server
        *   Created by the handshake protocol
        *   Define a set of cryptographic security parameters
        *   Used to avoid the expensive negotiation of new security parameters for each connection

## TLS Protocols

### Record Protocol

*   **Confidentiality:** The Handshake Protocol defines a shared secret key that is used for symmetric encryption of SSL payloads.
*   **Message integrity:** The Handshake Protocol also defines a shared secret key that is used to form a message authentication code (MAC).



**TLS Record Protocol Operation** **:**

1. Each upper-layer message is fragmented into blocks of 214 bytes (16,384 bytes) or less.
    1. compression is optionally applied
2. compute a MAC over the compressed data
3. symmetric encryption (compressed message + MAC)
4. SSL Record Protocol processing is to prepend a header
    1. content types that have been defined are change\_cipher\_spec, alert, handshake, and application\_data

> 對於TLS來說,所有在它之上使用TLS的應用層協議(比如HTTP),都是不透明的。TLS不需要理解應用資料的內容和格式。  
> TLS的工作是在傳輸層為TCP連接提供安全加密通道。它不依賴也不了解上層應用的協議邏輯。不管是HTTP、SMTP、FTP等任何應用,對TLS來說都是一樣的。  
> TLS運行在應用層協議之下,應用層協議產生的原始資料內容對TLS是不透明的。TLS只負責進行加密和傳輸,不依賴應用內容。

![](https://t3764800.p.clickup-attachments.com/t3764800/47a2937a-19ba-4e92-9cba-7d6d3324692a/Screen%20Shot%202023-11-12%20at%2011.14.43%20AM.png)

### Change Cipher Spec Protocol

*   consists of a single byte with the value 1
*   cause the pending state to be copied into the current state, which updates the cipher suite to be used on this connection

### Alert Protocol

*   convey(運送) TLS-related alerts to the peer entity
*   alert messages are compressed and encrypted, as specified by the current state



*   Each message in this protocol consists of two bytes to convey the severity of the message
    *   first byte
        *   warning(1)
        *   fatal(2)
            *   TLS immediately terminates the connection.
            *   Other connections on the same session may continue, but no new connections on this session may be established
    *   second byte: specific alert code
        *   a code that indicates the specific alert
        *   close\_notify(0), unexpected\_message(10), etc.
        *   e.g. fatal alert: an incorrect MAC
        *   e.g. nonfatal alert: a close\_notify message



### Handshake Protocol

*   Most complex part of TLS
*   Used before any application data are transmitted
*   Allows server and client to:
*   Comprises a series of messages exchanged by client and server
*   Exchange has four phases
    *   **Phase 1**
        *   Establish security capabilities, including protocol version, session ID, cipher suite, compression method, and initial random numbers.
    *   **Phase 2**
        *   Server may send certificate, key exchange, and request certificate. Server signals end of hello message phase.
    *   **Phase 3**
        *   Client sends certificate if requested. Client sends key exchange. Client may send certificate verification.
    *   **Phase 4**
        *   Change cipher suite and finish handshake protocol.

![](https://t3764800.p.clickup-attachments.com/t3764800/94ec402d-3faa-428d-857d-fae3df78e711/Screen%20Shot%202023-11-12%20at%2011.35.12%20AM.png)

### ClientHello (RFC)

### ![](https://t3764800.p.clickup-attachments.com/t3764800/ed946391-4556-461d-8df1-767ba3a5e078/Screen%20Shot%202023-11-12%20at%2011.40.08%20AM.png)

struct {

ProtocolVersion client\_version;

Random random;

SessionID session\_id;

CipherSuite cipher\_suites <2..2^16-2>;

CompressionMethod compression\_methods <1..2^8-1>;} ClientHello;



struct {

ProtocolVersion server\_version;

Random random;

SessionID session\_id;

CipherSuite cipher\_suite;

CompressionMethod compression\_method;} ServerHello;



### HeartBeat Protocol

*   A periodic signal generated by hardware or software
    *   Indicates normal operation or synchronizes other parts of a system
    *   Typically used to monitor the availability of a protocol entity
    *   Timer: 1s to 60s (RFC6347)
    *   Its Use is established during Phase 1 of the Handshake Protocol
*   Serves two purposes:
    *   Assures the sender that the recipient is still alive
    *   Generates activity across the connection during idle periods

![](https://t3764800.p.clickup-attachments.com/t3764800/7b2236d1-210d-49cc-adca-6ff11d8108e6/Screen%20Shot%202023-11-12%20at%2011.43.16%20AM.png)

## SSL/TLS Attacks

### Attack Categories

*   **Attacks on the Handshake Protocol:**
    *   Attacks have targeted the SSL/TLS handshake protocol implementation and RSA encryption. Countermeasures have led attackers to refine their techniques to bypass defenses and speed up attacks.
*   **Attacks on the record and application data protocols:**
    *   Vulnerabilities in the SSL/TLS record and application data protocols have enabled practical attacks like BEAST that exploit chosen-plaintext cryptanalysis. Subsequent patches address specific issues like BEAST and CRIME.
        *   BEAST: (Browser Exploit Against SSL/TLS)
        *   CRIME (Compression Ratio Info-leak Made Easy) attack
*   Attacks on the PKI:
    *   Research has revealed weaknesses in X.509 certificate validation across many SSL/TLS libraries and applications, demonstrating vulnerabilities in public key infrastructure.
*   **Other attacks:**
    *   Denial of service attacks are possible by overwhelming servers with handshake requests to consume computational resources for continuous cryptographic key generation.

#### **The Heartbleed Exploit**

![](https://t3764800.p.clickup-attachments.com/t3764800/1927cd26-b414-4f7a-b150-9c0c7dddd63d/Screen%20Shot%202023-11-12%20at%2011.51.49%20AM.png)

# **22.4  HTTPS**

## Connection Initiation

*   Combination of HTTP and SSL
    *   HTTP over TLS (RFC2818)
    *   Secure communication between a Web browser and a Web server
*   Built into all modern Web browsers
    *   URL addresses begin with https://
*   Connection initiation and closure
    *   HTTP client act as TLS client
    *   TLS handshake➔HTTP request
    *   Three levels: HTTP, TLS session, TCP



## Connection Closure

*   HTTP clients/servers can indicate closing a connection by sending a `Connection: close` header.
*   Closing an HTTPS connection requires the TLS layer to exchange closure alerts and close the TCP connection.
*   TLS implementations should initiate a proper closure alert exchange before closing a connection.
*   TLS can do an "incomplete close" by closing after sending an alert without waiting for the peer's alert.
*   HTTP clients must handle cases where the TCP connection closes without a TLS closure alert, which could indicate an attack.
*   Clients should warn the user if the TCP connection closes without a proper TLS closure exchange.



# **22.5  IPv4 and IPv6 Security**

## IP Security Overview

*   Application-specific security mechanisms exist like S/MIME, Kerberos, SSL etc but IP-level security is needed to protect all applications uniformly.
*   IPsec was added to IPv6 to provide authentication, encryption and key management. It can also work with IPv4.
*   IPsec includes authentication to verify packets are from claimed sources and unchanged, confidentiality via encryption, and key management for secure exchange.
*   Current IPsec version (IPsecv3) provides authentication and confidentiality. Key management is done separately via IKEv2.
*   IPsec architecture and technical details are then described.

![](https://t3764800.p.clickup-attachments.com/t3764800/0989ff95-e27d-406c-9363-a2cf9ad3b437/Screen%20Shot%202023-11-12%20at%2012.06.08%20PM.png)

*   IPsec can can encrypt and/or authenticate _all_ traffic at the IP level, secure all IP traffic including remote access, client/server apps, email etc.

IPsec provides capability to secure communications across a LAN:

*   **Secure branch office connectivity over the Internet:**
    *   enables secure VPN over the public internet for branch office connectivity. This reduces private network costs
*   **Secure remote access over the Internet:**
    *   provides secure remote access over the internet, reducing telecommuting costs.
*   **Establishing extranet and intranet connectivity with partners:**
    *   secures connectivity with partners by providing authentication, encryption and key exchange.
*   **Enhancing electronic commerce security:**
    *   It enhances electronic commerce security by encrypting/authenticating web and ecommerce traffic.

### Benefits of IPSec

*   Strong security applied to all traffic at a firewall or router
*   Resistant to bypass at a firewall
*   Transparent to apps
    *   No need to change software
*   Transparent to end users
    *   No need to train users on security mechanisms

### Routing apps

*   prevent attackers from disrupting communications or diverting some traffic
*   A router advertisement from an authorized router
*   A neighbor advertisement from an authorized router
*   A redirect message from the router to which the initial packet was sent
*   A routing update is nor forged

## The Scope of IPsec

*   Two main functions
    *   Encapsulating Security Payload (ESP): a combined authentication/encryption function
    *   A key exchange function: Internet Key Exchange standard (IKEv2)
*   VPN: both authentication and encryption are generally desired
*   Authentication Header (AH): authentication-only function (deprecated)

## Security Associations

*   A key concept of IPSec
    *   One-way relationship between a sender and a receiver
    1. Two-way secure exchange: two SAs(security association) are required
*   Uniquely identified by three parameters
    *   Security parameter index (SPI)
        *   A bit string assigned to this SA and having local significance only. The SPI is carried in an ESP header to enable the receiving system to select the SA under which a received packet will be processed.
    *   IP destination address
        *   the address of the destination endpoint of the SA, which may be an end-user system or a network system such as a firewall or router
    *   Protocol identifier: AH or ESP
        *   This field in the router IP header indicates whether the association is an AH or ESP security association
*   Characterized by the following parameters
    *   Sequence number counter: 32-bit
    *   Sequence counter overflow: A flag➔whether overflow➔an auditable event
    *   Anti-replay window: defining a sliding window
    *   AH information
        *   Algorithm, keys, key lifetimes, etc.
    *   ESP information
        *   Algorithm, keys, init values, key lifetimes, etc.
    *   Lifetime of this security association
    *   IPSec protocol mode: tunnel, transport, or wildcard
    *   *   Path MTU: maximum size of a packet that can be transmitted without fragmentation

### Two IPSec Operation Modes

*   Transport and Tunnel modes

## Encapsulating Security Payload(ESP)

*   ESP provides confidentiality services
    *   confidentiality of message contents
    *   limited traffic flow confidentiality
*   Figure 22.8 shows the format of an ESP packet. It contains the following fields:
    *   **Security Parameters Index (32 bits):** Identifies a security association.
    *   **Sequence Number (32 bits):** A monotonically increasing counter value.
    *   **Payload Data (variable):** This is a transport-level segment (transport mode) or IP packet (tunnel mode) that is protected by encryption.
    *   **Padding (0–255 bytes):** May be required if the encryption algorithm requires the plaintext to be a multiple of some number of octets.
    *   **Pad Length (8 bits):** Indicates the number of pad bytes immediately preceding this field.
    *   **Next Header (8 bits):** Identifies the type of data contained in the Payload Data field by identifying the first header in that payload (e.g., an extension header in IPv6, or an upper-layer protocol such as TCP).
    *   **Integrity Check Value (variable):** A variable-length field (must be an integral number of 32-bit words) that contains the integrity check value computed over the ESP packet minus the Authentication Data field.

![](https://t3764800.p.clickup-attachments.com/t3764800/6f27d0fa-7cc6-45f2-83eb-e6ced9287d8e/Screen%20Shot%202023-11-12%20at%2012.33.31%20PM.png)

## Transport and Tunnel Modes

### transport Mode

*   Protection: the payload of an IP packet
*   Typically used for end-to-end communication between two hosts
*   ESP protects the IP payload but not the IP header

### Tunnel Mode

*   Protection: the entire IP packet
*   Entire original packet travels through a tunnel from one point to another
*   Used when one or both ends of a security association are a security gateway
*   Hosts on networks behind firewalls may engage in secure communications without implementing IPSec

![](https://t3764800.p.clickup-attachments.com/t3764800/0ed31d53-fefc-4b25-beb8-7251c8d68f0a/Screen%20Shot%202023-11-12%20at%2012.24.24%20PM.png)



### IPSec: AH + ESP

*   IP AH only ![](https://t3764800.p.clickup-attachments.com/t3764800/d4f9ffdd-9db7-4f20-8c86-616f8a72402b/Screen%20Shot%202023-11-12%20at%2012.39.55%20PM.png)
*   IP AH + ESP
    *   Transport mode
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/135f261e-5a51-4836-8688-8bab2c8edb68/Screen%20Shot%202023-11-12%20at%2012.40.20%20PM.png)
    *   Tunnel mode
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/5856678b-856f-4792-b669-6ed76e29c372/Screen%20Shot%202023-11-12%20at%2012.40.37%20PM.png)

**Q: Does** IP AH + ESP **support NAT? Why?**

A: No, IPsec AH and ESP do not support NAT (Network Address Translation) well. There are a few key reasons:

*   AH and ESP encrypt the entire IP payload, including the source and destination IP addresses. This prevents NAT from modifying the IP headers.
*   AH authenticates portions of the IP header that NAT needs to modify, like IP addresses and checksums. This breaks the authentication.
*   ESP in tunnel mode encrypts the entire original IP packet, preventing NAT access to header fields.
*   AH and ESP use sequence numbers for anti-replay protection. NAT renumbering packets breaks the sequence.
*   Encryption hides the payload from NAT's analysis of protocols and ports.
*   IPsec security associations are based on fixed IP addresses which NAT modifies.



IPsec 是一種基於 IP 層的安全協定，它使用兩個協定來提供安全性：AH (Authentication Header) 和 ESP (Encapsulating Security Payload)。

*   **AH (Authentication Header):** AH 協定用於驗證 IP 包的來源和完整性。它使用雜湊函數來計算 IP 包的雜湊值，並將雜湊值附加到 IP 包中。接收方可以使用相同的雜湊函數來驗證 IP 包的完整性。
*   **ESP (Encapsulating Security Payload):** ESP 協定用於加密 IP 包的內容。它使用加密算法來加密 IP 包的內容，並將加密後的內容附加到 IP 包中。接收方可以使用相同的密鑰來解密 IP 包的內容。

IPsec 還包括兩種模式：隧道模式和傳輸模式。

*   **隧道模式:** 隧道模式將 IP 包完全封裝在另一個 IP 包中。這使得 IPsec 可以保護 IP 包的頭部和內容。
*   **傳輸模式:** 傳輸模式僅加密 IP 包的內容。這使得 IPsec 可以保護 IP 包的敏感內容，但不保護 IP 包的頭部。

IPsec 是一種強大的網路安全協定，它可以用於保護各種網路連接。IPsec 的使用可以幫助組織降低網路安全風險，保護敏感資料。

以下是 IPsec 的一些技術特性：

*   **安全性:** IPsec 使用加密、雜湊函數和身份驗證技術來保護 IP 包的機密性、完整性和可用性。
*   **可靠性:** IPsec 使用重組和檢測重傳 (ARQ) 技術來確保 IP 包的完整性。
*   **擴展性:** IPsec 可以擴展到支持各種安全需求。
*   **可管理性:** IPsec 可以使用各種管理工具來管理和配置。

IPsec 是一種成熟的網路安全協定，它已被廣泛部署在各種網路中。IPsec 的使用可以幫助組織降低網路安全風險，保護敏感資料。



### Case Study: VoWi-Fi Session Hijacking

*   VoWi-Fi (Voice over Wi-Fi): telephony calls over Wi-Fi
    *   Complements VoLTE (Vocie over LTE) for poor-signal areas
    *   Supported by a system called IMS (IP Multimedia Subsystem)

![](https://t3764800.p.clickup-attachments.com/t3764800/29d073a1-9c5d-42fa-9d6e-ac945dac2c69/Screen%20Shot%202023-11-12%20at%2012.42.15%20PM.png)

#### A Vulnerability at the Call State Machine

![](https://t3764800.p.clickup-attachments.com/t3764800/e5ebe25b-0897-4b74-a8e9-1676a836f96d/Screen%20Shot%202023-11-12%20at%2012.42.48%20PM.png)

#### VoWi-Fi SIP Sessions Protected by IPSec

*   How to hijack the session to exploit the vulnerability?

#### ![](https://t3764800.p.clickup-attachments.com/t3764800/e55edffe-3483-475f-b31a-9a760e9bd018/Screen%20Shot%202023-11-12%20at%2012.43.09%20PM.png)

### IPSec Implementation Analysis

### ![](https://t3764800.p.clickup-attachments.com/t3764800/d9d11e54-308f-4ff1-a2e5-519909c4a766/Screen%20Shot%202023-11-12%20at%2012.43.39%20PM.png)

*   XFRM (“transform”): The Linux kernel’s IP framework for transforming packets (such as encrypting payloads)
    *   Support IPSec

### Example: XFRM IPSec SAs

*   Phone 1
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/b0687aa5-cdbb-4fb9-977e-467769a32329/Screen%20Shot%202023-11-12%20at%2012.46.00%20PM.png)

### Example: XFRM IPSec SAs

*   Phone 2

![](https://t3764800.p.clickup-attachments.com/t3764800/93f8bdc2-5f46-45db-b670-6cee8ede93b3/Screen%20Shot%202023-11-12%20at%2012.46.31%20PM.png)

### IPSec SAs Negotiation

### ![](https://t3764800.p.clickup-attachments.com/t3764800/48a550b9-5f5f-4c10-89ba-5d2f1333926f/Screen%20Shot%202023-11-12%20at%2012.46.58%20PM.png)

#### IPSec Transport Packet

![](https://t3764800.p.clickup-attachments.com/t3764800/f309c89f-970d-4630-834a-a49183c5e9c3/Screen%20Shot%202023-11-12%20at%2012.47.26%20PM.png)

### How to Fabricate a IPSec-protected SIP Message?

*   SIP message content
    *   caller and callee numbers
    *   Static info: SIP server/proxy addresses and supported features, etc.
    *   Dynamic info: tag, call id, branch id, etc.
*   ESP integrity protection
    *   Obtain the IPSec security parameters from the SAD (Security Association DB)
        *   SPI and hash algorithm/keys
    *   Keep track of the sequence number of IPSec session
    *   Apply default ESP padding algorithm
    *   Generate authentication data using the hash algorithm/keys

# **22.6  Key Terms, Review Questions, and Problems**

Sure, here are the answers to your questions:

**22.1 List the default algorithms used for signing S/MIME messages.**

The default algorithms used for signing S/MIME messages are:

*   **Digital Signature Standard (DSS):** This algorithm provides digital signatures that are strong and reliable.
*   **Secure Hash Algorithm 1 (SHA-1):** This algorithm is used to create a hash of the message that is being signed. The hash is then encrypted with the signer's private key to create the digital signature.

**22.2 What is radix-64 conversion?**

Radix-64 conversion is a method of encoding binary data in a text format. This is useful for transmitting data over channels that cannot handle binary data, such as email.

**22.3 Why is radix-64 conversion useful for an e-mail application?**

Radix-64 conversion is useful for email applications because it allows binary data, such as attachments, to be transmitted over the email network. The radix-64 encoded data can be embedded in the email message itself.

**22.4 What is DKIM?**

DKIM (DomainKeys Identified Mail) is a method for verifying the identity of the sender of an email message. This helps to prevent email spoofing, which is the act of sending an email message that appears to be from someone else.

**22.5 During an HTTPS connection, which elements of the communication are encrypted?**

During an HTTPS connection, the following elements of the communication are encrypted:

*   The HTTP headers
*   The HTTP body

**22.6 What is the difference between an SSL connection and an SSL session?**

An SSL connection is a single communication between two parties. An SSL session is a series of SSL connections between two parties. An SSL session can be used to reduce the overhead of establishing new SSL connections.

**22.7 List the four categories of SSL/TLS attacks.**

The four categories of SSL/TLS attacks are:

*   **Man-in-the-middle attacks:** These attacks allow an attacker to intercept and modify traffic between two parties.
*   **Side-channel attacks:** These attacks exploit vulnerabilities in the implementation of SSL/TLS to obtain information about the communication.
*   **Downgrade attacks:** These attacks force a client to downgrade to a weaker version of SSL/TLS.
*   **Denial-of-service attacks:** These attacks attempt to prevent a client or server from using SSL/TLS.

**22.8 What is the purpose of HTTPS?**

The purpose of HTTPS is to secure communications between a web server and a web browser. This helps to protect sensitive information, such as credit card numbers, from being intercepted by third parties.

**22.9 State the three levels of awareness of a connection in HTTPS.**

The three levels of awareness of a connection in HTTPS are:

*   **Cleartext:** The communication between the client and the server is not encrypted.
*   **Transport layer security (TLS):** The communication between the client and the server is encrypted using TLS.
*   **End-to-end encryption:** The communication between the client and the server is encrypted using a key that is known only to the client and the server.

**22.10 Explain the transport and tunnel modes of ESP.**

ESP (Encapsulating Security Payload) is a security protocol that can be used to encrypt and authenticate IP packets. ESP can operate in two modes:

*   **Transport mode:** In transport mode, ESP is used to encrypt and authenticate the entire IP packet, including the IP header.
*   **Tunnel mode:** In tunnel mode, ESP is used to encrypt and authenticate the data payload of the IP packet. The IP header is not encrypted.

**22.11 What are the two ways of providing authentication in IPsec?**

There are two ways of providing authentication in IPsec:

*   **HMAC-SHA-1:** This method uses a hash function to authenticate the IP packet.
*   **Digital Signature Standard (DSS):** This method uses a digital signature to authenticate the IP packet.

I hope this helps!
