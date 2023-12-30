---
title: "Computer Security Principles and Practice"
permalink: /Computer-Security-Principles-and-Practice/8-Intrusion-Detection/
layout: default
---
# 8-Intrusion Detection

# **8.1  Intruders**

*   Cyber criminals （凡罪者）
    *   Individuals or members of an organized crime group with a goal of financial reward
    *   Activities: identity theft, theft of financial credentials, data theft, data ransoming
    *   Meet to trade tips in underground forums (e.g., [DarkMarket.org](http://DarkMarket.org), [theftservices.com](http://theftservices.com))
*   Activists
    *   Individuals or members of a larger group of outsider attackers
        *   Skill level is often low
    *   Goals: promote and publicize their social or political causes （政治傾向）
    *   Activities: website defacement, DoS attacks, theft and distribution of data
*   State-sponsored organizations （政府支援組織）
    *   Groups of hackers sponsored by governments to conduct espionage（spy） or sabotage activities
    *   Known as APTs
    *   Widespread nature: from China to the USA, UK, and their intelligence allies
*   Others
    *   Hackers with motivations other than the above
    *   Classic hackers or crackers: motivated by technical challenge or by peer- group esteem and reputation (個人名聲)

### Three Skill Levels of Intruders

*   Apprentice (學徒)
    *   Hackers with minimal technical skill who primarily uses existing attack toolkits
    *   Known as “script-kiddies” （只會用工具或script）
    *   The easiest to defend against
*   Journeyman
    *   Hackers with sufficient technical skills to modify/extend attack toolkits
    *   Be able to use new vulnerabilities; may be able to locate new ones
    *   The changes in attack tools make identifying and defending harder
*   Master
    *   Hackers with high-level technical skills to discover new vulnerabilities
    *   Highest difficulty for defense

## Intruder Behavior

*   Target acquisition and information gathering
    *   Identifying and characterizing the target systems using publicly information
    *   Using network exploration tools to map target resources
    *   Examples
        *   Exploring corporate website for information on structure, personnel, key systems
        *   Gathering information on target network using DNS lookup tools (e.g., dig, host)
*   Initial access
    *   Exploiting a remote network vulnerability, guessing weak authentication credentials, or installing malware
    *   Examples
        *   Brute force to guess passwords
        *   Exploiting vulnerability in Web server to gain system access
        *   Sending spear-phishing e-mail to key people
*   Privilege escalation
    *   Increasing the privileges via a local access vulnerability
    *   Examples
        *   Exploiting any vulnerable app to gain elevated privileges
        *   Installing sniffers to capture administrator passwords
*   Information gathering or system exploit
    *   Accessing or modifying information or resources on the system
    *   Examples
        *   獲取password file破解
        *   Scanning files for desired information
*   Maintaining access
    *   Installing backdoors or other malicious software
    *   Enabling continued access after the initial attack
    *   Examples
        *   Installing rootkit with backdoor for later access
        *   Modifying or disabling anti-virus programs running on system
*   Covering tracks （隱藏足跡）
    *   Disabling or editing audit logs to remove evidence of attack activity
    *   Examples
        *   Using rootkit to hide files installed on system

![](https://t3764800.p.clickup-attachments.com/t3764800/298b5f52-d818-4501-846c-2c725c394990/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/e1edf2c3-8ace-4093-8ac4-d0ea78659762/image.png)

# **8.2  Intrusion Detection**

*   Definitions from Internet Security Glossary (RFC 2828)
    *   Security intrusion: unauthorized act of bypassing the security mechanisms of a system （未授權行為火跳過安全機制）
    *   Intrusion detection: a hardware or software function that gathers and analyzes information from various areas within a computer or a network to identify possible security intrusions

### **Three logical components**

*   **Sensors - collect data**
    *   network packets, log files, and system call traces
    *   Sensors collect and forward to the analyzer
*   **Analyzers - determine if intrusion has occurred**
    *   an indication that an intrusion has occurred
    *   output: evidence supporting the conclusion
*   **User interface - view output or control system behavior**

### Intrusion Detection System (IDS)

*   Host-based IDS (HIDS)
    *   Monitoring the characteristics of a single host and its events
*   Network-based IDS (NIDS)
    *   Monitoring network traffic and analyzing network, transport, and app protocols
*   Distributed or hybrid IDS
    *   Combining information from sensors, often both host and network-based, in a central analyzer

### Example: The Zeek Network Security Monitor

### ![](https://t3764800.p.clickup-attachments.com/t3764800/f02d00f6-cada-4d86-b4da-faa904c36118/image.png)

## Basic Principles

*   Another line of defense against intrusions
    *   Others: authentication, access control, and firewall
*   Based on the assumption: the behavior of the intruder differs from that of a legitimate user



1. **Rapid Response and Damage Mitigation:**
    *   Timely intrusion detection allows for quick identification and removal of intruders before they cause harm.
    *   Even if detection isn't immediate, earlier awareness minimizes damage and speeds up recovery.
2. **Deterrence:**
    *   The presence of an effective IDS can discourage potential intruders, acting as a preventive measure.
3. **Information Gathering for Enhanced Security:**
    *   IDSs collect valuable data about intrusion techniques, enabling the development of stronger prevention strategies.



*   **false positives:** authorized users are identified as intruders
    *   條件較鬆，不合法判斷成合法
*   **false negatives :** tight interpretation of intruder behavior
    *   條件較緊，合法判斷成不合法

![](https://t3764800.p.clickup-attachments.com/t3764800/8eaeddd5-02f8-45b7-a17d-83aec04509e7/image.png)

## The Base-Rate Fallacy

**Finding the right balance between detecting real intrusions and avoiding false alarms in (IDS) is a significant challenge due to the** **low base rate of actual intrusions compared to legitimate system usage****.**

**Further explanations:**

*   A high false alarm rate can lead to ignored alerts or wasted time investigating them, rendering the IDS ineffective.
*   Current IDS haven't effectively overcome the "base-rate fallacy," where a low frequency of real intrusions makes it difficult to distinguish them from legitimate activity.
*   Appendix I provides more details on the mathematical complexities behind this challenge.



## Requirements

*   Run continually with minimal human supervision.
*   Be fault tolerant in the sense that it must be able to recover from system crashes and re-initializations.
*   Resist subversion(抵抗攻擊者). The IDS must be able to monitor itself and detect if it has been modified by an attacker.
*   Impose a minimal overhead（不影響正常運作） on the system where it is running.
*   Be able to be configured according to the security policies of the system that is being monitored.
*   Be able to adapt to changes in system and user (如開省電模式)behavior over time.
*   Be able to scale to monitor a large number of hosts.
*   Provide graceful degradation of service（一功能失效其他功能還可運行） in the sense that if some components of the IDS stop working for any reason, the rest of them should be affected as little as possible.
*   Allow dynamic reconfiguration（動態設定）; that is, the ability to reconfigure the IDS with- out having to restart it.

# **8.3  Analysis Approaches**

*   **Anomaly detection** **(合法行為偵測，不符合合法行為就為intruder)**
    *   Collecting data
        *   The behavior of legitimate users over a period of time
    *   Analyzing current observed behavior with a high level of confidence
        *   A legitimate user or an intruder
*   **Signature/Heuristic detection (已知惡意病毒偵測)**
    *   Using a set of known malicious data patterns (signatures) or attack rules (heuristics)
    *   Can only identify known attacks

## Anomaly Detection

### Categories of classification approaches

*   **Statistical** **(統計)**
    *   Analysis of the observed behaviors/metrics
    *   Using univariate, multivariate, or time- series models
    *   Pros: **simplicity**, **low computation cost**, and **lack of assumptions about behavior expected**
    *   Cons: **difficulty in selecting suitable metrics**, and **not all behaviors can be modeled (metric 用 traffic量或其他方法當metric做偵測才適當)**
*   **Knowledge based**
    *   Classifying the observed data using a set of rules
    *   Rules are developed during the training phase, usually manually
    *   Formal tools: finite-state machine or standard description language
    *   Pros: **robustness** and **flexibility**
    *   Cons: **difficulty/time required to develop high- quality knowledge rules (人工)**
*   **Machine-learning**
    *   Automatically determining a suitable classification model from the training data using data mining techniques
    *   Pros: **flexibility**, **adaptability**, and **ability to capture interdependencies between factors**
    *   Cons: **requiring significant time and computational resources**



*   A variety of machine-learning approaches with varying success
    *   **Bayesian networks:**Encode probabilistic relationships among observed metrics.
    *   **Markov models:** Develop a model with sets of states, some possibly hidden,
    *   interconnected by transition probabilities.
    *   **Neural networks:** Simulate human brain operation with neurons and synapse between them, that classify observed data.
    *   **Fuzzy logic:** Uses fuzzy set theory where reasoning is approximate, and can accommodate uncertainty
    *   **Genetic algorithms:** Uses techniques inspired by evolutionary biology, including inheritance, mutation, selection and recombination, to develop classification rules.
    *   **Clustering and outlier detection:** Group the observed data into clusters based on some similarity or distance measure, and then identify subsequent data as either belonging to a cluster or as an outlier.
*   What is the key limitation?
    *   只有已知行為受到訓練，未知的沒有
    *   generally only trained with legitimate data, unlike many of the other applications surveyed in \[CHAN09\] where both legitimate and anomalous training data is used

## Signature or Heuristic Detection

*   Signature approaches
    *   Matching a large collection of known patterns of malicious data in a system or over a network
    *   Signatures
        *   Large enough to minimize the false alarm rate
        *   Sill detecting a sufficiently large fraction of malicious data
    *   Widely used in anti-virus products (防毒軟體)
*   Rule-based heuristic identification
    *   Identifying known penetrations
    *   Identifying suspicious behavior within the bounds of established patterns of usage
    *   Specific to the machine and OS

# **8.4  Host-Based Intrusion Detection**

*   A specialized layer of security software to vulnerable or sensitive systems
    *   Monitor activity on the system to detect suspicious behavior
*   Main purpose: detect intrusions, log suspicious events, and send alerts
    *   Can use either anomaly or signature and heuristics approaches
*   Primary benefit: can detect both external and internal intrusions

## Data Sources and Sensors

*   System call traces
    *   A record of the sequence of system calls by processes on a system
    *   Work well for Unix and Linux systems, but problematic on Windows(DLL)
    *   95-99% detection rates \[CREE13\]
*   Audit (log file) records
    *   Most modern OSes have accounting software that collects information on user activity
    *   Pros: no additional collection software is needed
    *   Cons: may not contain the needed information or in a convenient form
    *   80% detection rates
*   File integrity checksums
    *   Periodically scan critical files for changes
    *   Cons: generate and protect the checksums, difficult to monitor changing files
*   Registry access
    *   Used on Windows to monitor access to the registry

## Anomaly HIDS

*   Gathering the system call traces using an OS hook, e.g., BSM (Basic Security Module) audit module
*   Using traces of key DDL function calls (南區別是否為惡意行為，只有call library的log)
    *   DDLs (Dynamic Link Libraries): an intermediary between process requests and system call interface

![](https://t3764800.p.clickup-attachments.com/t3764800/dd48ae5b-af4b-4895-b13d-96fb27201319/image.png)

## Signature or Heuristic HIDS

*   Using a database of
    *   File signatures: patterns of data found in known malicious software
    *   Heuristic rules: characterizing known malicious behavior
*   Widely used in anti-virus software
*   Efficient at detecting known malware, but not capable of detecting zero-day attacks

## Distributed HIDS

*   Major issues
    *   sensor分散在不同的地方或host，並把log傳回分析
    *   Need to deal with different data sensors
    *   Assure the integrity and confidentiality of the sensor data
    *   Architecture
        *   Centralized: bottleneck and single point of failure
        *   Decentralized: coordination
*   components
    *   **Host agent module****:** An audit collection module operating as a background process on a monitored system. Its purpose is to collect data on security-related events on the host and transmit these to the central manager. Figure 8.3 shows details of the agent module architecture.
    *   **LAN monitor agent module****:** Operates in the same fashion as a host agent module except that it analyzes LAN traffic and reports the results to the central manager
    *   **Central manager module****:** Receives reports from LAN monitor and host agents and processes and correlates these reports to detect intrusion.
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/adac3898-1351-445e-af35-c1b2ac2c1068/image.png)
*   **Agent Architecture**
    1. **Agent Captures Audit Records:**
        *   The agent intercepts audit records generated by the system's native auditing system.
        *   A filter selects only records relevant to security.
    2. **Reformatting and Analysis:**
        *   The records are standardized into a HAR (host audit record) format.
        *   A template-driven logic module analyzes HARs for suspicious activity.
            *   **Level 1:** Scans for individual notable events (e.g., failed logins, file access changes).
            *   **Level 2:** Detects sequences of events matching known attack patterns (signatures).
            *   **Level 3:** Identifies user behavior anomalies based on historical profiles.
    3. **Alerting the Central Manager:**
        *   If suspicious activity is discovered, an alert is sent to the central manager.
    4. **Central Manager Analysis and Correlation:**
        *   The central manager employs an expert system to draw inferences from received data.
        *   It can query individual systems for HAR copies to correlate with data from other agents.
    5. **LAN Monitor Agent Input:**
        *   The LAN monitor agent provides additional information to the central manager:
            *   Host-host connections
            *   Services used
            *   Traffic volume
        *   It flags events like sudden network load changes, security-related service usage, and suspicious activities.
    6. **Flexible and Expandable Architecture:**
        *   The architecture supports machine-independent intrusion detection.
        *   It can expand to correlate activity across multiple sites and networks, enhancing detection capabilities.
    *   *   ![](https://t3764800.p.clickup-attachments.com/t3764800/eafdc74e-8a35-4e0d-bd72-ddc9f7309f67/image.png)

# **8.5  Network-Based Intrusion Detection**

*   Monitoring traffic at selected points on a network or interconnected set of networks
    *   Packet by packet in real time, or close to real time
    *   Network-, transport-, and/or app-level protocol activity
*   What is different between NIDS and HIDS?
    *   NIDS: examines packet traffic toward potentially vulnerable systems on a network
    *   HIDS: examines user and software activity on a host
*   Typically included in the perimeter security infrastructure of an organization, located with the firewall
*   Including
    *   A number of sensors to monitor packet traffic
    *   One or more servers for management functions
    *   One or more management consoles for the human interface
*   Their ability gradually becomes to not function well
    *   Why?
    *   NIDS基本上就看traffic，但現在很多traffic基本上都加密，能看得剩IP/TCP header (IPsec只能看IP header)

## Types of Network Sensors

*   Inline sensors (直接在traffic通道上)
    *   Inserted into a network segment
    *   Combined with a firewall or a switch
    *   Motivation/Pros: block an attack when one is detected
    *   Pros: no additional separate hardware devices are needed
    *   Cons: negative impact on network performance
*   Passive sensors
    *   Monitoring a copy of network traffic (the actual traffic doesn’t pass through)
    *   Pros: more efficient and doesn’t contribute to packet delay
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/a03518d8-fbca-4b3a-b068-2a982003fa7e/image.png)

## NIDS Sensor Deployment

*   location 1 (common)
    *   advantages
        *   Sees attacks, originating from the outside world, that penetrate the network’s perimeter defenses (external firewall).
        *   Highlights problems with the network firewall policy or performance.
        *   Sees attacks that might target the Web server or ftp server.
        *   Even if the incoming attack is not recognized, the IDS can some times recognize the outgoing traffic that results from the compromised server
*   location 2
    *   advantage
        *   Documents number of attacks originating on the Internet that target the network.
        *   Documents types of attacks originating on the Internet that target the network.
*   location 3
    *   advantage
        *   Monitors a large amount of a network’s traffic, thus increasing the possibility of spotting attacks.
        *   Detects unauthorized activity by authorized users within the organization’s security perimeter.
*   location 4
    *   advantage
        *   Detects attacks targeting critical systems and resources.
        *   Allows focusing of limited resources to the network assets considered greatest value.

![](https://t3764800.p.clickup-attachments.com/t3764800/4ff62ab3-dee2-4282-b76e-b45e57a96acc/image.png)

## Intrusion Detection Techniques

## Logging of Alerts

# **8.6  Distributed or Hybrid Intrusion Detection**

*   Distributed systems that cooperate to identify intrusions and to adapt to changing attack profiles
    *   Can recognize attacks based on more subtle clues and then adapt quickly
    *   Anomaly detectors at local nodes look for unusual activity
*   Due to two key problems confronting IDSs
    *   these tools may not recognize new threats or modifications of existing threats (沒辦法辨識新威脅)
    *   it is difficult to update schemes rapidly enough to deal with threats

### Overall Architecture of an Automatic Enterprise Security System (by Intel)

*   Three types of input guide the actions of the central system:
    *   **Summary events:** Events from various sources are collected by intermediate collection points such as firewalls, IDSs, or servers that serve a specific segment of the enterprise network. These events are summarized for delivery to the central policy system.
    *   **DDI events:** Distributed detection and inference (DDI) events are alerts that are generated when the gossip traffic enables a platform to conclude that an attack is under way.
    *   **PEP events:** Policy enforcement points(PEPs) reside on trusted, self-defending platforms and intelligent IDSs. These systems correlate distributed information, local decisions, and individual device actions to detect intrusions that may not be evident at the host level.
*   

![](https://t3764800.p.clickup-attachments.com/t3764800/f3eaa800-bd41-4098-b5b7-47360b55c380/image.png)

###   

# **8.7  Intrusion Detection Exchange Format**

# **8.8  Honeypots**

*   Decoy systems designed to
    *   Lure a potential attacker away from critical systems
    *   Collect information about the attacker’s activity
    *   Encourage the attacker to stay on the system long enough for administrators to respond
*   Systems are filled with fabricated information that a legitimate user of the system wouldn’t access
*   Resources that have no production value
    *   Incoming communication is most likely a probe, scan, or attack
    *   Initiated outbound communication suggests that the system has probably been compromised

### Honeypot Classifications

*   Low interaction honeypot
    *   Emulating particular IT services or systems well enough to provide a realistic initial interaction, but does not execute a full version
    *   Providing a less realistic target
    *   Often sufficient for use as a component of a distributed IDS to warn of imminent attack
*   High interaction honeypot
    *   A real system, with a full OS, services and applications, which are instrumented and deployed where they can be accessed by attackers
    *   A more realistic target that may occupy an attacker for an extended period
    *   However, it requires significantly more resources
    *   If compromised, could be used to initiate attacks on other systems

### Example of Honeypot Deployment

*   **Location 1: Outside the External Firewall**
    *   **Pros:**
        *   Tracks attempts to connect to unused IP addresses.
        *   Doesn't increase internal network risk.
        *   Reduces alerts from firewall and IDS, easing management.
    *   **Cons:**
        *   Limited ability to trap internal attackers.
*   **Location 2: Within the DMZ (Demilitarized Zone)**
    *   **Pros:**
        *   Can detect attacks on externally available services.
    *   **Cons:**
        *   Requires careful security measures to protect other DMZ systems.
        *   Might require opening firewall beyond permissible levels or limiting honeypot effectiveness.
*   **Location 3: Fully Internal**
    *   **Pros:**
        *   Catches internal attacks.
        *   Detects misconfigured firewalls.
    *   **Cons:**
        *   If compromised, can attack other internal systems.
        *   Requires firewall adjustments, complicating configuration and potentially compromising the internal network.

![](https://t3764800.p.clickup-attachments.com/t3764800/cbb1b79d-3cab-4f6f-bef1-ecab1134e0ac/image.png)



# **8.9  Example System: Snort**

## Snort Architecture

## Snort Rules

# **8.10  Key Terms, Review Questions, and Problems**

#
