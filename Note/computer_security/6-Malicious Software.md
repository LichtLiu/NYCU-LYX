---
title: "Computer Security Principles and Practice"
permalink: /Computer-Security-Principles-and-Practice/6-Malicious-Software/
layout: default
---
# 6-Malicious Software

[https://www.youtube.com/watch?v=X-ezH6QTil4](https://www.youtube.com/watch?v=X-ezH6QTil4)



*   NIST \[SOUP13\] defines malware as:

> “A program that is inserted into a system, usually covertly, with the intent of compromising the **confidentiality**, **integrity**, or **availability** **(CIA)** of the victim’s data, applications, or operating system or otherwise annoying or disrupting the victim.”

\[SOUP13\] Souppaya, M., and Scarfone, K. _Guide to Malware Incident Prevention and Handling for Desktops and Laptops_. NIST Special Publication SP 800-83, July 2013.

###   

# **6.1  Types of Malicious Software (Malware)**

| **Name** | **Description** |
| ---| --- |
| Advanced Persistent Threat (APT) | Cybercrime directed at business and political targets, using a wide variety of intrusion technologies and malware, applied persistently and effectively to specific targets over an extended period, often attributed to state-sponsored organizations. |
| Adware | Advertising that is integrated into software. It can result in pop-up ads or redirection of a browser to a commercial site. |
| Attack kit | Set of tools for generating new malware automatically using a variety of supplied propagation and payload mechanisms. |
| Auto-rooter | Malicious hacker tools used to break into new machines remotely. |
| Backdoor (trapdoor) | Any mechanism that bypasses a normal security check; it may allow unauthorized access to functionality in a program, or onto a compromised system. |
| Downloaders | Code that installs other items on a machine that is under attack. It is normally included in the malware code first inserted on to a compromised system to then import a larger malware package. |
| Drive-by-download | An attack using code on a compromised website that exploits a browser vulnerability to attack a client system when the site is viewed. |
| Exploits | Code specific to a single vulnerability or set of vulnerabilities. |
| Flooders (DoS client) | Used to generate a large volume of data to attack networked computer systems, by carrying out some form of denial-of-service (DoS) attack. |
| Keyloggers | Captures keystrokes on a compromised system. |
| Logic bomb | Code inserted into malware by an intruder. A logic bomb lies dormant until a predefined condition is met; the code then triggers some payload. |
| Macro virus | A type of virus that uses macro or scripting code, typically embedded in a document or document template, and triggered when the document is viewed or edited, to run and replicate itself into other such documents. |
| Mobile code | Software (e.g., script and macro) that can be shipped unchanged to a heterogeneous collection of platforms and execute with identical semantics. |
| Rootkit | Set of hacker tools used after attacker has broken into a computer system and gained root-level access. |
| Spammer programs | Used to send large volumes of unwanted e-mail. |
| Spyware | Software that collects information from a computer and transmits it to another system by monitoring keystrokes, screen data, and/or network traffic; or by scanning files on the system for sensitive information. |
| Trojan horse | A computer program that appears to have a useful function, but also has a hidden and potentially malicious function that evades security mechanisms, sometimes by exploiting legitimate authorizations of a system entity that invokes it. |
| Virus | Malware that, when executed, tries to replicate itself into other executable machine or script code; when it succeeds, the code is said to be infected. When the infected code is executed, the virus also executes. |
| Worm | A computer program that can run independently and can propagate a complete working version of itself onto other hosts on a network, by exploiting software vulnerabilities in the target system, or using captured authorization credentials. |
| Zombie, bot | Program installed on an infected machine that is activated to launch attacks on other machines. |

## A Broad Classification of Malware

*   Propagation(繁殖): how it spreads or propagates to reach the desired targets
    *   Infection of existing content by viruses
        *   Subsequently spread to other systems
    *   Exploit of software vulnerabilities by worms or drive-by-downloads
        *   Allow the malware to replicate
    *   Social engineering attacks
        *   Convince users to bypass security mechanisms to install Trojans or to respond to phishing attacks
*   Payloads(附載): how it performs once a target is reached
    *   Corruption of system or data files
    *   Theft of service: make the system a zombie agent
    *   Theft of information
    *   Stealing/hiding its presence on the system



*   Independent?
    *   Need a host program: parasitic code such as viruses
    *   Independent, self-contained programs: worms, Trojans, and bots
*   Replicate?
    *   Yes: viruses and worms
    *   No: Trojans and spam e-mail
*   **blended attack**
    *   uses multiple methods of infection or propagation to maximize the speed of contagion and the severity of the attack (**使用多種感染或傳播方法以最大限度地提高傳染速度和攻擊的嚴重性**)



## Attack Kits

*   Malware development/deployment: considerable technical skills
    *   Early 1990s: virus-creation toolkits
    *   2000s: more general attack kits
*   Widely used toolkits: Zeus, Blackhole, Sakura, Phoenix, etc.
*   Toolkits: known as “crimeware”
    *   A variety of propagation mechanisms and payload modules
        *   Even novices can combine, select, and deploy
    *   A large number of new variants can be generated by attackers



## Attack Sources

*   Attacker change
    *   Individuals→more organized/dangerous attack sources (**攻擊者從個人（通常出於向同行展示其技術能力的動機）轉向更有組織和更危險的攻擊來源**)
    *   changing resource available and motivation behind the rise of malware
        *   A large underground economy: the sale of attack kits, access to compromised hosts, and stolen information (**一個大型地下經濟的發展，其中涉及攻擊工具包的銷售、對受感染主機的訪問以及被盜信息的銷售**)

![](https://t3764800.p.clickup-attachments.com/t3764800/c756afbd-1ec0-406f-b05b-7d6058d8e393/Screen%20Shot%202023-11-10%20at%205.00.18%20PM.png)

# **6.2  Advanced Persistent Threat**

Advanced Persistent Threat (APT) 是指由具有高技能和資源的組織或個人發起的長期、持續的攻擊。APT 攻擊的目標通常是敏感信息，例如企業機密、政府數據或國家安全信息。

*   Well-resourced, persistent threats
    *   Selected target, usually business or political
    *   Characteristics: careful target selection, persistent, and stealthy
    *   High profile attacks: RSA, APT1, Hydraq (Aurora), etc.
        *   e.g., exposing One of China's Cyber Espionage Units (video)
*   Advanced
    *   Using a wide variety of intrusion technologies and (custom) malware
    *   Components may not be technically advanced but are carefully selected
*   Persistent
    *   Over an extended period against the target: maximize the chance of success
    *   A variety of attacks may be progressively applied
        *   Until the target is compromised
*   Threats
    *   Organized, capable, and well-funded attackers→specifically chosen targets
    *   Active involvement of people in the process with automated attacks tools

### APT Attacks

*   Goals
    *   From: theft of intellectual property or data
    *   To: physical disruption of infrastructure
*   Techniques
    *   Social engineering, spear-phishing email, drive-by-downloads, etc.
*   Intent
    *   Infecting the target with sophisticated malware
        *   Multiple propagation mechanisms and payloads

# **6.3  Propagation—Infected Content—Viruses**

## The Nature of Viruses

### Viruses: Propagation via Infected Content

*   A piece of software: “infect” other programs (Virus**會附加到某些現有的可執行內容上**)
    *   Any type of executable content
    *   Modifying them to include a copy of the virus
    *   Replicating and going on to infect other content
    *   Easily spreading through network environments
*   Can do anything that the host program is permitted to do
    *   Executing secretly when the program is run
*   Specific to OS and hardware
    *   Taking advantage of their details and weaknesses



three states of a computer virus :

*   **Infection mechanism**
    *   Means by which a virus spreads or propagates
    *   Also referred to as the _infection vector_
*   Trigger
    *   Event or condition that determines when the payload is activated or delivered
    *   Sometimes known as _a logic bomb_
*   **Payload**
    1. What the virus does (besides spreading)
    2. May involve damage, or benign but noticeable activity



Virus lifetime:

*   **Dormant phase****(睡眠階段):** The virus is idle. The virus will eventually be activated by some event
    *   such as a date, the presence of another program or file, or the capacity of the disk exceeding some limit. Not all viruses have this stage.
*   **Propagation phase****(繁殖階段):**The virus places a copy of itself into other programs or into certain system areas on the disk. The copy may not be identical to the propagating version; viruses often morph to evade detection. Each infected program will now contain a clone of the virus, which will itself enter a propagation phase.
*   **Triggering phase****(觸發階段):** The virus is activated to perform the function for which it was intended. As with the dormant phase, the triggering phase can be caused by a variety of system events, including a count of the number of times that this copy of the virus has made copies of itself.
*   **Execution phase****(執行階段):** The function is performed. The function may be harmless, such as a message on the screen, or damaging, such as the destruction of pro- grams and data files.

![](https://t3764800.p.clickup-attachments.com/t3764800/341e24a9-2e27-47c9-87ca-83b541101a58/Screen%20Shot%202023-11-10%20at%206.15.02%20PM.png)

### A Simple Virus

*   This virus code, V, is prepended to infected programs
    *   Assume that the entry point to the program is the main action block
*   However, it is easily detected. Why?

![](https://t3764800.p.clickup-attachments.com/t3764800/0675d07e-09d7-4aa0-9ceb-e241b894cf6e/Screen%20Shot%202023-11-10%20at%206.17.41%20PM.png)

### A Compression Virus

![](https://t3764800.p.clickup-attachments.com/t3764800/c6a5f861-37ed-4b1b-af61-a25bec7f323a/Screen%20Shot%202023-11-10%20at%206.19.35%20PM.png)

#### Logic of the Compression Virus

![](https://t3764800.p.clickup-attachments.com/t3764800/d4607158-4880-4105-9648-33e410f2df73/Screen%20Shot%202023-11-10%20at%206.20.01%20PM.png)

## Macro and Scripting Viruses (巨集病毒)

### Macro and Scripting Viruses

*   Macro viruses infect scripting code used to support active content in a variety of user document types
    *   Very common in mid-1990s
    *   Platform independent; active content in commonly used apps
        *   e.g., macros in MS Word
    *   Infect documents (not executable portions of code)
        *   e.g., MS Office products
        *   e.g., Adobe PDF: embedded JavaScript in pdf (link)
    *   Easily spread
        1. **electronic mail**
    *   Traditional file system access controls are of limited use. Why?
        1. **Because macro viruses infect user documents rather than system programs, traditional file system access controls are of limited use in preventing their spread, since users are expected to modify them.**
*   Various anti-virus products: also developed tools against macro viruses
*   Microsoft: increased protection against macro viruses
    *   An optional macro virus protection, digital signature over macros

### Macro Virus Structure

*   Macro languages may have a similar syntax, but the details depend on apps
    *   e.g., a MS Word macro is different from an Excel macro
*   Either be saved with a document, or in a global template
*   Some macros are run automatically when certain actions occur
    *   e.g., macros can run when MS Word starts
    *   not just perform operations on the document content, but can read/write files, and call other apps
*   Melissa macro virus: a mass-mailing macro virus
    *   Targets: MS Word and Outlook-based systems
        *   Contained in the Document\_Open macro
    *   Damage: considerable network traffic
    *   Hiding: disabling the Macro menu and some related security features
        *   Harder for the user to stop or remove its operation
    *   Infection: (1) every subsequent documents opened in the system; (2) sending infected documents to other users via email



**Figure 6.1 Melissa Macro Virus Pseudo-code**

```powershell
macro Document_Open
    disable Macro menu and some macro security features
    if called from a user document
       copy macro code into Normal template file
    else
       copy macro code into user document being opened
    end if
    if registry key “Melissa” not present
       if Outlook is email client
          for first 50 addresses in address book
              send email to that address
              with currently infected document attached
          end for
      end if
        create registry key “Melissa”
   end if
   if minute in hour equals day of month
     insert text into document being opened
   end if
end macro
```

## Viruses Classification

two orthogonal axes:

1. the type of target the virus tries to infect
2. method the virus uses to conceal(隱蔽) itself from detection by users and anti-virus software.



### Virus Classifications (By Target)

*   Boot sector infector
    *   Infects a master boot record or boot record
    *   Spreads when a system is booted from the disk containing the virus
*   File infector
    *   Infects files that OS or shell considers to be executable
*   Macro virus
    *   Infects files with macro or scripting code that is interpreted by an app
*   Multipartite virus
    *   Infects files in multiple ways or multiple types of files



### Virus Classifications (By Concealment Strategy)

*   Encrypted virus
    *   Uses encryption to obscure its content
    *   A portion creates a random encryption key and encrypts the remainder of the virus
    *   When the virus replicates, a different random key is selected
*   Stealth virus (秘密病毒)
    *   Hides itself from detection by anti-virus software
        *   Using code mutation, compression, or rootkit techniques
*   Polymorphic virus (多形病毒)
    *   Creates replication copies that are functionally equivalent but have different bit patterns
        *   Using inserting superfluous instructions, encryption, etc.
    *   “signature” will vary with each copy
*   Metamorphic virus (變形病毒)
    *   Mutates(突變) with every infection
    *   Difference from Polymorphic ones: rewrites itself completely at each iteration
        *   Using multiple transformation techniques, etc.
    *   May change both behaviors and appearance



# **6.4  Propagation—Vulnerability Exploit—Worms**

*   Programs that actively seeks out more machines to infect（主動感染）
    *   Each infected machine: an automated launching pad for attacks on other machines
*   Some characteristics
    *   Exploiting software vulnerabilities in client or server programs
    *   Spreading: network connections, shared media (e.g., USB drives, CD/DVD), E-mails (in macro/script code)
    *   Upon activation, they may replicate and propagate again
*   First known implementation: Xerox Palo Alto Labs (early 1980s)



To replicate itself, a worm uses some means to access remote systems. These include the following, most of which are still seen in active use:

*   Electronic mail or instant messenger facility
    *   a copy of itself via email or an attachment via an instant message service
*   File sharing
    *   creating a copy of itself or infecting a file as a virus on removable media (USB drive)
    *   using auto-run mechanism by exploiting some software vulnerability
*   Remote execution capability
    *   A worm executes a copy of itself on another system
        *   using an explicit remote execution facility
        *   exploiting a program flaw(瑕疵) in a network service to subvert(破壞) its operations (as we will discuss in Chapters 10 and 11).
*   Remote file access or transfer capability
    *   uses a remote file access or transfer service to another system to copy itself from one system to the other
*   Remote login capability
    *   A worm logs onto a remote system as a user and then uses commands to copy itself from one system to the other, where it then executes.



*   [same phases as a computer virus](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4622?block=block-e4279db5-f01d-4e6b-b161-e880b3519ff1): dormant, propagation, triggering, and execution
    *   propagation phase
        *   Search for appropriate access mechanisms on other systems to infect
            *   examining host tables, address books, buddy lists, trusted peers, and other similar repositories of remote system access details
    *   Use the access mechanisms found to transfer a copy of itself to the remote system, and cause the copy to be run.

## Target Discovery

*   Scanning (or fingerprinting)
    *   1st function in the propagation phase for a network worm
    *   search for other systems to infect
*   Scanning strategies
    *   Random
        *   Each compromised host probes(探索) random addresses in the IP address space, using a different seed
        *   high volume of Internet traffic
    *   Hit-list
        *   compiles a long list of potential vulnerable machines (**編制一份潛在易受攻擊機器的主機清單**)
        *   slow process done over a long period to avoid detection that an attack (**長時間才能完成的緩慢過程，以避免被發現正在進行攻擊**)
        *   Once the list is compiled, attacker begins infecting machines on the list (**編制完列表後，攻擊者將開始感染列表中的機器)**
        *   Each infected machine is provided with a portion of the list to scan (**每個受感染的機器都會獲得一份要掃描的主機列表**)

> short scanning period ➝ difficult to detect

*       *   Topological
        *   uses information contained on an infected victim machine to find more hosts to scan (**用受感染受害者機器上包含的信息來查找更多要掃描的主機)**
*       *   Local subnet
        *   If a host can be infected behind a firewall, that host then looks for targets in its own local network (**如果主機可以在防火牆後面被感染，則該主機將在其自己的本地網絡中搜索目標)**



## Worm Propagation Model

> teacher doesn't teach this section

## The Morris Worm

*   Earliest significant worm infection
    *   Released by Robert Morris in 1988
*   Designed to spread on UNIX systems
    *   Attempted to crack local password file to use login/password to logon to other systems
    *   Exploited a bug in the finger protocol which reports the whereabouts of a remote user
    *   Exploited a trapdoor in the debug option of the remote process that receives and sends mail
*   Infection steps
    *   Successful communication with the system shell (command interpreter)
    *   Execute a short bootstrap program through the shell
    *   The bootstrap program calls back the parent program and downloads the remainder of the worm
    *   Execute the new worm
*   

## A Brief History of Worm Attacks

| **Melissa** | **1998** | **e-mail worm: propagated to all of the email addresses known to the infected host; took only three days to infect over 100,000 computers** |
| ---| ---| --- |
| **Code Red**<br> | **July 2001**<br> | **exploited a security hole in the Microsoft Internet Information Server (IIS) DDoS attacks against a government website by flooding**<br>**Infected nearly 360,000 servers in 14 hours** |
| **Code Red II**<br> | **August 2001**<br> | **Installed a backdoor for a hacker to remotely execute commands** |
| **Nimda**<br> | **September 2001**<br> | **had worm, virus and mobile code characteristics**<br>**spread using e-mail, Windows shares, Web servers, Web clients, backdoors** |
| **SQL Slammer**<br> | **Early 2003**<br> | **exploited a buffer overflow vulnerability in MS SQL server**<br>**compact and spread rapidly: infected 90% of vulnerable hosts within 10 mins** |
| **Sobig.F**<br> | **Late 2003**<br> | **exploited open proxy servers to turn infected machines into spam engines produced more than one million copies of itself within the first 24 hours** |
| **Mydoom**<br> | **2004**<br> | **mass-mailing e-mail worm**<br>**installed a backdoor in infected machines replicated up to 1,000 times per minute** |
| **Warezov**<br><br> | **2006**<br> | **(1) creates executables in system directories; (2) sends itself as an e-mail attachment; (3) can disable security related products and updating capability**<br> |
| **Conficker (Downadup)**<br> | **November 2008**<br> | **exploits a Windows buffer overflow vulnerability most widespread infection since SQL Slammer**<br> |
| **Stuxnet**<br> | **2010**<br> | **restricted rate of spread to reduce chance of detection**<br>**targeted industrial control systems (Iranian nuclear program)**<br>**propagation: USB drives, network file shares, zero-day vulnerability exploits**<br>**1st serious use of a cyberwarfare weapon against a nations physical infrastructure** |
| **Duqu**<br> | **2011**<br> | **Used code related to Stuxnet Targeted the Iranian nuclear program** |
| **Flame family**<br> | **2012**<br> | **Targeted Middle-Eastern countries**<br>**Very successful infection strategies: infected many countries, including the systems physically isolated from Internet** |
| **WannaCry**<br> | **2017**<br> | **Ransomware attack: encrypted files; demanded a ransom payment to recover Very fast propagation: infected > 100,000 systems over a period of hours to days Exploited a vulnerability in the SMB file sharing service on unpatched Windows** |

![](https://t3764800.p.clickup-attachments.com/t3764800/5f43fda2-3ab9-46af-9406-d9f43903d48e/Screen%20Shot%202023-11-10%20at%2011.02.10%20PM.png)

## State of Worm Technology

*   Multiplatform
    *   A variety of platforms (Windows, UNIX); macro or scripting languages supported in popular document types
*   Multi-exploit
    *   Exploits against Web servers, browsers, e-mail, file sharing, other network-based apps, etc.
*   Ultrafast spreading
    *   Optimize the spread rate; locate as many vulnerable machines as possible in a short time period
*   Polymorphic (多形)
    *   Each copy has new code generated on the fly using functionally equivalent instructions and encryption techniques
*   Metamorphic (變形)
    *   Unleashed behavior patterns at different stages of propagation
*   Transport vehicles
    *   Worms can rapidly compromise a large number of systems
    *   Ideal for spreading a wide variety of malicious payloads, such as DDoS bots
*   Zero-day exploit
    *   In 2015, 54 zero-day exploits were discovered and exploited
    *   Many of these were in common computer and mobile software

## Mobile Code (行動程式碼)

*   Programs that can be shipped unchanged to a variety of platforms (**可移植到各種平台的不變程序**)
    *   Cross-platform: transmitted from a remote system to a local system and then executed on the local system
*   Popular vehicles include Java applets, Active X, JavaScript and VBScript➔since they are cross-platform
*   Common methods of using mobile code for malicious operations
    *   Interactive and dynamic websites, e-mail attachments, and downloads from untrusted sites or of untrusted software

Reference: [https://owasp.org/www-community/vulnerabilities/Unsafe\_Mobile\_Code](https://owasp.org/www-community/vulnerabilities/Unsafe_Mobile_Code)

## Mobile Phone Worms

*   Cabir worm: first appeared on mobile phones (2004)
    *   Communicated through Bluetooth or multimedia messaging service (MMS)
    *   Early mobile worms targeted Symbian, but recent ones target Android and iPhone
    *   Can completely disable the phone, delete data on the phone, or force the device to send costly messages
*   CommWarrior worm
    *   通過藍牙：replicates by means of Bluetooth to other phones in the receiving area
    *   通過 MMS 消息：sends itself as an MMS file to numbers in the phone’s address book and in automatic replies to incoming text messages and MMS messages
    *   copies itself to the removable memory card and inserts itself into the program installation files on the phone

## Client-Side Vulnerabilities and Drive-by-Downloads

*   Exploits browser vulnerabilities to download and installs malware on the system when the user views a Web page controlled by the attacker
*   In most cases, they do not actively propagate
*   Spread when users visit the malicious Web page
*   Multiple vulnerabilities in the Adobe Flash Player and Java plugins have been exploited over many years

## Clickjacking

*   Also known as a user-interface (UI) redress attack
    *   to collect an infected user’s clicks
    *   Typically, using multiple transparent or opaque layers
*   Keystrokes can be hijacked
    *   A user can be led to believe they are typing in the password to their email or bank account
    *   But, are instead typing into an invisible frame controlled by the attacker
        ![](https://t3764800.p.clickup-attachments.com/t3764800/6b36d898-74e8-4068-b5dc-0d317dc7b145/Screen%20Shot%202023-11-11%20at%2012.41.58%20AM.png)

# **6.5  Propagation—Social Engineering—Spam E-Mail, Trojans**

*   “Tricking” users to assist in the compromise of their own systems

## Spam (Unsolicited Bulk) E-Mail

*   Unsolicited bulk e-mail (未經請求的大量email)
    *   imposes significant costs on both network infrastructure and users.
*   Significant carrier of malware (**垃圾郵件是惡意軟體的重要載體**)
*   Used for phishing attacks

## Trojan Horses

特洛伊木馬是一種惡意軟體，它看起來像是合法的軟體或有用的工具，但實際上執行了有害的操作。特洛伊木馬可以用來獲取敏感信息、安裝間諜軟體或執行其他惡意活動。

*   Program or utility containing harmful hidden code
*   Used to accomplish functions that the attacker could not accomplish directly
*   Trojan horses are malicious programs that appear to be useful or benign but actually perform harmful actions when executed.
*   Trojan horses can be used to gain access to sensitive information, install spyware, or perform other malicious activities.
*   Trojan horses can be disguised as legitimate software or exploit software vulnerabilities to install themselves without user consent. (假扮成合法軟體)
*   Tech support scams are a growing problem involving call centers that trick users into installing Trojan malware on their systems.



特洛伊木馬可以以多種方式傳播，包括：

*   電子郵件附件：攻擊者可能會將特洛伊木馬作為電子郵件附件發送給受害者。當受害者打開附件時，特洛伊木馬就會被安裝在受害者的計算機上。
*   惡意網站：攻擊者可能會在惡意網站上托管特洛伊木馬。當受害者訪問該網站時，特洛伊木馬就會被下載到受害者的計算機上。
*   惡意軟體更新：攻擊者可能會偽裝成合法的軟體更新，但實際上包含特洛伊木馬。當受害者安裝該更新時，特洛伊木馬就會被安裝在受害者的計算機上。

特洛伊木馬可以執行各種有害操作，包括：

*   竊取敏感信息，例如密碼、信用卡號碼和個人身份信息。
*   安裝間諜軟體，以監視受害者的活動。
*   發送垃圾郵件或其他惡意電子郵件。
*   控制受害者的計算機，以執行其他惡意活動。



## Mobile Phone Trojans

*   First appeared in 2004 (Skuller)
*   Target is the smartphone (Symbian, Android, and Apple phones.)
*   Smartphones are an attractive target for criminals and other attackers because they contain valuable personal information.
*   The number of vulnerabilities discovered in smartphones and the number of malware families targeting them have both increased steadily in recent years.
*   iPhone Trojans often target "jail-broken" phones and are distributed via unofficial sites. However, some versions of the iPhone O/S have contained vulnerabilities that could be exploited by malware.
*   In 2015, XcodeGhost malware was discovered in a number of legitimate Apple Store apps. This malware was installed without the knowledge or consent of the app developers.

# **6.6  Payload—System Corruption**

payload : what actions it will take on this system

*   Malware can have different payloads
    *   spreading
    *   performing covert actions for the attacker.
*   payloads result in
    *   data destruction, display unwanted messages, or inflict real-world damage on the system, targeting the integrity of software, hardware, or user data. These actions are triggered by specific conditions.



## Data Destruction and Ransomware (勒索病毒)

*   Virus
    *   Chernobyl: Windows-95 and 98 virus; first seen in 1998
    *   Infected executable files and corrupted the entire file system (a date is reached)
*   Worm
    *   Klez: mass-mailing worm infecting Windows-95 to XP systems; first seen in 2001
    *   On trigger dates (13th of several months each year), caused files on the hard drive to become empty
*   Ransomware
    *   PC Cyborg Trojan (1989)
        *   encrypts data using public-key cryptography with larger key sizes, making it impossible to crack without paying a ransom, and is a common type of malware spread through drive-by downloads or spam emails.
    *   WannaCry (2017)
        *   infected numerous systems in multiple countries in May 2017, encrypting specific file types and demanding ransom payments in Bitcoins for recovery.
    *   Encrypted the user’s data and demands payment for recovery
*   Recovery:
    *   good backups
    *   incident response
    *   disaster recovery plan



## Real-World Damage

*   Causes damage to physical equipment
    *   Chernobyl virus not only corrupted data, but also rewrote the BIOS code
    *   Stuxnet worm targets industrial control system software→may drive the controlled equipment outside its normal operating range
    *   Critical infrastructure: e.g., disrupted [Ukrainian power systems in 2015](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4622?block=block-8f12d156-1299-446f-bc6b-17089a4bf995) \[SYMA16\]

### Ukraine Power Grid Cyberattack

*   1st known successful cyberattack on a power grid
    *   Damage: up to 73 MWh of electricity was not supplied (0.015% of daily in Ukraine)
    *   Attributed to Sandworm (Russian advanced persistent threat group)
*   Complex cyberattack
    *   Spear-phishing emails with BlackEnergy malware
    *   Seizing SCADA under control, remotely switching substations off
        *   SCADA: Supervisory Control And Data Acquisition (監督控制和資料取得)
    *   Disabling/destroying IT infrastructure components (power supplies, modems, etc.)
    *   Destruction of files stored on servers with the KillDisk malware
    *   DoS attack on call-center to deny consumers up-to-date information

## Logic Bomb

*   Code embedded in the malware that is set to “explode” when certain conditions are met
    *   May alter or delete data or entire files, cause a machine to halt, etc.
    *   Tim Lloyd was convicted of setting a logic bomb at Omega Engineering, resulting in over 10 _million losses_,



# **6.7  Payload—Attack Agent—Zombie, Bots**

*   Takes over another Internet attached computer and uses that computer to launch or manage attacks

## Uses of Bots

*   _Botnet_ – collection of bots capable of acting in a coordinated manner
*   Uses:
    *   Distributed denial-of-service (DDoS) attacks
        *   cause a loss of service to users and can be examined in Chapter 7
    *   Spamming
        *   used to send massive amounts of spam emails
    *   Sniffing traffic
        *   use a packet sniffer to watch for interesting clear-text data passing by a compromised machine
    *   Keylogging
        *   capture keystrokes on infected machines to retrieve sensitive information
    *   Spreading new malware
        *   used to spread new malware by downloading and executing files via HTTP or FTP, allowing for fast spreading and causing more harm.
    *   Installing advertisement add-ons and browser helper objects (BHOs)
        *   automate clicks on advertisements, allowing the operator of a fake website to profit from hosting companies that pay for ad clicks. This process can be further enhanced by hijacking the start-page of compromised machines.
    *   Attacking IRC(nternet Relay Chat) chat networks
        *   **Clone attacks:**
            *   botnet controller orders each bot in the botnet to connect to the victim IRC network and create a large number of clones. These clones then all attempt to connect to the victim network at the same time, overwhelming the network and causing it to crash.
        *   **Channel flooding**
        *   **Denial-of-service attacks (DDoS)**
    *   Manipulating online polls/games
        *   exploiting the fact that each bot has a distinct IP address and can thus cast votes or perform actions that appear to come from different real users

## Remote Control Facility

*   Distinguishes a bot from a worm (**區分機器人和蠕蟲**)
    *   Worm propagates itself and activates itself (蠕蟲會自我繁殖並自行激活)
    *   Bot is initially controlled from some central facility (機器人最初由某個中央機構控制)
*   Typical means of implementation: an IRC (Internet Relay Chat) server
    *   Joining a specific channel on this server and treat incoming messages as commands (加入此服務器上的特定頻道並將收到的消息視為命令)
    *   More recent botnets use covert communication channels via protocols such as HTTP (近期機器人網絡使用HTTP等協議通過隱蔽的通信渠道)
    *   Distributed control mechanisms use P2P protocols to avoid a single point of failure (Distributed control mechanisms使用P2P協議來避免單點故障)

# **6.8  Payload—Information Theft—Keyloggers, Phishing, Spyware**

*   malware often collects data stored on infected systems to use for malicious purposes.
*   login credentials, documents, and system configuration details.
*   The attacker can use this information to impersonate(扮演) the victim, access their accounts, or steal sensitive data.

## Credential Theft, Keyloggers, and Spyware

### Keylogger

*       *   Captures keystrokes to allow attackers to monitor sensitive information
    *   Uses some form of filtering mechanism that only returns information close to keywords
        *   (e.g., “login” or “password” or “paypal.com”)

#### Privacy Leakage of InputConnection Interface in Android

*   Vulnerability: input channel hijacking
*   Threat: user input can be leaked to a web page rendered by WebView ![](https://t3764800.p.clickup-attachments.com/t3764800/d17139fd-145e-4845-bb5a-8e8f3975f6ca/Screen%20Shot%202023-11-11%20at%204.05.28%20PM.png)![](https://t3764800.p.clickup-attachments.com/t3764800/4c282cb1-ca11-4275-934b-d92b9ff7e6e4/Screen%20Shot%202023-11-11%20at%204.05.58%20PM.png)

> Chi-Yu Li, Hsin-Yi Wang, Wei-Ching Wang, Chun-Ying Huang, “Privacy Leakage and Protection of InputConnection Interface in Android,” IEEE TNSM, 2021.

### Spyware

*       *   Subverts the compromised machine to allow monitoring of activities on the system (顛覆受感染的機器以允許監控系統上的活動)
    *   Monitors history and content of browsing activity(監視瀏覽活動的歷史記錄和內容)
    *   Redirects certain web page requests to fake sites (將某些網頁請求重定向到虛假網站)
    *   Dynamically modifies data exchanged between the browser and certain web sites (動態修改瀏覽器和某些網站之間交換的數據)

## Phishing and Identity Theft

### Phishing

*   exploits social engineering to leverage the user’s trust by masquerading as communication from a trusted source
*   e.g., includes a URL in a spam e-mail that links to a fake Web site
    *   Mimicking the login page of a banking, gaming, or similar site
*   e.g., deceives the user that some urgent action is required



### Spear-phishing

*   Recipients are carefully researched by the attacker
*   E-mail is crafted to specifically suit its recipient
*   Often quoting a range of information to convince them of its authenticity



## Reconnaissance, Espionage, and Data Exfiltration

*   Credential theft (憑證竊取)and identity theft(身份盜竊) are common forms of reconnaissance(偵查) payloads used by attackers to obtain desired information.
*   Operation Aurora in 2009 and the Stuxnet worm in 2010 are examples of attacks that targeted source code repositories and captured hardware and software configuration details.(針對源代碼儲存庫並捕獲硬件和軟件配置詳細信息的攻擊示例。)
*   Insider leaks, such as the Wikileaks and Edward Snowden cases, involved individuals exploiting their legitimate access rights for ideological reasons.(內部洩漏，例如Wikileaks和Edward Snowden案件，涉及個人出于意識形態原因濫用其合法訪問權限。)
*   The Ashley Madison and Panama Papers leaks, on the other hand, were carried out by outside hackers targeting poorly secured systems. (另一方面，Ashley Madison和巴拿馬文件洩漏是由outside hackers對安全保護不佳的系統的進行的。)



# **6.9 Payload—Stealthing—Backdoors, Rootkits**

## Backdoor

*   A secret entry point into a program: allowing the attacker to gain access and bypass the security access procedures
*   Maintenance hook: a backdoor used by programmers to debug and test programs
    *   Usually implemented as a network service listening on some non-standard port
*   Difficult to implement OS controls for backdoors in apps (難以在應用程序中實施 OS 控制以防範後門)
*   Security measures must focus on
    *   Program development and software update activities (app更新)
        *   Programs that wish to offer a network service

## Rootkit

*   A set of hidden programs installed on a system to maintain covert access to the system with root privileges (一套隱藏在系統上的程序，用於以 root 權限保持對系統的秘密訪問)
*   Root access: attacker has complete control of the system, and alters the system’s standard functionality in a malicious and stealthy way (攻擊者對系統擁有完全的控制權，並以惡意和隱秘的方式更改系統的標準功能)
*   Hides by subverting the mechanisms that monitor and report on the processes, files, and registries on a computer (通過破壞監視和報告計算機上進程，文件和註冊表的機制來隱藏)



*   Rootkit Classification Characteristics
    *   **Persistent**: activates each time the system boots
    *   **Memory based**: cannot survive a reboot(no persistent code, it is only in memory), but can be harder to detect
    *   **User mode**: intercepts calls to APIs and modifies returned results (攔截對 API 的調用並修改返回的結果)
    *   **Kernel mode**: can intercept calls to native APIs in kernel mode (可以攔截內核模式下對本機 API 的調用)
    *   **Virtual machine based**: installs a lightweight virtual machine monitor, and then runs the OS in a virtual machine above it
    *   **External mode**: located outside the normal operation mode (e.g., in BIOS or system management mode, it can directly access hardware ) (位於正常操作模式之外（例如，在 BIOS 或系統管理模式中, 可以直接存取硬體））



## Kernel Mode Rootkits

*   early rootkit: work in user mode
*   Kernel mode rootkit: next generation(work in kernel mode)
    *   Making changes inside the kernel and co-existing with the OS code ➔ Make their detection much harder
    *   A primary target: system calls
    *   three techniques that can be used to change system calls:
        *   **Modify the system call table(**修改系統調用表**)****:** The attacker modifies selected syscall addresses stored in the system call table. This enables the rootkit to direct a system call away from the legitimate routine to the rootkit’s replacement. (攻擊者修改存儲在系統調用表中的所選 syscall 地址。這使 rootkit 能夠將系統調用從合法的例程轉移到 rootkit 的替換例程。)Figure 6.3 shows how the knark rootkit achieves this.
        *   **Modify system call table targets(**修改系統調用表目標**)****:** The attacker overwrites selected legitimate system call routines with malicious code. The system call table is not changed. (攻擊者使用惡意代碼覆蓋所選的合法系統調用例程)
        *   **Redirect the system call table(**重定向系統調用表**)****:** The attacker redirects references to the entire system call table to a new table in a new kernel memory location.
*   Example: system call table modification by the knark Rootkit

![](https://t3764800.p.clickup-attachments.com/t3764800/6f928cc9-dfb2-42f5-becc-6aeba32f88d1/Screen%20Shot%202023-11-11%20at%204.20.38%20PM.png)

## Virtual Machine and Other External Rootkits

# **6.10 Countermeasures**

*   known as “anti-virus” mechanisms

## Malware Countermeasure Approaches

*   What is the ideal solution?
    *   Prevention: do not allow malware to get into the system
    *   However, it is nearly impossible
*   NIST suggests four main elements of prevention
    *   Policy: e.g., having all patches installed
    *   Awareness: e.g., having a training course
    *   Vulnerability mitigation: e.g., disabling unused services
    *   Threat mitigation: e.g., having anti-virus/IDS software installed
*   If prevention fails:
    *   **Detection(偵測)****:** Once the infection has occurred, determine that it has occurred and locate the malware.
    *   **Identification(確認)****:** Once detection has been achieved, identify(確認) the specific malware that has infected the system.
    *   **Removal(去除)****:** Once the specific malware has been identified, remove all traces of malware virus from all infected systems so it cannot spread further.



*   requirements for effective malware countermeasures:
    *   Generality(通用性): handle a wide variety of attacks(處理各種攻擊)
    *   Timeliness(及時性): respond quickly→limit the number of infected programs (快速響應→限制受感染程序的數量)
    *   Resiliency(彈性): resistant to evasion techniques(抵抗逃避技術)
    *   Minimal DoS costs(最小的 DoS 成本): minimal reduction in capacity or service (最小化容量或服務的減少)
    *   Transparency(透明度): no modification to existing OSs, app software, hardware (不修改現有操作系統、應用程序軟體、硬體)
    *   Global and local coverage(全球和本地覆蓋範圍): against attack sources both from outside and inside the network (針對來自網絡外部和內部的攻擊源)

## Host-Based Scanners and Signature-Based Anti-Virus

*   First generation: simple scanners (簡單的掃描器)
    *   Require a malware signature to identify the malware (需要惡意軟件簽名來識別惡意軟件)
    *   Limited to the detection of known malware (需要惡意軟件簽名來識別惡意軟件)
*   Second generation: heuristic scanners (需要惡意軟件簽名來識別惡意軟件)
    *   Execute the questionable program in VM or decompile them and analyze source codes (在虛擬機中執行可疑程序或反編譯它們並分析源代碼)
    *   Another approach is integrity checking (另一種方法是完整性檢查)
*   Third generation: activity traps (活動陷阱)
    *   Memory-resident programs that identify malware by its actions rather than its structure in an infected program (駐留在內存中的程序，通過分析受感染程序中的操作而不是其結構來識別惡意軟件)
*   Fourth generation: full-featured protection (全功能保護)
    *   Packages consisting of a variety of anti-virus techniques used in conjunction (結合使用多種防病毒技術的軟件包)
    *   Include scanning and activity trap components and access control capability - e.g., using firewall to limit the malware propagation (包括掃描和活動陷阱組件以及訪問控制功能 - 例如，使用防火牆限制惡意軟件傳播)



*   Generic decryption (GD)
    *   通用解密 (GD) 是一種反病毒技術，旨在檢測和刪除未知惡意軟件。GD 通過分析惡意軟件的行為而不是其特徵來工作。這使其能夠檢測尚未被簽名的惡意軟件。
    *   detect the most complex polymorphic viruses and malware
    *   based on the behavior: when a file containing a polymorphic virus is executed, the virus must **_decrypt_** itself to activate
    *   executable files are run through a GD scanner
        *   Including CPU emulator, virus signature scanner, emulation control module, etc.
    *   the emulator begins interpreting instructions in the target code, one at a time ◼ Searching for decryption routines
    *   Difficult design issue?
        *   To determine how long to run each interpretation

### Host-based dynamic Malware analysis

*   Host-based Behavior-Blocking software
    *   Integrate with the OS and monitors program behavior in real time for malicious actions
    *   Block potentially malicious actions, before they have a chance to affect the system
    *   Block suspicious software in real time, so it has an advantage over anti-virus detection techniques such as fingerprinting or heuristics
    *   Drawback? Malicious codes must run on the target before all its behaviors can be identified
        *   It can cause harm before it has been detected



*       *   Monitored behaviors can include the following:
        *   Attempts to open, view, delete, and/or modify files
        *   Attempts to format disk drives and other unrecoverable disk operations
        *   Modifications to the logic of executable files or macros
        *   Modification of critical system settings, such as start-up settings
        *   Scripting of e-mail and instant messaging clients to send executable content
        *   Initiation of network communications

### **Spyware Detection and Removal**

Spyware is software that secretly installs itself on a computer without the user's knowledge or consent to collect personal information or track online activity.

*   Spyware can be used to steal sensitive information, track browsing habits, and install other malware.
*   Anti-spyware software is designed to detect and remove spyware from a computer.
*   Common signs of spyware infection include decreased system performance, pop-up ads, and unknown applications running in the background.

### **Rootkit Countermeasures**

Rootkits are a type of malware that hides itself deep within a computer's system, granting attackers unauthorized control.

*   Rootkits can be extremely difficult to detect and remove due to their stealthy nature.
*   Strong passwords, two-factor authentication, and up-to-date software can help protect against rootkit infections.
*   Specialized anti-rootkit tools are often necessary to eliminate rootkits effectively.

###   

## Perimeter Scanning Approaches

Perimeter scanning involves monitoring a network's borders to identify and block potential threats.

*   Firewalls, intrusion detection systems (IDS), and intrusion prevention systems (IPS) are commonly used tools for perimeter scanning.
*   Scanning all incoming and outgoing traffic is effective but resource-intensive.
*   Focusing on specific traffic types, such as those from suspicious IP addresses, can be more efficient but less comprehensive.



## Distributed Intelligence Gathering Approaches

Distributed Intelligence (DI) gathering involves collecting information from various sources, such as sensors, social media, and open-source intelligence (OSINT).

**Key Points:**

*   DI gathering provides a comprehensive view of threats and vulnerabilities across a wide range of sources.
*   Collected data can be analyzed to identify patterns, trends, and potential threats.
*   DI gathering is used for security analysis, market research, and social science research.



# **6.11 Key Terms, Review Questions, and Problems**

**6.1 What are three broad mechanisms that malware can use to propagate?**

1. **Replication:** Malware copies itself to other systems, often through email attachments, infected websites, or removable media.
2. **Exploitation:** Malware takes advantage of vulnerabilities in software to gain unauthorized access to a system.
3. **Social engineering:** Malware tricks users into installing it or revealing sensitive information.



**6.2 What are four broad categories of payloads that malware may carry?**

1. **Destructive:** Malware that damages or destroys data or systems.
2. **Data theft:** Malware that steals sensitive information, such as passwords or financial data.
3. **Disruptive:** Malware that disrupts normal operations, such as by launching denial-of-service attacks.
4. **Spyware:** Malware that collects information about users' activities without their knowledge or consent.



**6.3 What characteristics of an advanced persistent threat give it that name?**

1. **Stealth:** Advanced persistent threats (APTs) are designed to be stealthy and avoid detection.
2. **Targeted:** APTs are typically targeted at specific organizations or individuals.
3. **Resourceful:** APTs have access to significant resources and can adapt to changing security measures.
4. **Persistent:** APTs can maintain access to a system for extended periods of time.



**6.4 What are typical phases of operation of a virus or worm?**

1. **Infection:** The virus or worm infects a single system.
2. **Propagation:** The virus or worm replicates itself and spreads to other systems.
3. **Payload execution:** The virus or worm executes its payload, which may be destructive, disruptive, or data theft-related.



**6.5 What is a blended attack?**

A blended attack is an attack that combines multiple attack vectors, such as phishing emails with malicious attachments.



**6.6 What is the difference between a worm and a zombie?**

A worm is a type of malware that can replicate itself and spread to other systems without human intervention. A zombie is a computer that has been infected with malware and can be controlled remotely by an attacker.



**6.7 What does “fingerprinting” mean for network worms?**

Fingerprinting is the process of identifying a network worm by analyzing its code or behavior.



**6.8 What is a “drive-by-download” and how does it differ from a worm?**

A drive-by-download is a type of attack that exploits vulnerabilities in web browsers to install malware on a computer. Unlike a worm, a drive-by-download does not replicate itself.



**6.9 How does a Trojan enable malware to propagate? How common are Trojans on computer systems? Or on mobile platforms?**

Trojans enable malware to propagate by tricking users into installing them. Trojans are relatively common on both computer systems and mobile platforms.



**6.10 What is a “logic bomb”?**

A logic bomb is a type of malware that is triggered by a specific event, such as a date or a time.



**6.11 What is the difference between a backdoor, a bot, a keylogger, spyware, and a rootkit? Can they all be present in the same malware?**

*   **Backdoor:** A backdoor is a hidden entry point that allows an attacker to access a system without authorization.
*   **Bot:** A bot is a computer that has been infected with malware and can be controlled remotely by an attacker.
*   **Keylogger:** A keylogger is a type of malware that records the keystrokes of a user.
*   **Spyware:** Spyware is a type of malware that collects information about users' activities without their knowledge or consent.
*   **Rootkit:** A rootkit is a type of malware that hides itself deep within a computer's system, granting attackers unauthorized control.

Yes, all of these types of malware can be present in the same piece of malware.



**6.12 What is the difference between a “phishing” attack and a “spear-phishing” attack, particularly in terms of who the target may be?**

A phishing attack is a type of attack that attempts to trick users into revealing sensitive information, such as passwords or credit card numbers. Spear-phishing is a more targeted form of phishing that is directed at specific individuals or group
