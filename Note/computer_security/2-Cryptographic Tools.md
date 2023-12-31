---
title: "Computer Security Principles and Practice"
permalink: /Computer-Security-Principles-and-Practice/2-Cryptographic-Tools/
layout: default
---
# 2-Cryptographic Tools

Learning Objectives

After studying this chapter, you should be able to:

*   Explain the basic operation of symmetric block encryption algorithms. （對稱區塊加密演算法）
*   Compare and contrast block encryption and stream encryption. （比較區塊加密跟串流加密）
*   Discuss the use of secure hash functions for message authentication. （訊息安全hash函數）
*   List other applications of secure hash functions. （安全hash函數）
*   Explain the basic operation of asymmetric block encryption algorithms.(非同步加密演算法)
*   Present an overview of the digital signature mechanism and explain the concept of digital envelopes. （數位簽章機制及解釋數位封裝的概念）
*   Explain the significance of random and pseudorandom numbers in cryptography. （密碼學中偽隨機性的重要性）

[https://www.youtube.com/watch?v=8I\_q-NNm7Nw&t=3s](https://www.youtube.com/watch?v=8I_q-NNm7Nw&t=3s)



# 2.1 Confidentiality with Symmetric Encryption

block encryption algorithms :

*   Data Encryption Standard (DES)
*   Advanced Encryption Standard (AES)

symmetric stream encryption algorithms

## Symmetric encryption(對稱加密)

*   Symmetric encryption == conventional encryption == single-key encryption
*   the only type of encryption in use prior to the introduction of public- key encryption in the late 1970s (是 20 世紀 70 年代末期引入公鑰加密之前唯一使用的加密類型。)
*   secret communication: Julius Caesar, U-boat, present-day diplomatic, military, commercial users
*   more widely used than asymmetric encryption (對稱式加密更廣泛使用)



two requirements for secure use of symmetric encryption:

1. A strong encryption algorithm
    *   Opponent: Unable to decrypt cipher text or discover the key, (given pairs of cipher texts and plain texts, as well as the algorithm)
2. Secure key distribution and maintenance (安全的分配及維運)

![](https://t3764800.p.clickup-attachments.com/t3764800/af11315e-bffd-4ddf-bef3-b7e7c07572dc/Screen%20Shot%202023-09-24%20at%208.57.11%20PM.png)

*   **Plaintext:** original message or data as input.
*   **Encryption algorithm:** The encryption algorithm performs various substitutions and transformations on the plaintext.
*   **Secret key:** The secret key is also input to the encryption algorithm. The exact substitutions and transformations performed by the algorithm depend on the key.
*   **Ciphertext:** This is the scrambled message produced as output. It depends on the plaintext and the secret key. For a given message, two different keys will produce two different ciphertexts.
*   **Decryption algorithm:** This is essentially the encryption algorithm run in reverse. It takes the ciphertext and the secret key and produces the original plaintext.



### Two approaches to attacking a symmetric encryption scheme(對稱式加密攻擊情況)

1. Cryptanalytic Attacks (密碼破譯)
*   Exploit:
    *   Nature of the algorithm(演算法本身有問題)
    *   general characteristics of the plaintext (有特徵字)
    *   Sample plain text-cipher text pairs
*   Trick:
    *   Deduce a specific plaintext or the key（推論出特定文字或金鑰）
*   effect:
    *   All future and past messages encrypted with that key are compromised
2. Brute-Force Attack （暴力破解）
*   Exploit
    *   Knowledge about the expected plaintext(解出來且自己要看得懂)
*   Trick:
    *   Try all possible keys on some ciphertexts
        *   Until an intelligible translation into plaintext is obtained
        *   On average half of all possible keys must be tried to achieve success
*   effect:
    *   get the plain text



### **Symmetric Block Encryption Algorithms** **(對稱式加密演算法)**

most commonly used symmetric encryption algorithms

*   block ciphers
    *   block cipher processes the plaintext input in fixed-size blocks and produces a block of ciphertext of equal size for each plaintext block (它將明文分成多個等長的模組（block），使用確定的演算法和對稱金鑰對每組分別加密解密)
    *   Block Ciphers:
        *   Data Encryption Standard (DES)
        *   triple DES
        *   Advanced Encryption Standard (AES)



#### Data Encryption Standard (DES)

*   Adopted in 1977 by the NIST (FIPS PUB 46)
    *   Most widely used encryption scheme: aka Data Encryption Algorithm (DEA) (最常用加密情況)
    *   64-bit plaintext blocks and a 56-bit key➔64-bit ciphertext blocks (使用64bit的明文區塊與56bit的key 加密產出 64bit的密文區塊)
*   Security concerns
    *   Algorithm: characteristics may be exploited?
        *   Most-studied encryption algo: numerous attempts to find weakness, but no fatal one yet
    *   Key length: too short
        *   56 bits➔256 = 7.2 x 10^16 possible keys (Inadequate for today’s processor speed)

![](https://t3764800.p.clickup-attachments.com/t3764800/8d5bd066-a828-4865-8071-4c0aa500e612/Screen%20Shot%202023-09-25%20at%209.52.28%20AM.png)



#### Brute-Force Attacks against DES

*   On average, half the key space has to be searched
    *   One DES encryption per micro second➔more than 1000 years (3.6 x 10^16 keys)
*   In July 1998, EFF broke a DES encryption
    *   DES cracker: less than $250,000, less than three days
    *   [http://cs-exhibitions.uni-klu.ac.at/index.php?id=263](http://cs-exhibitions.uni-klu.ac.at/index.php?id=263)![](https://t3764800.p.clickup-attachments.com/t3764800/e1d12e14-6f78-436f-ae66-15a6d1b9dcfd/Screen%20Shot%202023-09-25%20at%2010.04.08%20AM.png)



*   Encryption speeds advance
    *   Seagate Technology \[SEAG08\]
        *   Multicore computers (2008): 10^9 per second
    *   EE Times \[AROR12\]
        *   Contemporary supercomputer (2012): 10^13 per second➔break DES within 1 hour

> EFF (Electronic Frontier Foundation): the leading nonprofit organization defending civil liberties in the digital world

![](https://t3764800.p.clickup-attachments.com/t3764800/21aeaefa-ea42-45af-a2c3-38ece9c5d6c0/Screen%20Shot%202023-09-25%20at%2010.08.18%20AM.png)



#### [Triple DES (3DES)](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-3722)

*   Part of the DES in 1999: FIPS PUB 46-3
    *   Repeat basic DES algorithm 3 times using either 2 or 3 unique keys (有助於向下相容)
    *   A key size of 112 or 168 bits
*   3DES was first standardized for use in financial applications in ANSI standard X9.17 in 1985
*   _resistant to cryptanalysis_
    *   no effective cryptanalytic attack based on the algorithm rather than brute force has been found(尚未發現基於該演算法有效密碼分析攻擊(除了暴力破解的))![](https://t3764800.p.clickup-attachments.com/t3764800/9ee0f1a8-a93b-4896-a237-8af36de50bfc/Screen%20Shot%202023-09-25%20at%2010.19.43%20AM.png)
*   Two attractions
    *   168-bit key length: overcomes brute-force attack of DES
    *   Underlying encryption algorithm is the same as in DES
*   Two drawbacks
    *   Sluggish(緩慢) algorithm/software: not efficient software code and three times as DES （最初的 DES 是為 20 世紀 70 年代中期實作硬體而設計的，不能產生高效的軟體程式碼）
    *   Uses a 64-bit block size: not efficient and not secure, a larger block size is desirable (大一點的區塊大小效率及安全更佳)



#### Advanced Encryption Standard (AES)

*   AES: now widely available in commercial products
    *   A replacement for 3DES
    *   3DES was not reasonable for long term use
*   NIST called for proposals for a new AES in 1997(不確定足不足夠安全，所以到2001才release)
    *   Security strength: equal to or better than 3DES
    *   Significantly improved efficiency
        *   Evaluation criteria included security, computational efficiency, memory requirements, hardware and software suitability, and flexibility
    *   Symmetric block cipher (對稱區塊加密)
    *   128-bit block length data and 128/192/256 bit keys
*   Selected Rijndael Algorithm in Nov. 2001: published as FIPS 197



#### Practical Security Issues

*   electronic codebook (ECB)
    *   plaintext is handled _b_ bits at a time (Typically _b_ \= 64 or _b_ \= 128) (通常區塊大小為64bit 或128bit)
    *   each block of plaintext is encrypted using the same key (每個區塊都是用同一個key加密)
    *   A plain text of length _n\*b_ is divided into _n b_\-bit blocks (_P_1, _P_2, c, _Pn_). Each block is encrypted using the same algorithm and the same encryption key, to produce a sequence of _n b_\-bit blocks of ciphertext (_C_1, _C_2, ...., _Cn_).
    (n\*b明文大小的明文(_通常區塊大小為64bit 或128bit_)，每個區塊都用一樣的演算法與一樣的key加密，製造出n個b-bit區塊的密文)![](https://t3764800.p.clickup-attachments.com/t3764800/bb6265b7-b986-471c-b5d8-4d5362050cea/Screen%20Shot%202023-09-30%20at%2010.45.10%20AM.png)
    *   _exploit_
        *   not secure with lengthy messages
        *   cryptanalyst able to exploit regularities in the plaintext (密碼分析者也許能夠利用明文中的規律來簡化解密任務)
*   **modes of operation**
    *   Cipher Block Chaining (CBC) Mode
        *   Five modes of operation defined by NIST
            *   ECB, CBC, etc.
    *   CBC can overcome the weakness of ECB
    *   explored in Chapter 20

![](https://t3764800.p.clickup-attachments.com/t3764800/57f71fb2-7027-40ab-bae6-6bb5afe19413/Screen%20Shot%202023-09-30%20at%202.03.32%20PM.png)



### **Stream Ciphers**

*   processes the input elements continuously, producing output one element at a time (持續輸入再讓結果一次輸出)
    *   _block cipher_ processes the input one block of elements at a time, producing an output block for each input block (區塊加密輸入一次並加密個別輸入的區塊)
    *   block cipher are far more common (區塊加密比較常見，但還是有適合stream cipher的場合)
    *   stream cipher may be designed to operate on one bit at a time or on units larger than a byte at a time.
    *   The output of the generator, called a **keystream**, is combined one byte at a time with the plaintext stream using the bitwise exclusive- OR (XOR) operation



![](https://t3764800.p.clickup-attachments.com/t3764800/0d0d3d4b-e156-479c-88d9-e54e4f632292/Screen%20Shot%202023-09-30%20at%2011.01.01%20AM.png)



| Block Cipher | Stream Cipher |
| ---| --- |
| ⚫ Processing one block at a time<br>⚫ Each input block → an output block<br><br><br>⚫ Pro: Can reuse keys<br> More common<br>⚫ Apps: file transfer, e-mail, and database | ⚫ Processing input elements continuously<br>⚫ One element at a time<br> Typically: one byte; one bit or larger units are also allowed<br>⚫ Pro: almost always faster (XOR) and use far less code<br>⚫ Apps: data stream over a communication channel or a browser/Web link<br> |
|  | The keystream must not be reused!!<br>Consider: (A ⊕ K) ⊕ (B ⊕ K) = A ⊕ B |

# 2.2 Message Authentication and Hash Function

### **Authentication Using Symmetric Encryption**

*   Message (data) authentication
    *   Communicating parties can verify that received/stored messages are authentic
    *   Against falsification of data and transactions (反偽造數據和交易)
*   Two major aspects to verify
    *   Message contents: not altered (內容不被替換)
    *   Message source: authentic (資源可信)
*   Another aspect
    *   Message timestamp timeliness/sequence: not artificially delayed or replayed (沒有延遲傳輸)

#### Can We Use Symmetric Encryption?

*   Authentic source (可信來源)
    *   Only the sender and the receiver share the key (只有發送者及接收者共享金鑰)
*   No altered contents (沒有替換內容)
    *   An error-detection code (錯誤檢測程式碼)
*   Proper message timeliness (適當的消息或時間戳記)
    *   A sequence number or a timestamp

**_It seems proper, but it is not a suitable tool for data authentication. Why?_**

### Message Authentication w/o Encryption (訊息驗證無加密)

*   Message authentication: a separate function from message encryption
    *   e.g., a broadcast message to many destinations(當發送broadcast message 沒有共享key時), not able to decrypt all incoming messages(來不及解密), wasteful of processor resources(浪費處理器資源)
*   How? an auth. tag is generated and appended to each message
    *   Message Authentication Code (MAC)
    *   One-Way Hash Function



#### Message Authentication Code (MAC)

*   Use a secret key to generate a small block of data (用密鑰來產生小區塊資料)
*   Assumption: two communicating parties share the secret key ![](https://t3764800.p.clickup-attachments.com/t3764800/0c506ab7-63a0-4030-8511-2938546e7505/Screen%20Shot%202023-09-30%20at%2011.02.01%20PM.png)(兩個交流的人共享同一個密鑰)
*   MAC algorithms: NIST recommends DES ![](https://t3764800.p.clickup-attachments.com/t3764800/0cc94f65-f35f-419d-a7b7-72e96dce3127/Screen%20Shot%202023-09-30%20at%2011.01.33%20PM.png)
*   MAC: last 16- or 32-bit code of the encrypted message

if the received code _matches_ the calculated code, then:

1. message has not been altered (訊息沒有被替換)
2. receiver is assured that the message is from the alleged sender (接收者確信該訊息來自所謂的發送者) ➝ _Because no one else knows the secret key_
3. If the message includes a sequence number (such as is used with X.25, HDLC, and TCP), then the receiver can be assured of the proper sequence **➝** _because an attacker cannot successfully alter the sequence number._ ![](https://t3764800.p.clickup-attachments.com/t3764800/9960d68d-73b1-463b-82f4-1c9b47e3cca0/Screen%20Shot%202023-09-30%20at%2011.17.51%20PM.png)
*   Drawbacks
    *   Encryption software is quite slow
    *   Encryption hardware costs are non-negligible
    *   Encryption hardware is optimized toward large data sizes

Does message authentication really need encryption of the message?

*   No. Why?
    *   Authentication need not be reversible
    *   Only need a way to generate a tag which can verify messages

> 回想一下我們在第 2.1 節中對實際安全問題的討論，對於大量數據，需要某種操作模式來將分組密碼（例如 DES）應用於大於單一區塊的資料量。對於這裡提到的MAC應用，DES應用在所謂的密碼塊連結模式(CBC)中。本質上，DES 按順序應用於訊息的每個 64 位元區塊，加密演算法的輸入是當前明文區塊和前一個密文區塊的 XOR。 MAC 源自於最終的區塊加密。有關 CBC 的討論請參閱第 20 章。



#### One-way Hash Function

![](https://t3764800.p.clickup-attachments.com/t3764800/92eefe3e-46a9-4187-91e0-54a977c87e28/image.png)

*   One-way Hash Function是一種用於MAC的替代方法。
*   One-way Hash Function接受可變長度的消息 M 作為輸入，並生成固定長度的消息摘要 H(M) 作為輸出。
*   Message通常會填充為某個固定長度（例如，1024 位）的整數倍，並且填充包括原始消息長度（以比特為單位）的值。
*   長度字段是一種安全措施，用於增加攻擊者生成具有相同Hash value的替代消息的難度。



*   A variable-size message M➔Tag: a fixed-size message digest H(M) (該訊息被填滿為某個固定長度（例如，1024 位元）的整數倍，並且填入包含原始訊息的長度值（以位元為單位）。長度欄位是一種安全措施，旨在增加攻擊者產生具有相同雜湊值的替代訊息的難度。)
*   Unlike MAC
    *   does not take a secret key as input



> The hash value ensures only unaltered contents. How about authentic source?

#### Hash Function w/ Symmetric Encryption

![](https://t3764800.p.clickup-attachments.com/t3764800/c4ef310e-09ba-461f-a4df-0b36fc617334/image.png)

*   The message digest can be encrypted using symmetric encryption(message hash後用key密並填入填充加長度字段)

#### Hash Function w/ Public-key Encryption

![](https://t3764800.p.clickup-attachments.com/t3764800/0f7b4e83-5711-4fe7-9ffb-a83602120936/image.png)

*   The message digest be encrypted using public-key encryption (message hash後用public key加密並填入填充加長度字段) ➝ Section 2.3
    *   Pros
        *   It provides a digital signature as well as message authentication (它提供數位簽名以及訊息認證)
        *   it does not require the distribution of keys to communicating parties.(它不需要向通訊各方分發金鑰)



這兩種方法(Hash Function w/ Symmetric Encryption & Hash Function w/ Public-key Encryption)比加密整個訊息的方法具有優勢，因為需要較少的計算。但更常見的方法是使用_完全避免加密_的技術。 \[TSUD92\] 中指出了幾個這種興趣的原因:

*   Encryption software is quite slow. Even though the amount of data to be encrypted per message is small, there may be a steady stream of messages into and out of a system.(加密軟體速度相當緩慢。儘管每個訊息要加密的資料量很小，但係統中可能會有穩定的訊息流進出。)
*   Encryption hardware costs are non-negligible. Low-cost chip implementations of DES and AES are available, but the cost adds up if all nodes in a network must have this capability.(加密硬體成本不可忽視。 DES 和 AES 的低成本晶片實作是可用的，但如果網路中的所有節點都必須具有此功能，則成本會增加。)
*   Encryption hardware is optimized toward large data sizes. For small blocks of data, a high proportion of the time is spent in initialization/invocation overhead.(加密硬體針對大數據量進行了最佳化。對於小資料塊，很大一部分時間花費在初始化/呼叫開銷上。)
*   An encryption algorithm may be protected by a patent.(加密演算法可能受專利保護。)

#### Hash Function w/o Encryption: Keyed Hash MAC

![](https://t3764800.p.clickup-attachments.com/t3764800/a63734bb-388d-4223-87ab-f6b69ee53600/image.png)

*   hash function but no encryption for message authentication.
1. **Key Preparation:**
    *   Ensure that you have a secret key (K) for both the sender and the recipient.
2. **Padding:**
    *   If necessary, pad the key to match the block size of the hash function (e.g., by hashing it if it's longer than the block size).
3. **Inner Hash:**
    *   XOR the key with a constant (ipad) and hash the result together with the message (M) using the chosen hash function (H).

```plain
scss
H(K XOR ipad || M)
```

1. **Outer Hash:**
    *   XOR the key with a different constant (opad) and hash the result todether with the output of the inner hash using the same hash function (H).

```plain
mathematica
H(K XOR opad || H(K XOR ipad || M))
```

1. **Output:**
    *   The result of the outer hash is the HMAC value, which can be used for message authentication and integrity verification.

The HMAC construction ensures that both the secret key and the message are involved in the hash computation, making it resistant to various types of attacks.

### Secure Hash Functions

#### haSh Function rEquirEMEntS

A hash function 𝐻 must have the following properties（函數 𝐻 必須具有以下特性）

1. 𝐻 can be applied to a block of data of any size （𝐻 可應用於任何大小的數據塊）
2. 𝐻 produces a fixed-length output（𝐻 產生固定長度的輸出）
3. 𝐻(𝑥) is relatively easy to compute for any given 𝑥 （對於任何給定的 𝑥，計算 𝐻(𝑥) 相對容易）
    *   Making both hardware and software implementations practical （可以用於硬件和軟件實現）
4. One-way (pre-image resistant) （可以用於硬件和軟件實現）
    *   For any given code h, it is computationally infeasible to find 𝑥 such that 𝐻(𝑥)=h （對於任何給定的代碼 h，計算上是不可能找到 𝑥 使得 𝐻(𝑥)=h）
5. Second pre-image (weak collision) resistant （𝐻 是第二原像抵抗（抗弱碰撞攻擊））
    *   For any given block 𝑥, it is computationally infeasible to find 𝑦 ≠ 𝑥 with 𝐻(𝑦)= 𝐻(𝑥) （對於任何給定的數據塊 𝑥，計算上是不可能找到 𝑦 ≠ 𝑥 使得 𝐻(𝑦)= 𝐻(𝑥)）
6. Collision (strong collision) resistant（𝐻 是碰撞抵抗（抗強碰撞攻擊））
    *   It is computationally infeasible to find any pair (𝑥, 𝑦) such that 𝐻 𝑥 = 𝐻(𝑦)= h （計算上是不可能找到任何一對 (𝑥, 𝑦) 使得 𝐻(𝑥) = 𝐻(𝑦)）



Feature

*   fixed-length output, computationally feasible
*   one-way property: computationally infeasible to find a message given its hash code, and finding an alternative message with the same hash value should also be impossible.
*   weak hash function satisfies the first five properties
*   strong hash function satisfies all six properties, including protection against attacks where one party generates a message for another party to sign.
*   A message digest generated by a hash function provides data integrity by detecting any accidental alterations in the message during transit.



#### Security of hash Functions

*   There are two approaches to attacking a secure hash function: cryptanalysis and brute-force attack.
*   **cryptanalysis**
    *   exploits logical weaknesses in the algorithm
    *   nature of the algorithm + knowledge of the general characteristics of the plaintext + some sample plaintext-ciphertext pairs
*   brute-force attacks
    *   The strength of a hash function against brute-force attacks depends on the length of the hash code produced by the algorithm.
    *   difficult to attack
        *   message compressed before encryption ➝ recognition difficult
        *   numerical file compressed ➝ recognition difficult

the level of effort required is proportional to the following:

![](https://t3764800.p.clickup-attachments.com/t3764800/1872b30c-351f-4f2e-bd6b-d83328b0078b/Screen%20Shot%202023-11-04%20at%202.43.44%20PM.png)

*   Preimage resistant: 2𝑛
*   Second preimage resistant: 2𝑛
*   Collision resistant: 2𝑛/2
    *   Based on that a birthday attack on a message digest of size n produces a collision
    *   128-bit MD5 \[VANO94\]: 24 days
    *   160-bit SHA: > 4000 years

#### Secure hash function algorithm

*   Most widely used hash algorithm: Secure Hash Algorithm (SHA)
    *   Developed by NIST, and published in FIPS 180, 1993
    *   SHA-1 160-bit (1995)
    *   SHA-2共有六個變種 : SHA-256, SHA-384, SHA-512 (2002)
    *   SHA-3共有五個變種： SHA-3-224, SHA-3-256, SHA-3-384, SHA-3-512 (2015)
    *   SHA-3 與 SHA-2 的主要區別如下：

| 特徵 | SHA-3 | SHA-2 |
| ---| ---| --- |
| 結構 | 海綿函數 | Feistel 迴圈 |
| 摘要長度 | 任意 | 固定 |
| 安全性 | 高 | 高 |
| 效率 | 高 | 高 |
| 擴展性 | 易 | 難 |

### Other Applications of Hash Function

*   Applications of hash functions
    *   Message authentication （認證）
    *   Digital signatures（數位簽章） (later in this Chapter)
    *   Passwords（加密） (Chapter 3)
        *   In password storage, the hash of a password is stored instead of the password itself, making it difficult for hackers to retrieve the actual password. In intrusion detection, hash values are used to determine if a file has been modified without changing the hash value.
    *   Intrusion detection (Chapter 8)
        *   Store the hash value for a file, H(F), for each file on a system and secure the hash values
        *   An intruder would need to change F without changing H(F).
        *   This application requires weak second preimage resistance.



# 2.3 Public-Key Encryption

## **Public-Key Encryption Structure(公鑰加密結構)**

*   Public-key cryptography
    *   Proposed by Diffie and Hellman in 1976
    *   Asymmetric algorithm (非對稱加密算法)
        *   Two separate keys: public and private keys (它使用兩把分開的密鑰：公鑰和私鑰)
    *   Based on mathematical functions (基於數學函數)
        *   Different from symmetric algorithms: simple operations on bit patterns(不同於對稱加密算法中對位模式進行簡單操作的運算。)
*   Three common _misconceptions_ for public-key encryption (**三個常見誤解**)
    *   More secure than symmetric ones (公鑰加密比對稱加密更安全)
        *   **公鑰加密和對稱加密各有其優缺點。**公鑰加密更難以破解，但運算效率較低。對稱加密運算效率較高，但密鑰分發和管理更加困難**。在實際應用中，通常會將公鑰加密和對稱加密結合使用，以獲得更好的安全性和性能。**
    *   A general-purpose technique that has made symmetric ones obsolete (公鑰加密是一種通用技術，它已經使對稱加密過時)
        *   公鑰加密和對稱加密各有其適用場景。公鑰加密通常用於身份驗證和數位簽名，而對稱加密通常用於數據加密。公鑰加密不能完全替代對稱加密，因為對稱加密在某些場景中具有更好的性能優勢。
    *   Key distribution is trivial (密鑰分發非常簡單)
        *   公鑰加密中的密鑰分發確實比對稱加密要簡單一些。公鑰可以公開發布，而私鑰需要保密。在通信之前，發送方可以向接收方發送自己的公鑰。接收方收到公鑰後，可以使用公鑰來加密數據。只有接收方可以使用自己的私鑰來解密密文。但是，公鑰加密中的密鑰分發也存在一些挑戰，例如如何防止中間人攻擊

For public-key key distribution, some form of protocol is needed, often involving a central agent, and the procedures involved are no simpler or any more efficient than those required for symmetric encryption.（對於公鑰加密中的鍵分發，需要使用某種形式的協議，通常涉及一個中央代理，而涉及的過程並不比對稱加密所需的簡單或高效。）

![](https://t3764800.p.clickup-attachments.com/t3764800/d42ae125-5cda-4d4b-b2d9-7713662dbaec/Screen%20Shot%202023-11-04%20at%205.36.25%20PM.png)

一個公鑰加密方案有六個組成部分（見圖 2.6a）：

*   明文（Plaintext）：這是作為輸入餵給算法的可讀消息或數據。
*   加密算法（Encryption algorithm）：加密算法對明文進行各種轉換。
*   公鑰和私鑰（Public and private key）：這是一對經過選擇的密鑰，如果一個密鑰用於加密，另一個密鑰就用於解密。加密算法進行的具體轉換取決於作為輸入提供的公鑰或私鑰。
*   密文（Ciphertext）：這是作為輸出生成的混淆消息。它取決於明文和密鑰。對於給定的消息，兩個不同的密鑰將產生兩個不同的密文。
*   解密算法（Decryption algorithm）：該算法接受密文和匹配的密鑰，並產生原始明文。

通用公鑰加密算法依賴於一個密鑰進行加密，另一個相關的密鑰進行解密。

基本步驟如下：

1. 每個用戶生成一對密鑰，用於對消息進行加密和解密。
2. 每個用戶將兩個密鑰中的其中一個放入公共註冊表或其他可訪問文件中。這就是公鑰。伴隨的密鑰是保密的。正如圖 2.6a 所示，每個用戶都維護一個從他人那裡獲得的公鑰集合。
3. 如果Bob想向Alice發送私人消息，Bob將使用Alice的公鑰對消息進行加密。
4. 當Alice收到消息時，她將使用她Alice的私鑰對其進行解密。沒有其他收件人可以解密消息，因為只有Alice知道Alice的私鑰。

圖 2.6a 的方案旨在提供機密性(confidential)

圖 2.6b 的方案旨在提供身份驗證(authentication)和/或數據完整性(data Integrity)

## Application for Public-Key Cryptosystems (公鑰加密系統的應用)

1. 數位簽名
2. 對稱密鑰分發
3. 秘密密鑰

| **Algorithm** | **Digital Signature** | **Symmetric Key Distribution** | **Encryption of Secret Keys** |
| ---| ---| ---| --- |
| RSA | Yes | Yes | Yes |
| Diffie–Hellman | No | Yes | No |
| DSS | Yes | No | No |
| Elliptic Curve | Yes | Yes | Yes |

*   RSA 是一種廣泛使用的非對稱加密算法，實現用於公鑰加密。它使用區塊加密，需要 1024 位元的密鑰大小以獲得強大的安全性。
*   Diffie-Hellman 金鑰交換是第一個發佈的公開金鑰算法，可讓兩個用戶安全地同意共用密鑰以進行後續對稱加密。
*   數位簽名標準 (DSS) 是一種使用數位簽名演算法 (DSA) 和 SHA-1 的數位簽名技術。它僅針對數字簽名功能而設計，不像RSA，DSS不能用於加密或密鑰交換。
*   橢圓曲線密碼學 (ECC) 是與 RSA 競爭的系統，具有較小的位元大小提供相同的安全性，從而降低了處理費用。然而，與 RSA 相比，ECC 是相對新的，信心水平較低。 -ECC 正在被 IEEE 等組織標準化，並在加密和數字簽名應用程序中越來越受歡迎。 -RSA 中必須使用較大的金鑰大小以維持安全性，如一個挑戰所示，一個 129 個小數位數字金鑰在 8 個月內使用 1600 台計算機被破解。

## Requirements for Public-Key Cryptosystems(**公鑰加密的要求**)

*   Computationally easy (計算上容易)
    *   Create key pairs (生成一對密鑰)
    *   for sender knowing public key to encrypt messages(發送方知道公鑰即可加密消息)
    *   for receiver knowing private key to decrypt ciphertext (接收方知道私鑰即可解密密文)
*   Computationally infeasible for opponent knowing public key (計算上不可能)
    *   Determine private key (對手知道公鑰也無法確定私鑰)
    *   Recover original message, which is encrypted by public key (對手知道公鑰和密文也無法恢復原始消息)
*   Either of private and public keys can be used for encryption (私鑰和公鑰都可以用於加密)

# 2.4 Digital Signatures and Key Management

*   The secure distribution of public keys (公開金鑰的安全分發)
*   The use of public-key encryption to distribute secret keys(使用公鑰加密發布密鑰)
*   The use of public-key encryption to create temporary keys for message encryption (創建用於消息加密的臨時金鑰。)

## Digital Signature

*   public encryption 可用於通過 digital signature 進行身份驗證。 
*   digital signature 提供來源身份驗證(digital signature)，數據完整性(data integrity)和簽署者的非拒絕(signatory non-repudiation)。
*   digital signature : data-dependent bit pattern(資料區塊所產生的唯一模式)
*   允許其他代理程式(agent)驗證簽署者的身份
    *   **驗證：**
        *   **數據塊已由聲稱的簽名者簽署（**alleged signer**）**
        *   **數據塊自簽署以來未被篡改。**

the use of one of three digital signature（FIPS 186-4）：

*   Digital Signature Algorithm (DSA): The original NIST-approved algorithm, which is based on the difficulty of computing discrete logarithms.
*   RSA Digital Signature Algorithm: Based on the RSA public-key algorithm.
*   Elliptic Curve Digital Signature Algorithm (ECDSA): Based on elliptic-curve cryptography.

![](https://t3764800.p.clickup-attachments.com/t3764800/7b5d6cd6-7378-4d5d-a336-f5fe3c061b74/Screen%20Shot%202023-11-04%20at%206.37.10%20PM.png)

**步驟：**

1. Bob 使用安全 Hash\_func(message) ➝ hash value。
2. Bob 使用自己的 Digital\_signature\_gen\_func(bob\_private key , hash value)➝ Bob's Signature。
3. Bob 將帶有簽名的消息(Message+Bob's Signature)發送給 Alice。
4. Alice 收到帶有signature 的message後，使用 Bob 的 public key 驗證 signature。
    1. 計算該 Message 的 hash value
    2. 將 **hash value** 和 **Bob 的 public key** 作為 Digital Signature Verification 的輸入。
5. 如果簽名有效，則 Alice 可以確信該消息一定是 Bob 簽署的，並且沒有被篡改。



## Public-Key Certificates

*   Public key distribution（**公鑰分發**）
    *   Any person can release his or her public key（任何人都可以發布自己的公鑰）
    *   But anyone can forge such a public announcement（但任何人都可以偽造這樣的公鑰公告）
*   Solution: public-key certificate （**公鑰證書**）
    *   Certificate: a public key + a user ID of the key owner （公鑰 + 密鑰所有者的用戶 ID）
    *   The whole block signed by a trusted third party, CA (Certificate Authority)
        *   CA has to be trusted by the user community (e.g., government)（CA 必須受到用戶群體（例如政府）的信任）
    *   Certificate also includes CA information and validity period （證書還包括 CA 信息和有效期）
*   X.509 standard: universally accepted certificates （**普遍接受的證書**）
    *   Used in most network security apps: IPSec, TLS, SSH, S/MIME



key steps

![](https://t3764800.p.clickup-attachments.com/t3764800/93d87a0a-9ccd-4824-8ef6-ab802a938b52/image.png)

1\. User software (client) creates a pair of keys: one public and one private.

2\. Client prepares an unsigned certificate that includes the user ID and user’s

public key.

3\. User provides the unsigned certificate to a CA in some secure manner. This might

require a face-to-face meeting, the use of registered e-mail, or happen via a Web

form with e-mail verification.

4\. CA creates a signature as follows:

a. CA uses a hash function to calculate the hash code of the unsigned certificate. A hash function is one that maps a variable-length data block or message into a fixed-length value called a hash code, such as SHA family that we will discuss in Sections 2.2 and 21.1.

b. CA generates digital signature using the CA’s private key and a signature generation algorithm.

5\. CA attaches the signature to the unsigned certificate to create a **signed certificate**.

6\. CA returns the signed certificate to client.

7\. Client may provide the signed certificate to any other user.

8\. Any user may verify that the certificate is valid as follows:

a. User calculates the hash code of certificate (not including signature).

b. User verifies digital signature using CA’s public key and the signature verification algorithm. The algorithm returns a result of either signature valid or invalid.

![](https://t3764800.p.clickup-attachments.com/t3764800/d1b903ab-1727-4204-b8a9-ccd7a2f35be2/Screen%20Shot%202023-11-04%20at%207.45.17%20PM.png)

## **Symmetric Key Exchange Using Public-Key Encryption**

**使用對稱加密時，雙方安全通信的一個基本要求是共享一個秘密密鑰。假設 Bob 想要創建一個消息應用程序，使他能夠與任何有權訪問 Internet 或他們共享的其他網絡的人安全地交換電子郵件。假設 Bob 想使用對稱加密來做到這一點。**

**一種方法是使用 Diffie-Hellman 密鑰交換。這種方法確實被廣泛使用。但是，它在最簡單的形式下存在一個缺點，即 Diffie-Hellman** **不提供兩個通信方身份驗證****。有克服此問題的 Diffie-Hellman 變體。此外，還有使用其他公鑰算法的協議可以實現相同的目標。**

### **Digital Envelopes(數位信封)**

*   Protect a message without having the same secret key between sender/receiver (sender和receiver**不需具有相同秘密密鑰**)
    *   Equate to the same thing as a sealed envelope containing a letter
*   Can also be used to deliver a symmetric key only

![](https://t3764800.p.clickup-attachments.com/t3764800/abd0976c-881c-400d-a977-fad80b89bf30/Screen%20Shot%202023-11-04%20at%208.08.19%20PM.png)

假設 Bob 想向 Alice 發送保密消息，但他們沒有共享對稱秘密密鑰：

1. 準備Message。
2. 生成一個只用一次的隨機 symmetric key。
3. 使用one-time key使用 symmetric key 加密該Message。
4. 使用 Alice 的公鑰使用 public-key encryption 加密 one-time key。
5. 將加密的一次性密鑰附加到**加密的消息**上並將其發送給 Alice。

只有 Alice 能夠解密一次性密鑰，因此能夠恢復原始消息。如果 Bob 通過 Alice 的公鑰證書獲取了 Alice 的公鑰，那麼 Bob 可以確定它是一個有效的密鑰。



# 2.5 Random and Pseudorandom Numbers

## **The Use of Random Numbers**

*   Used for generation of：
    *   公鑰算法的密鑰(keys for public-key algo)、stream keys for symmetric stream cipher (對稱流密鑰的流密鑰)、對稱密鑰(symmetric keys)
*   兩個不同的要求
    *   隨機性( Randomness)
        *   Uniform distribution (均勻分佈)：每個數字出現的頻率應該大致相同
        *   Independence獨立性：任何一個值都不能從其他值推斷出來
    *   不可預測性(Unpredictability)
        *   不太要求數字序列在統計學上是隨機的
        *   但是，序列的後繼成員是不可預測的

### Random vs. Pseudorandom

*   Pseudorandom(**偽隨機**): its use is widely accepted
    *   Apps typically use deterministic algorithms (應用程序通常使用確定性算法)
    *   Sequences: not statistically random, but can satisfy statistical randomness tests(不是統計上是隨機的，但可以滿足統計隨機性測試)
*   Random(**隨機**): true random number generator(真隨機數生成器 ) (TRNG)
    *   Use a nondeterministic source to produce randomness(使用非確定性源產生隨機性)
    *   Most operate by measuring unpredictable natural processes
        *   E.g., radiation(輻射), gas discharge(氣體放電), leaky capacitors(漏電容), thermal noise(熱噪聲)
    *   Increasing provided on modern chips

###
