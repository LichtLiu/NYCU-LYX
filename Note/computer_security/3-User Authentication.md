---
title: "Computer Security Principles and Practice"
permalink: /Computer-Security-Principles-and-Practice/3-User-Authentication/
layout: default
---
# 3-User Authentication

[https://www.youtube.com/watch?v=Vk3M4mbaTjY&t=553s](https://www.youtube.com/watch?v=Vk3M4mbaTjY&t=553s)



*   User authentication is the fundamental building block of computer security.
*   User authentication has two functions: identification（身份識別） and verification（驗證）.
*   Identification：user provides a claimed identity to the system such as user ID
*   verifies： system verifies the user by the exchange of authentication information
*   User authentication is distinct from message authentication(message integrity).
*   This chapter will provide an overview of different means of user authentication and examine each in some detail.

# **3.1  Digital User Authentication Principles**

*   The process of verifying an identity claimed by or for a system entity
*   Two steps
    *   Identification step: presenting an identifier to the security system
    *   Verification step: presenting or generating authentication information that corroborates the binding between the entity and the identifier



## A Model for Digital User Authentication



**registration authority (RA)** : 註冊機構 (trusted entity)

負責建立(establishes )和驗證(vouch保證)申請人對 CSP 的身份

**credential service provider (CSP):** 憑證服務提供商

與訂閱者進行交流

**credential :**

**(**憑證是一種數據結構，它將身份(identity)和其他屬性(additional attribute)與訂閱者(subscriber)擁有的 token 綁定在一起，並且可以在身份驗證交易(authentication transaction)中呈現給驗證者時進行驗證。**)**



![](https://t3764800.p.clickup-attachments.com/t3764800/9e8389ca-83f5-4217-bc3e-bc45173faf22/Screen%20Shot%202023-11-05%20at%2012.30.33%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/6b249b34-6973-425f-b7ff-65b78539ab55/Screen%20Shot%202023-11-05%20at%2012.31.02%20PM.png)

_Defined by NIST SP 800-63-2 (Electronic Authentication Guideline, August 2013)_

註冊過程

1. **申請人(applicant)向 RA 申請成為subscriber。**

申請人向 RA 提交申請，包括個人信息、聯繫信息和其他相關信息。RA 驗證申請人的身份，並確保申請人符合 CSP 的註冊要求。

1. **RA 驗證申請人(applicant)的身份。**

RA 可以通過多種方式驗證 applicant 的身份，例如要求申請人提供身份證明、進行面談或進行生物識別掃描。

1. **CSP 向 subscriber 發布電子憑證。**

CSP 根據 RA 的驗證結果，向申請人發布電子憑證。憑證包含訂閱者的身份信息和其他屬性。

1. **訂閱者使用憑證進行身份驗證。**

訂閱者在需要身份驗證時，可以使用憑證向驗證者進行身份驗證。驗證者可以通過檢查憑證的有效性來驗證訂閱者的身份。



驗證過程：

1. **claimant 向verifier 提供身份驗證信息。**

**claimant**可以通過多種方式提供身份驗證信息，例如輸入密碼、提供生物識別信息或使用令牌。

1. **verifier驗證claimant提供的身份驗證信息。**
    1. claimant successfully demonstrates possession and control of a token to a verifier through an authentication protocol

verifier可以通過多種方式驗證claimant提供的身份驗證信息，例如檢查密碼是否匹配、驗證生物識別信息是否正確或檢查token是否有效。

1. **verifier向 Replying party 提供關於claimant身份的斷言(assertion)。**

**verifier**向**Replying party**提供關於**claimant**身份的**assertion**，包括**claimant**的身份信息和其他屬性。**Replying party**可以使用這些信息做出訪問控制(access control)或授權決定(authorization decision)。



### Cornerstone: Credential and Token

*   Credential**憑證**
    *   紙質憑證：證明身份的文件
        *   例如，護照、駕駛執照和學生證
        *   包含主體的描述、主體的照片或主體的簽名
    *   E-authentication credential 電子身份驗證憑證：一種object或數據結構
        *   Authoritatively binds an identity (via an identifier) and (optionally) additional attributes, to at least one token (or authenticator) possessed and controlled by a subscriber (權威地將身份（通過識別符）和（可選）其他屬性與訂閱者擁有和控制的至少一個令牌（或身份驗證器）綁定在一起 )
*   **Token令牌：** Claimant 擁有和控制的用來authenticate the Claimant’s identity
    *   通常是加密模塊或密碼(cryptographic module or password)
    *   也稱為身份驗證器(authenticator)
*   **換句話說，**authentication establishes confidence
    *   The Claimant has possession of an authenticator(s) bound to the credential(claimant擁有與憑證綁定的身份驗證器，以及（可選）訂閱者的屬性值)
        *   屬性值：他（她）是台灣公民或NCTU學生

### Digital Identity Model

![](https://t3764800.p.clickup-attachments.com/t3764800/eb928781-53ee-4329-9f35-31f5c042f786/Screen%20Shot%202023-11-05%20at%2012.56.14%20PM.png)

## Means of Authentication

身份驗證可以用來驗證用戶的身份。有四種通用的身份驗證方法，可以單獨使用或組合使用：

*   Something the individual knows
    *   e.g., password, answers to prearranged questions
*   Something the individual possesses
    *   e.g., electronic keycards, smart cards
*   Something the individual is (static biometrics)
    *   e.g., fingerprint, retina, face
*   Something the individual does (dynamic biometrics)
    *   e.g., voice pattern, handwriting

Problem:

*       *   攻擊者可能能夠猜測或竊取密碼。同樣，攻擊者也可能能夠偽造或竊取令牌。用戶可能會忘記密碼或丟失令牌。

Solution: **Multifactor authentication(多因子驗證)**

*       *   **Multifactor authentication** refers to the use of more than one of the authentication(兩種以上驗證) means in the preceding list (see Figure 3.2)
    *   two factors are considered to be stronger than those that use only one factor, and so on.

![](https://t3764800.p.clickup-attachments.com/t3764800/58ad5434-53d4-490d-b5da-6df6f9d0541f/Screen%20Shot%202023-11-05%20at%201.02.07%20PM.png)



## Risk Assessment for User Authentication

> Teacher doesn't teach this section

# **3.2  Password-Based** **Authentication**

*   **A Widely Used Line of Defense Against Intruders(**密碼系統是一種廣泛使用的防禦入侵者的方法**)**
    *   **User provides name or identifier (ID) and password.**
    *   **System compares password with the stored one.**
        *   **Password file** indexed by user ID that stores usernames or hash values of passwords.
*   **User ID**
    *   Determines whether the user is authorized to access the system.
        *   In some systems, only those who already have an ID filed on the system are allowed to gain access.
    *   Determines the user's privileges.
        *   administrator or “superuser” : enables to read files and perform functions especially protected by the operating system.
        *   guest or anonymous accounts : limited privileges .
    *   Used in discretionary access control (ID 用於所謂的自主訪問控制)
        *   通過列出其他用戶的 ID，用戶可以授予他們閱讀該用戶擁有的文件的權限(user may grant permission to them to read files owned by that user.)。

## The Vulnerability of Passwords

*   Offline dictionary attack
    *   Obtain the system’s password file (passwords stored in hash values)
        *   CVE cases: [https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=password](https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=password)
    *   Search for valid passwords with hash values of commonly used passwords
        *   Tools: [http://www.openwall.com/john/](http://www.openwall.com/john/), [http://project-rainbowcrack.com/](http://project-rainbowcrack.com/)
    *   Countermeasure: prevent unauthorized access to the password file, intrusion detection measures to identify a compromise, etc.
*   Specific account attack
    *   Submit password guesses until the correct password is discovered or the account Is blocked (more than 5 failure times)
*   Popular password attack
    *   Try popular passwords, e.g., 123456, against a wide range of user IDs
        *   Assume that adversary obtains user IDs in advance
    Countermeasure: inhibiting the selection by users of common passwords(禁止使用者選擇通用密碼), scanning the IP addresses of auth requests and client cookies for submission patterns
*   Password guessing against single user
    *   Gain knowledge about the account holder and system password policies, and use that knowledge to guess the password
    *   Countermeasure: enforcement of password policies that make passwords difficult to guess (e.g., minimum length of the password)
*   Workstation hijacking
    *   Wait until a logged-in workstation is unattended
    *   Countermeasure: automatically logging the workstation out after a period of inactivity
*   Exploiting user mistakes
    *   Mistakes: write it down, share it via any ways, keep preconfigured passwords, etc.
    *   Countermeasure: user training, intrusion detection, simpler passwords combined with another auth. mechanism, etc.
*   Exploiting multiple password uses
    *   Different network devices share the same or similar password for a given user
    *   Countermeasure: a policy that forbids it
*   Password sniffing/phishing
    *   Passwords are transmitted without encryption, e.g., http or ftp
    *   Phishing web pages
    *   Countermeasure: encryption, inputting passwords with trusted devices and environments, etc.
*   Reasons for the persistent popularity of passwords
    *   Cheap, convenient for use, and easy to implement
    *   Other techniques based on client-side hardware require the implementation of the software on both client and server
        *   e.g., fingerprint scanners and smart card readers
    *   Physical tokens are expensive and/or inconvenient
        *   e.g., smart cards
    *   Biometric tokens are expensive and/or not sufficiently accurate



## The Use of Hashed Passwords

*   A widely used password security technique
    *   hashed passwords and a salt value.
    *   On all UNIX variants and other OSes
    *   password is combined with a fixed-length **salt** value \[MORR79\]
        *   older salt: related to the time the password is assigned to the user
        *   newer salt: pseudorandom or random number
    *   hashing algorithm
        *   input : password + salt
        *   output：fixed-length hash code
            ![](https://t3764800.p.clickup-attachments.com/t3764800/b7340611-7fcf-4f1d-9ba1-2b831dc1862f/Screen%20Shot%202023-11-05%20at%202.02.11%20PM.png)
*   hash algorithm is designed to be slow to execute in order to thwart attacks （挫敗攻擊）
*   Password Stored:
    *   hashed password(encrypted password)
    *   plaintext copy of the salt (明文salt)
    *   corresponding user ID
*   hashed password method has been shown to be secure against a variety of _cryptanalytic attacks_

_login procedure__:_

![](https://t3764800.p.clickup-attachments.com/t3764800/f5f9d9c7-1e35-4620-b0f3-8aa4d221cbff/Screen%20Shot%202023-11-05%20at%202.02.36%20PM.png)

1. user provides an ID and a password (see Figure 3.3b)
2. OS uses the ID to index into the password file and retrieve the plaintext salt and the encrypted password.
3. salt and user-supplied password are used as input to the encryption routine.
4. If the result matches the stored value, the password is accepted.



### Why Salt?

*   Purpose I: prevents duplicate passwords from being visible in the password file
*   Purpose II: greatly increases the difficulty of offline dictionary attacks
    *   For a salt of length 𝑏 bits, the number of possible passwords is increased by a factor of 2𝑏
*   Purpose III: Nearly impossible to find out whether a person has used the same password on multiple systems

### Two Threats to UNIX password scheme

*   Threat I: password guessing on the machine
    *   Attackers gain access on a machine using a guest account or by some other means
    *   Run a password guessing program, called a password cracker
*   Threat II: password guessing on another machine
    *   They can have a copy of the password file on another machine, and then run the cracker
    *   Run through millions of possible passwords in a reasonable period

### UNIX Implementation

#### Old Implementation of UNIX Password Scheme

*   Password: up to 8 characters in length (56-bit value using 7-bit ASCII)
    *   Serving as the key input to DES
*   Modified DES encryption
    *   one-way hash function with a data input of a 64-bit block of zeros (修改後的 DES 算法使用由零組成的 64 位塊的數據輸入執行。然後，算法的輸出用作第二次加密的輸入。此過程總共重複 25 次加密。)
*   Repeated for a total of 25 encryptions
*   Has been regarded as inadequate (50 million password guesses in about 80 minutes)
    *   But, still often required for compatibility with existing account management software or multivendor environments

#### Improved Implementation of UNIX Password Scheme

*   Recommended hash function is based on MD5
    *   Salt: up to 48-bit
    *   Password length is unlimited (密碼長度沒有限制)
    *   A 128-bit hash value
    *   Slowdown: an inner loop with 1000 iterations (遠遠慢於 crypt(3))
*   Bcrypt: developed for OpenBSD based on the Blowfish symmetric block cipher
    *   Most secure version of Unix hash/salt scheme
    *   allows passwords of up to 55 characters (允許密碼長度最長為 55個字元)
    *   A 128-bit salt and a 192-bit hash value
    *   Configurable cost variables (number of iterations)



## Password Cracking of User-Chosen Passwords

### Traditional Approach

*   Traditional approaches
    *   Dictionary attack
        *   Prepare a large dictionary of possible password and try each
        *   Each password must be hashed using each salt value and then compared to stored hash values
        *   Countermeasure: slow hash functions
*   Password crackers exploit that fact that people choose easily guessable passwords
*   Rainbow table attacks
    *   Pre-compute tables of hash values for all salts (a mammoth table)
    *   Example: using 1.4GB rainbow table to crack 99.9% of all alphanumeric Windows password hashes in 13.8s ([http://lasecwww.epfl.ch/~oechslin/publications/crypto03.pdf](http://lasecwww.epfl.ch/~oechslin/publications/crypto03.pdf))
    *   Countermeasure: a sufficiently large salt value and a large hash length
    *   Notable open-source password cracker (developed in 1996 and still in use): Join the Ripper
        *   A combination of brute-force and dictionary techniques
        ![](https://t3764800.p.clickup-attachments.com/t3764800/a226ece3-5326-4d3f-9ce6-f13efcd9a563/Screen%20Shot%202023-11-05%20at%202.56.42%20PM.png)



### Modern Approach

*   Complex password policy
    *   Forcing users to pick stronger passwords
*   However, password-cracking techniques have also improved
    *   The processing capacity available for password cracking has increased dramatically (GPU)
        *   a single AMD Radeon HD7970 GPU, for instance, can try on average an 8.2 \* 109 password combinations each second, depending on the algorithm used to scramble them \[GOOD12a\]
        *   [http://www.cs.cornell.edu/~shmat/shmat\_ccs05pwd.pdf](http://www.cs.cornell.edu/~shmat/shmat_ccs05pwd.pdf)
    *   Studying examples and structures of actual passwords in use
        *   Apply data mining techniques to studying public password files (leaked by security vulnerability)
        *   E.g., an SQL injection attack against online games, [Rockyou.com](http://Rockyou.com)

→ a data breach resulting in the exposure of over 32M plaintext passwords in 2009



## Password File Access Control

*   Access control: makes the password file available only to privileged users
    *   One way to thwart a password attack is to deny the opponent access to the password file.
    *   hashed password file is accessible by a privileged user, then the opponent cannot read it without already knowing the password of a privileged user. (如果文件中的hash password部分只能由特權用戶訪問，則opponent在不知道特權用戶密碼的情況下無法讀取它。)
*   **shadow password file** **:** hashed passwords are kept in a separate file from the user IDs

Vulnerabilities

*   Weakness in the OS that allows access to the file
*   Accident with permissions making it readable
*   Users with same password on other systems
*   Weakness in physical security may provide access to backup media
*   Sniffing network traffic



## Password Selection Strategies

*   User education
    *   Users can be told the importance of using hard-to-guess passwords
*   Computer-generated passwords
    *   FIPS 181 Automated Password Generator: [http://pass.rasm.se/](http://pass.rasm.se/)
    *   But, users have trouble remembering them
*   Reactive password checking
    *   System periodically runs its own password cracker to find guessable passwords
*   Complex password policy or proactive password checker
    *   Rejecting guessable passwords

### Proactive Password Checking

*   Rule enforcement
    *   Specific rules that passwords must adhere to
    *   e.g., must be at least eight characters long, must include at least one for each of uppercase and lowercase
*   Password checker
    *   Compile a large dictionary of “bad” passwords not to use
    *   But, it is space-consuming and time-consuming



_Can we use a hash function to address the issues?_



*   Bloom filter: a space-efficient probabilistic data structure
    *   Used to test whether an element is a member of a set
    *   A bit array of _m_ bits, and _k_ different hash functions
    *   But, false positive matches are possible
    *   有兩個H1跟H2的Hash Function，abc跟123是弱密，abc hash 出25 bit 及998、123 hash 出83bit 跟 665bit，假設輸入xyz(非弱密)，但hash出665bit跟998bit，結果就會顯示為弱密，此情況又稱為 false positive
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/ae031a1c-dd3b-46da-b122-619d45fcaaed/Screen%20Shot%202023-11-12%20at%206.22.52%20PM.png)
        *   Result: possibly in set or definitely in set
    *   Space advantage: do not store the data items ()
*   Applied to the password checking
    *   (Traditional) build a table based on dictionary
    *   check desired password against the table

A Bloom filter of order _k_ consists of a set of _k_ independent hash functions _H_1(_x_), _H_2(_x_), c , _Hk_(_x_)（**k階Bloom filter由一組k個獨立的hash functions**）, where each function maps a password into a hash value in the range 0 to _N_ \- 1(其中每個函數將密碼映射到範圍為0到N- 1的哈希值).That is,

![](https://t3764800.p.clickup-attachments.com/t3764800/57dd4632-5644-4cd8-80cd-739bb7246784/Screen%20Shot%202023-11-05%20at%203.26.25%20PM.png)

*   Hi : **k個獨立的hash functions其中一個函數**
1. Xj = 密碼字典中的第j個單詞 （_j_th word in password dictionary ）
2. D = 密碼字典中的單詞數量（number of words in password dictionary）

1. **A hash table of** **_N_** **bits is defined, with all bits initially set to 0. (**定義一個N位哈希表，其中所有位最初都設置為0**)**
2. **For each password, its** **_k_** **hash values are calculated, and the corresponding bits in the hash table are set to 1. Thus, if** **_Hi_** **(X****_j_****) = 67 for some (****_i_****,** **_j)_****, then the sixty-seventh bit of the hash table is set to 1; if the bit already has the value 1, it remains at 1.(**對於每個密碼，計算其k個哈希值，並將哈希表中相應的位設置為1。因此，如果Hi(Xj) = 67對於某些(i, j)，則哈希表的第六十七位設置為1；如果該位已經有值1，它將保持為1**)**



當向檢查器呈現新密碼時，會計算其k個哈希值。 如果哈希表的所有相應位都等於1，則密碼將被拒絕。字典中的所有密碼都將被拒絕。但是還有一些“誤報”（即，字典中不存在但會在哈希表中產生匹配的密碼）

![](https://t3764800.p.clickup-attachments.com/t3764800/129b6cad-46fb-4bfe-a92a-3b833022384e/Screen%20Shot%202023-11-05%20at%203.36.30%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/e9e996e6-4461-4856-9f80-d68e82a76046/Screen%20Shot%202023-11-05%20at%203.37.45%20PM.png)

用array記Hash value，hash rable越大 false positive機率越小

![](https://t3764800.p.clickup-attachments.com/t3764800/7f586866-795a-40c5-8fef-acb539d42317/Screen%20Shot%202023-11-12%20at%206.31.39%20PM.png)

reference:

[https://www.evanlin.com/BloomFilter/](https://www.evanlin.com/BloomFilter/)

[https://medium.com/@Kadai/%E8%B3%87%E6%96%99%E7%B5%90%E6%A7%8B%E5%A4%A7%E4%BE%BF%E7%95%B6-bloom-filter-58b0320a346d](https://medium.com/@Kadai/%E8%B3%87%E6%96%99%E7%B5%90%E6%A7%8B%E5%A4%A7%E4%BE%BF%E7%95%B6-bloom-filter-58b0320a346d)



# **3.3  Token-Based Authentication**

tokens : Objects that a user possesses for the purpose of user authentication

*   two types of tokens that are widely used
*   cards that have the appearance and size of bank cards (see Table 3.3)

![](https://t3764800.p.clickup-attachments.com/t3764800/8e78df2a-9a28-4833-89a7-6fb8fbbbe649/Screen%20Shot%202023-11-05%20at%203.47.38%20PM.png)

## Memory Cards

*   Functions
    *   Can store but do not process data
    *   Can include an internal electronic memory
*   Most common: the bank card with a magnetic stripe on the back (黑磁條)
*   Alone for physical access (e.g., Hotel room)
    *   Combined with a password or PIN(personal identification number): provides significantly greater security
*   Drawbacks
    *   A special reader is required
        *   increases the cost of using the token and creates the requirement to maintain the security of the reader’s hardware and software.
    *   Token loss
        *   A lost token temporarily prevents its owner from gaining system access.
    *   User dissatisfaction
        *   no difficulty for ATM access, but for computer access inconvenient

## Smart Cards

### Smart Tokens

*   Categorized along four dimensions
    *   Physical characteristics
        *   Include an embedded microprocessor
        *   Like a bank card: smart card
        *   Others: calculators(HSBC calculator), keys, small portable objects
    *   User interface
        *   Manual interfaces include a keypad and display for interaction
    *   Electronic interface
        *   Required by a smart card or other token to communicate with a compatible reader/writer
        *   Contact（**接觸式）：** direct contact between a card reader and a conductive contact plate on the card （**接觸式智能卡必須插入具有與卡表面導電接觸板（通常鍍金）直接連接的智能卡讀卡器中。命令、數據和卡狀態的傳輸通過這些物理接觸點進行。**
        *   Contactless（**非接觸式）：**both the reader and the card have an antenna (天線)（**非接觸式卡只需要靠近讀卡器。讀卡器和卡都有一個天線，並且兩者使用無線電頻率進行通信。大多數非接觸式卡也從這種電磁信號中為內部芯片提供電力。對於無電池供電的卡來說，典型的範圍是一半到三英寸，這對於需要非常快速卡接口的應用（例如建築物入口和支付）來說是理想的選擇。）**
    *   Authentication protocol
        *   Static
            *   User authenticates himself or herself to the token (**用戶先向Token驗證自己**)
            *   Token authenticates the user to the computer (Token**再向計算機驗證用戶**)
        *   Dynamic password generator
            *   Token generates a unique password periodically (e.g., every minute) (Token**會定期（例如每分鐘）生成一個唯一密碼**)•
            *   Initialized and synchronized for the token and the computer ( Token **和 Computer 必須初始化並保持同步，以便計算機知道該令牌當前有效的密碼。**)
        *   Challenge-response
            *   Computer generates a challenge
            *   Token generates a response to the challenge (**智能Token會根據challenge生成response**)

### Smart Cards

*   Contains an entire microprocessor
    *   Including processor, memory, and I/O ports
    *   (optional) a special co-processing circuit for cryptographic operation
*   Three types of memory
    *   Read-only memory (ROM)
        *   stores data that does not change during the card’s life
        *   card number and the cardholder’s name
    *   Electrically erasable programmable ROM (EEPROM)
        *   holds application data and programs
        *   protocols (that the card can execute)
        *   etc. telephone card : holds the remaining talk time
    *   Random access memory (RAM)
        *   holds temporary data generated when applications are executed

typical interaction between a smart card and a reader or computer system.

### ![](https://t3764800.p.clickup-attachments.com/t3764800/6337ec5b-d8d0-49db-b98a-2e040c1c8895/Screen%20Shot%202023-11-05%20at%205.32.55%20PM.png)

*   card is inserted into a reader
*   reset function: reset is initiated by the reader to initialize parameters such as clock value
*   card responds with answer to reset (ATR) message (**卡會響應重置（ATR）消息**)
    *   ATR message: parameters and protocols that the card can use and functions it can perform
*   PTS command (protocol type selection)
    *   terminal may be able to change the protocol used and other parameters
*   PTS response confirms
    *   confirms the protocols and parameters to be used
*   terminal and card can now execute the protocol to perform the desired application

## Electronic Identify Cards

*   eID card is a smart card that Verified by the national government as valid and authentic
    *   Most advanced eID: German eID card
*   data printed on its surface
    *   **Personal data :** name, birth, address
    *   **Document number :** alphanumerical nine-character unique identifier
    *   **Card access number(CAN) :** six-digit decimal random number
    *   **Machine readable zone (MRZ) :**Three lines of human- and machine-readable text on the back of the card
*   Three eID functions
    *   ePass: government use; offline (e.g., electronic passport)
        *   Stores a digital representation of the identity (e.g., face and fingerprint images)
    *   eID: general-purpose use; offline and online
        *   Stores an identity record that authorized service can access with cardholder permission (e.g., name, date of birth, address)
        *   inspection system : terminal for law enforcement checks(border control officers)
            *   inspection system can read identifying information of the cardholder as well as bio- metric information stored on the card, such as facial image and fingerprints.
    *   eSign: generating a digital signature
        *   Stores a private key and a certificate verifying the key (e.g., X.509 certificate)

![](https://t3764800.p.clickup-attachments.com/t3764800/5a0d0471-1164-40f6-a31f-7642480b2988/Screen%20Shot%202023-11-05%20at%206.02.04%20PM.png)

### **User Authentication with eID**

![](https://t3764800.p.clickup-attachments.com/t3764800/cdb260cc-b757-48c2-beb8-fddc08b2a797/Screen%20Shot%202023-11-05%20at%206.06.02%20PM.png)

1. eID user visits a website and requests a service that requires authentication (1,2)
2. Web site sends back a redirect message that forward an authentication request to an eID server (3,4)
3. eID server requests that the user enter the PIN number for the eID card (5)
4. correctly entered the PIN (6)
5. authentication protocol exchange with the microprocessor on the eID card (7)
6. Authentication results are sent back to the user system to be redirected to the Web server application (8,9,10)

### _Password Authenticated Connection Establishment (PACE)_

*   ensures contactless RF chip in the eID card cannot be read without explicit access control
*   Online application : 6-digit PIN (known by holder)
*   offline application : MRZ, CAN



# **3.4  Biometric Authentication**

## Physical Characteristics Used in Biometric Applications

*   Authentication based on unique physical characteristics
    *   Static: facial characteristics, fingerprints, hand geometry, Retinal pattern(視網膜), Iris(虹膜), vein(靜脈)
    *   Dynamic: signature, voice
*   Relies on pattern recognition technologies
    *   More complex and expensive than passwords and tokens
    *   Not yet to mature as a standard tool

![](https://t3764800.p.clickup-attachments.com/t3764800/08b9c0ab-17ae-414e-aa52-d17a6a9c9422/Screen%20Shot%202023-11-05%20at%206.21.34%20PM.png)

## Operation of a Biometric Authentication System

*   users must first be **enrolled** in the system
    *   user presents a name and, typically, some type of password or PIN to the system
    *   system senses some biometric characteristic of this user (e.g., fingerprint of right index finger)
    *   digitizes the input and stored as a number
    *   user enrolled in the system ((ID), PIN or password, biometric value.)
*   **Verification**: analogous(類似) to a user logging on to a system by using a smart card and a PIN
*   **Identification**: user presents biometric info without other info; system compares it with stored templates

![](https://t3764800.p.clickup-attachments.com/t3764800/27199427-a426-40b7-93fa-ffb931230856/Screen%20Shot%202023-11-05%20at%206.34.01%20PM.png)

## Biometric Accuracy

*   false match rate（錯**誤匹配率-錯的判成對的**）：the frequency with which biometric samples from different sources are erroneously assessed to be from the same source. (**來自不同來源的生物識別樣本被錯誤評估為來自相同來源的頻率**)
*   false nonmatch rate(錯**誤識別率-對的判成錯的**)： the frequency with which samples from the same source are erroneously assessed to be from different sources. (**來自相同來源的樣本被錯誤評估為來自不同來源的頻率**)

![](https://t3764800.p.clickup-attachments.com/t3764800/fd17a342-76e5-4406-acb8-7f13f1bdabe0/Screen%20Shot%202023-11-05%20at%206.45.03%20PM.png)

s>=t a match is assumed, and for s < t , a mismatch is assumed



### **Ideal Biometric Measurement** operating characteristic curve.

*   The curve that is lower and to the left performs better
*   **Increase threshold : Increased security, decreased convenience**
*   **Decrease threshold : Decreased security, increased convenience**

![](https://t3764800.p.clickup-attachments.com/t3764800/99f5977d-ee91-4027-a24c-6eb9f5ee7ac8/Screen%20Shot%202023-11-05%20at%208.08.17%20PM.png)



### **Actual Biometric Measurement Operating Characteristic Curves**

*   false match rates, the face biometric is the worst performer
*   iris system had no false matches in over 2 million cross-comparisons.

![](https://t3764800.p.clickup-attachments.com/t3764800/6eb8c7a3-9edf-484b-9bf4-f449cbef61be/Screen%20Shot%202023-11-05%20at%208.14.29%20PM.png)

# **3.5  Remote User Authentication**

*   More complex than local authentication: over a network, the Internet, or a communication link
*   Why?
    *   More security threats: eavesdropping(竊聽), capturing a password, and replaying an authentication sequence that has been observed
*   General solution: challenge-response protocols
    *   password portocol
    *   token protocol
    *   static biometric protocol
    *   dynamic biometric protocol

## Password Protocol

*   [Kerberos](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4602) (CH23)

example :

1. transmits his or her identity to the remote host
2. host generates a random number _`r`__,_ called a **nonce**
3. returns `(`_`r`_`,` _`h`_`(),` _`f`_`())` to user to be used in the response ➝ (h(), f() are host specifies)
4. user’s response is the quantity _`f`_`(`_`r`_`′,` _`h`_`(`_`P`_`′))` ➝ _`r`_`′ =` _`r`_ and _P_′ is the user’s password
5. _`h`_`(`_`P`_`(`_`U`_`))` ➝ host stores the hash function of each registered user’s password
6. host compares the incoming _`f`_`(`_`r`_`′,` _`h`_`(`_`P`_`′))` to the calculated _`f`_`(`_`r`_`, h(`_`P`_`(`_`U`_`)))`

Against:

1. hash code of the password
2. No hash of the password is transmitted directly ➝ function in which the password hash is one of the arguments.
3. function _f_, the password hash cannot be captured during transmission.
4. replay attack: the use of a random number as one of the arguments of _`f`_ defends

![](https://t3764800.p.clickup-attachments.com/t3764800/05e4fc09-49af-467c-91f4-c708c901fce8/Screen%20Shot%202023-11-05%20at%208.32.51%20PM.png)



## Token Protocol

*   token
    *   stores a static passcode
    *   generates a one-time random passcode.
        *   the token synchronized in some fashion with the host.
        *   In either case（任一種情況）, the user activates the passcode by entering a password _P_′.
        *   password shared only between the user and the token and does not involve the remote host.

example :

1. transmits his or her identity to the remote host
2. host generates a random number _`r`_
3. returns `(`_`r`_`,` _`h`_`(),` _`f`_`())` to user to be used in the response ➝ (h(), f() are host specifies)
4. user’s response is the quantity _`f`_`(`_`r`_`′,` _`h`_`(W′))` ➝ _`r`_`′ =` _`r`_ and _`P' ➝ W'`_ password to passcode via token
5. hash registered user’s passcode
    1. static passcode : host stores the hash value `U` ➝ _`h`_`(W(`_`U`_`))`
    2. dynamic passcode : host generates a one-time passcode `U` ➝ _`h`_`(W(`_`U`_`))`
6. host compares the incoming _`f`_`(`_`r`_`′,` _`h`_`(W′))` to the calculated _`f`_`(`_`r`_`, h(W(`_`U`_`)))`



![](https://t3764800.p.clickup-attachments.com/t3764800/f2ac0718-f72b-4cf6-9fa5-67fef167b6b5/Screen%20Shot%202023-11-05%20at%208.39.15%20PM.png)

## Static Biometric Protocol

Figure 3.13c is an example of a user authentication protocol using a static biometric. As before, the user transmits an ID to the host, which responds with a random num- ber _r_ and, in this case, the identifier for an encryption _E_(). On the user side is a client system that controls a biometric device. The system generates a biometric template _BT_′ from the user’s biometric _B_′ and returns the ciphertext _E_(_r_′, _D_′, _BT_′), where _D_′ identifies this particular biometric device. The host decrypts the incoming message to recover the three transmitted parameters and compares these to locally stored values. For a match, the host must find _r_′ = _r_. Also, the matching score between _BT_′ and the stored template must exceed a predefined threshold. Finally, the host provides a simple authentication of the biometric capture device by comparing the incoming device ID to a list of registered devices at the host database.



![](https://t3764800.p.clickup-attachments.com/t3764800/6a676cbc-d73f-4727-a6a4-e31814872981/image.png)

## Dynamic Biometric Protocol

Figure 3.13d is an example of a user authentication protocol using a dynamic biometric. The principal difference from the case of a stable biometric is that the host pro- vides a random sequence as well as a random number as a challenge. The sequence challenge is a sequence of numbers, characters, or words. The human user at the client end must then vocalize (speaker verification), type (keyboard dynamics verification), or write (handwriting verification) the sequence to generate a biometric signal _BS_′(_x_′). The client side encrypts the biometric signal and the random number. At the host side, the incoming message is decrypted. The incoming random number _r_′ must be an exact match to the random number that was originally used as a challenge _(r)._ In addition, the host generates a comparison based on the incoming biometric signal _BS_′(_x_′), the stored template _BT_(_U_) for this user and the original signal _x._ If the comparison value exceeds a predefined threshold, the user is authenticated. ![](https://t3764800.p.clickup-attachments.com/t3764800/2d7709cc-2587-4bcf-8f50-41661a3ccd74/image.png)



Figure 3.13d is an example of a user authentication protocol using a dynamic biometric. The principal difference from the case of a stable biometric is that the host pro- vides a random sequence as well as a random number as a challenge. The sequence challenge is a sequence of numbers, characters, or words. The human user at the client end must then vocalize (speaker verification), type (keyboard dynamics verification), or write (handwriting verification) the sequence to generate a biometric signal _BS_′(_x_′). The client side encrypts the biometric signal and the random number. At the host side, the incoming message is decrypted. The incoming random number _r_′ must be an exact match to the random number that was originally used as a challenge _(r)._ In addition, the host generates a comparison based on the incoming biometric signal _BS_′(_x_′), the stored template _BT_(_U_) for this user and the original signal _x._ If the comparison value exceeds a predefined threshold, the user is authenticated. ![](https://t3764800.p.clickup-attachments.com/t3764800/2d7709cc-2587-4bcf-8f50-41661a3ccd74/image.png)



# **3.6  Security Issues for User Authentication**

*   Client attacks（**客戶端攻擊**）: masquerade as a legitimate user（**偽裝成合法用戶**）
    *   Guessing, exhaustive search, and false match （猜測、窮舉搜索和錯誤匹配）
    *   Countermeasures: strong passwords and limited attempts （強密碼和有限的嘗試次數）
*   Host attacks（**主機攻擊**）: steals the user file where passwords, token passcodes, or biometric templates are stored （**竊取存儲密碼、token密碼或生物特徵模板的用戶文件**）
    *   Theft of plaintext, passcode, and template (竊取明文、密碼和模板)
    *   Countermeasures: strong access control (強訪問控制)
*   Eavesdropping (**竊聽**)
    *   Shoulder surfing, keystroke logging, copying biometric (肩膀衝浪、擊鍵記錄、複製生物特徵)
    *   Countermeasures: multifactor authentication and anomaly detection (多因素身份驗證和異常檢測)
*   Relay(**中繼**): repeats a previously captured user response (**重複以前捕獲的用戶響應**)
    *   Replays stolen password, passcode, and biometric template(重播被竊的密碼、密碼和生物特徵模板)
    *   Countermeasures: a random number in [challenge-response protocols](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4042?block=block-32267149-9624-42dc-ad63-4f2e9ae29f58) (挑戰-響應協議中的隨機數)
*   Trojan horse(**木馬**): installation of rogue client or capture device (**安裝惡意客戶端或捕獲設備**)
    *   e.g., rogue ATM or credit card scanner(惡意 ATM 或信用卡掃描儀)
    *   Countermeasures: authentication of client or capture device within trusted security perimeter (在受信任的安全範圍內對客戶端或捕獲設備進行身份驗證)
*   Denial of service (**服務拒絕**): lockout by multiple failed authentications (**多次身份驗證失敗導致鎖定**)
    *   Countermeasures: multifactor with token (多因素 with token)



* * *

# **3.7  Practical Application: An Iris Biometric System**

> Teacher doesn't teach this section

# **3.8  Case Study: Security Problems for ATM Systems**

> Teacher doesn't teach this section

# **3.9  Key Terms, Review Questions, and Problems**

Here are the answers to your questions:

**3.1 In general terms, what are four means of authenticating a user’s identity?**

The four means of authenticating a user's identity are:

*   **Knowledge-based authentication:** This type of authentication relies on the user knowing something, such as a password, PIN, or security question.
*   **Token-based authentication:** This type of authentication relies on the user having something, such as a smart card or security token.
*   **Biometric authentication:** This type of authentication relies on the user's unique physical characteristics, such as fingerprints, facial features, or voice patterns.
*   **Multi-factor authentication:** This type of authentication combines two or more of the above authentication methods.



**3.2 List and briefly describe the principal threats to the secrecy of passwords.**

The principal threats to the secrecy of passwords are:

*   **Weak passwords:** Passwords that are easy to guess, such as "password" or "123456", are more likely to be compromised.
*   **Password reuse:** If a user reuses the same password for multiple accounts, if one account is compromised, all of the user's accounts are at risk.
*   **Phishing attacks:** Phishing attacks trick users into revealing their passwords by sending them fake emails or websites that look like legitimate ones.
*   **Malware:** Malware can be used to steal passwords from infected devices.



**3.3 What is the significance of a shadow password file?**

A shadow password file is a file that stores the encrypted passwords of users. The shadow password file is not accessible to users, which makes it more difficult for attackers to steal passwords.



**3.4 Explain how the proactive password checker approach can improve password security.**

A proactive password checker is a tool that can be used to check passwords for strength and complexity. Proactive password checkers can help users to choose strong passwords and can also be used to identify and block weak passwords.



**3.5 How can we classify the authentication protocols used with smart tokens?**

Authentication protocols used with smart tokens can be classified into two main categories:

*   **Challenge-response protocols:** These protocols require the smart token to generate a response to a challenge from the server.
*   **Static password protocols:** These protocols require the smart token to store a static password that is used to authenticate the user.



**3.6 List and briefly describe the principal physical characteristics used for biometric identification.**

The principal physical characteristics used for biometric identification are:

*   **Fingerprints:** Fingerprints are unique to each individual and can be used to identify users.
*   **Facial features:** Facial features can be used to identify users, but they are not as unique as fingerprints.
*   **Voice patterns:** Voice patterns can be used to identify users, but they are not as reliable as fingerprints or facial features.



**3.7 In the context of biometric user authentication, explain the terms, enrollment, verification, and identification.**

*   **Enrollment:** The process of registering a user's biometric data with the system.
*   **Verification:** The process of comparing a user's biometric data to their enrolled data to verify their identity.
*   **Identification:** The process of comparing a user's biometric data to a database of known biometric data to identify the user.



**3.8 How does remote user authentication differ from local authentication? Which one raised more security threats?**

Remote user authentication is the process of authenticating a user over a network, such as the Internet. Local authentication is the process of authenticating a user on a local device, such as a computer or smartphone.

Remote user authentication raises more security threats than local authentication. This is because remote user authentication is more susceptible to attacks such as phishing and man-in-the-middle attacks.



**3.9 What is a Trojan horse attack?**

A Trojan horse attack is a type of malware that disguises itself as a legitimate program in order to trick users into installing it. Once installed, the Trojan horse can steal data, install other malware, or damage the user's computer.

I hope this answers your questions. Please let me know if you have any other questions.
