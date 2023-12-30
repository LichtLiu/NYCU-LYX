---
title: "Computer Security Principles and Practice"
permalink: /1-Overview/
layout: default
---
# 1-Overview-zh

> **書名：C**omputer **S**ecurity Principles and Practice  
> **版本：Fourth Edition Global Edition**  
> **作者：William Stallings Lawrie Brown**



> 學習目標  
> ◆ 描述 機密性(confidentiality)、完整性(Integrity)、可用性(availability) 的關鍵安全要求。  
> ◆ 討論必須處理的安全威脅(security threats)和攻擊類型(attacks)，並舉例說明適用於不同類別的計算機(computer)和網路資產(network assets)的威脅和攻擊類型。  
> ◆ 總結計算機安全的功能需求。  
> ◆ 解釋基本的安全設計原則。  
> ◆ 討論攻擊面(attack surface)和攻擊樹(attack tree)的使用。  
> ◆ 了解全面安全策略(comprehensive security strategy)的原則方面。

**1\. 我們要保護什麼資產？**（What assets do we need to protect? ）

**2\. 這些資產如何受到威脅？（**How are those assets threatened?）

**3\.** 我們可以做什麼來應對這些威脅？（What can we do to counter those threats?）



* * *



# 1.1 Computer Security Concepts

## 電腦安全定義 (definition of computer security)

The NIST Internal/Interagency Report NISTIR 7298 (_Glossary of Key Information Security Terms_, May 2013) 定義

> **Computer Security:** Measures and controls that ensure confidentiality, integrity, and availability of information system assets including hardware, software, firm- ware, and information being processed, stored, and communicated.  
> 電腦安全：計畫及控制確保保密性、完整性、可用性包含資訊系統資產之硬體、軟體、韌體及處理中/儲存中/溝通中的資訊



![](https://t3764800.p.clickup-attachments.com/t3764800/9bc14555-062d-4786-942c-99b3bfc20ef2/Screen%20Shot%202023-12-30%20at%2011.41.35%20PM.png)



_三個電腦安全關鍵目標_：

*   保密性（Confidentiality）: 該術語涵蓋兩個相關概念

\-- 資料保密性（**Data confidentiality**）：確保私人或機密信息不會向未經授權的個人提供或披露。

\-- 隱私性（Privacy）：確保個人可控制或影響收集和儲存與其相關的哪些信息以及可以向誰披露該信息。

*   完整性：該術語涵蓋兩個相關概念：

— 資料完整性：確保信息和程序僅被更改以指定和授權的方式。

— 系統完整性：確保系統以不受損害的方式執行其預期功能，免受故意或無意的未經授權的系統操縱。

*   可用性：確保系統及時運行並且不會拒絕向授權用戶(authorized users

)提供服務。



1. 這三個概念又被稱為 **CIA triad。**
2. 這三個概念體現 資料、資訊及運算服務的基礎安全目標。
3. the NIST standard FIPS 199 (_Standards for Security Categorization of Federal Information and Information Systems_, February 2004) 列出 保密性、完整性、可用性 為資訊和資訊系統的三個安全目標。

_FIPS 199 在每個類別中定義安全損失及提供了這三個目標的有用特徵_：

*   保密性：保留對訊息訪問和披露(disclosure)的授權限制，包括保護個人隱私和專有(proprietary)信息的手段。機密性喪失是指未經授權的信息洩露。
*   完整性：防止訊息被不當修改或破壞，包括確保訊息的不可否認性(nonrepudiation)和真實性(authenticity)。完整性喪失是指未經授權的修改(modification )或破壞信息(destruction)。
*   可用性：確保及時、可靠地訪問和使用信息。可用性喪失是指信息或信息系統的訪問或使用中斷(disruption )。

其他兩個最常被提及的概念

*   真實性(**Authenticity**)：真實(genuine)且能夠被驗證和信任的屬性；對傳輸(transmission)、消息(message)或消息來源(message originator)有效性的信心。這意味著驗證用戶是否是他們所說的人，以及到達系統的每個輸入都來自可信來源。
*   問責制(**Accountability** )：安全目標是實體(entity)的操作能夠唯一地(uniquely)追踪到該實體。這支持不可否認性(nonrepudiation)、威懾(deterrence)、故障隔離(fault isolation)、入侵檢測(intrusion detection)和預防以及事後恢復和法律行動。由於真正安全的系統還不是一個可實現的目標，因此我們必須能夠追踪安全漏洞的責任方​​。系統必須保存其活動記錄，以便以後進行取證分析，以追踪安全漏洞或幫助解決交易糾紛。

_Note: 請注意，FIPS 199 包括完整性下的真實性。_

![](https://t3764800.p.clickup-attachments.com/t3764800/f81ac74a-b06a-4082-9d83-f809bfe62090/Screen%20Shot%202023-09-16%20at%203.56.36%20PM.png)



## 三個等級的資安衝擊 (Three levels of security impacts)

三個以FIPS 199 分級的範例：

*   Low: limited adverse(有害的) effect (minor)

對組織營運、資產、個人在損失有可預期有限的有害影響

*   主要功能執行能力下降
*   造成組織較小的資產損失
*   造成組織較小的財務損失
*   造成個人較小的傷害

*   Moderate: serious adverse effect (significant)

對組織營運、資產、個人在損失有可預期的嚴重有害影響

*   主要功能執行能力大幅下降
*   造成組織重大的資產損失
*   造成組織重大的財務損失
*   對個人造成重大傷害，但不涉及生命損失或嚴重危及生命的傷害

*   High: catastrophic adverse effect (catastrophic)

對組織營運、資產、個人在損失有可預期災難性的有害影響

*   主要功能執行能力失效
*   造成組織較大的的資產損失
*   造成組織較大的財務損失
*   對個人造成重大傷害，包含生命損失或嚴重危及生命的傷害



Confidentiality

在美國，學生成績受到 Family Educational Rights and Privacy Act (FERPA) 規範，成績資訊是一種學生認為其保密性非常重要的資產

*   Low: 學生列表或部門列表 低保密性等級
*   Moderate: 學生註冊資訊為 中等保密等級(covered by FERPA)
*   High: 學生成績僅可被學生、家人或受僱者工作需要所利用(covered by FERPA)



Integrity

被篡改的資料庫需要快速恢復到可信基礎，並且應該可以將錯誤追溯到責任人

*   Low: 匿名網路調查
*   Moderate: 文章討論留言
*   High: 病患過敏資訊



Availability

組件或服務越關鍵，所需的可用性級別就越高。服務的損失會轉化為員工生產力下降和潛在客戶流失的巨大財務損失

*   Low: 線上電話尋找系統
*   Moderate: 全球性公開網站
*   High: 重要系統的驗證服務



## 電腦資訊安全的挑戰 (Challenges of computer security)

*   資訊安全並不簡單
    *   需求看起來很直接
    *   要達成需求的機制很複雜
*   考慮潛在攻擊
    *   成功的攻擊通常是利用不同的角度檢視問題
    *   利用非預期的弱點
*   過程通常很直觀
    *   通常安全機制很複雜
    *   只有考慮到威脅的各個方面才有意義
*   決定在哪裡部署機制
    *   在網路的哪個點
    *   在架構(OSI)的哪一層
*   涉及算法和秘密信息（密鑰）
    *   如何建立、分配、保護秘密資訊
    *   依賴底層協議可能使開發變複雜
*   攻擊者與管理者的戰爭
    *   攻擊者：尋找漏洞，只需找出一個弱點
    *   設計師：堵住漏洞，消除所有弱點
*   用戶直到出現安全故障時才感受到好處
    *   安全需要定期且持續的監控
    *   在當今的短期超載環境中很困難
*   經常是事後的想法（不是完整的）
    *   不是設計過程的組成部分
*   高安全性造成效率和使用者友善的阻礙



## 電腦安全模型 (Computer Security model)

計算機系統的資產(assets)可分為以下幾類：

*   硬體：包括電腦系統和其他資料處理、資料儲存和資料通信設備。
*   軟體：包括作業系統、系統公用程式和應用程式。
*   資料：包括檔案和資料庫，以及與安全相關的資料，例如 密碼文件。
*   通信設施和網絡：LAN 和 WAN 通訊鏈結、橋接、路由等。



*   弱點(Vulnerability) : 系統資源弱點
    *   走樣的(Corrupted): 失去完整性
    *   洩漏的(Leaky): 失去保密性
    *   不可用或遲緩(Unavailable or very slow): 失去可用性
*   威脅(Threat): 利用弱點的能力
    *   潛在危害資產的風險
*   Attack: a threat that is carried out (threat action)
    *   被動的(Passive): 學習或利用信息，但不影響系統資源
    *   主動的(Active) : 改變系統資源或影響其運行
    *   內部(Inside): 由授權用戶（以未經批准的方式使用授權資源）
    *   外部(Outside): 由非授權用戶



*   對策(Countermeasure)
    *   用於應對安全攻擊的手段
        *   _防止攻擊_
        *   _檢測它們然後恢復_
    *   本身可能會引入新的漏洞
    *   殘留漏洞可能仍然存在
    *   目標是最大限度地降低資產的殘餘風險水平
        *   _殘餘風險：通過風險控制降低固有風險後，與剩餘行動/事件相關的風險量_

![](https://t3764800.p.clickup-attachments.com/t3764800/828579c1-773b-4b5e-ad8f-188063b9e432/Screen%20Shot%202023-09-16%20at%2010.02.38%20PM.png)





| **Adversary (threat agent)**<br> | 進行或意圖進行有害活動的個人、團體、組織或政府。 |
| ---| --- |
| **Attack** | 任何試圖收集、破壞、否認、降級或破壞信息系統資源或信息本身的惡意活動 |
| **Countermeasure** | 一種設備或技術，其目標是損害不良或對抗性活動的操作有效性，或防止間諜活動、破壞、盜竊或未經授權訪問或使用敏感信息或信息系統。 |
| **Risk**<br> | 衡量實體受到潛在情況或事件威脅的程度，通常是以下因素的函數： 1) 如果情況或事件發生，將產生不利影響； 2) 發生的可能性。 |
| Security Policy | 提供安全服務的一套標準。它定義並限制數據處理設施的活動，以維持系統和數據的安全狀態 |
| System Resource(Asset) | 主要應用程式、通用支持系統、高影響程式、物理工廠、關鍵任務系統、人員、設備或邏輯相關的系統組。 |
| Threat | 任何可能通過信息系統通過未經授權的訪問、破壞、披露、修改信息對組織運營（包括使命、職能、形像或聲譽）、組織資產、個人、其他組織或國家產生不利影響的情況或事件和/或拒絕服務。 |
| Vulnerability | 資訊系統、系統安全程序、內部控製或實施中可能被威脅源利用或觸發的弱點。 |



# 1.2 Threats, Attacks, and Assets

## 威脅和攻擊(Threat and Attack)

| **Threat Consequence** | **Threat Action (Attack)** |
| ---| --- |
| **未授權公開(Unauthorized Disclosure)**<br>\- 保密性威脅 | **(1) 暴露(Exposure)：敏感資料被直接發布給未授權實體(Entity)**;<br>**(2) 攔截(Interception)：**未經授權的實體直接訪問在授權來源和目的地之間傳輸的敏感數據。<br>**(3)推斷(Inference)**: 間接訪問敏感數據（但不一定是通信中包含的數據）<br>**(4) 侵入(Intrusion)：**未經授權的實體通過繞過系統的安全保護來訪問敏感數據。 |
| **欺騙(Deception)**<br>\- 系統/資料完整性威脅 | **(1) 變裝(Masquerade)：**未授權用戶通過冒充授權用戶或特洛伊木馬(Trojan horse)行為來獲取系統訪問權限；<br>**(2) 竄改(Falsification)：**虛假數據欺騙授權實體。<br>**(3) 拒絕(Repudiation)**: 一個實體通過錯誤地否認對某種行為負責來欺騙另一個實體 |
| **崩潰(Disruption)**<br>\- 可用性/系統完整性威脅<br> | **(1) 使無能力(Incapacitation)**: 通過禁用系統組件來阻止或中斷系統操作。<br>**(2) 墮落(Corruption)**: 不期望地改變系統操作。<br>**(3) 阻礙(Obstruction)**: 中斷提供系統服務<br> |
| **篡奪(Usurpation)**<br>\- 系統完整性威脅<br> | **(1) 濫用(Misappropriation)**: 對系統資源進行未經授權的邏輯logical或物理physical控制<br>**(2) 誤用(Misuse)**: 未經授權存取系統<br> |

> trojan horse它是一種惡意軟體，通常被隱藏成電子郵件附檔或免費下載檔案，然後傳輸到使用者的裝置。惡意程式碼經下載後，就會執行攻擊者所設計的任務，例如：取得企業系統的後門存取權、監視使用者的網路活動，或竊取敏感資料。



## 威脅和資產 (Threat and Asset)

*   Assets: hardware, software, data, and communication lines and networks.
    *   Threats: breaches of availability, confidentiality, and integrity
*   **硬體****(Hardware)：**
    *   硬體風險包括來自事故、故意攻擊和盜竊（尤其是USB驅動器）的可用性問題。
*   **軟體****(Software)：**
    *   軟體，特別是應用程式，可能會被刪除、修改或盜版。
*   **數據****(Data)：**
    *   數據安全問題涉及可用性、保密性和完整性，重點關注數據破壞和未經授權訪問。
    *   該段還討論了通過統計數據庫分析在組合數據集時出現的隱私侵犯威脅，可以揭示個體特徵。
*   網路安全攻擊 (communication lines and networks.)
    *   被動攻擊
        *   竊聽(Eavesdropping)或監控(monitoring)傳輸
        *   目標：獲取正在傳輸的信息
        *   兩種類型：消息內容的洩露和流量分析。
    *   主動攻擊
        *   涉及對數據流的某些修改或創建虛假流(stream)
        *   四種類型：重放(replay)、偽裝(masquerade)、消息修改(modification of messages)和拒絕服務（DoS）
            *   重放：重放攻擊涉及被動捕獲數據單元，然後重新傳送它以產生未經授權的影響。
            *   偽裝：偽裝發生在一個實體假裝成另一個實體的情況下。攻擊偽裝通常包括其他形式的主動攻擊之一。例如，身份驗證序列可以在有效的身份驗證序列發生後被捕獲並重放，從而使身份驗證序列變得更脆弱。權限較少的授權實體能夠通過冒充擁有這些權限的實體來獲得額外的權限。
    *   



![](https://t3764800.p.clickup-attachments.com/t3764800/74ad7c20-09fa-4210-9917-ab80501d1edd/Screen%20Shot%202023-09-17%20at%2012.18.32%20AM.png)



![](https://t3764800.p.clickup-attachments.com/t3764800/3a14c071-aff5-466e-9a2a-945897141188/Screen%20Shot%202023-09-17%20at%2012.14.07%20AM.png)





# 1.3 Security Functional Requirements



> One computer security expert, Bruce Schneier, observed  
> If you think technology can solve your security problems, then you don’t understand the problems and you don’t understand the technology.



1. 討論了對減少漏洞和診斷系統資產威脅的分類和特徵化。
2. 從功能需求的角度來考慮對策，遵循FIPS 200中定義的分類。
3. FIPS 200列舉了保護信息系統和數據機密、機密性和可用性的17個安全相關領域。
4. 這些要求包括各種對策，可分為兩類：技術措施（硬件或軟件）和管理問題。
5. 主要需要技術措施（訪問控制、識別、身份驗證、系統和通信保護以及系統和信息缺陷）的功能領域。
6. 主要涉及管理控制和程序的功能領域包括意識和培訓、審計和會計、認證、認可、稽查計劃、維護、物理和環境保護、計劃、人員安全、評估以及系統和服務採購。
7. 一些功能領域同時涉及技術措施和管理控制，包括配置管理、事件響應和媒體保護。
8. FIPS 200中的大部分功能要求領域涉及管理組成部分，強調了在實現有效的計算機安全時需要綜合技術和管理方法的重要性。
9. 段落強調了理解技術和管理方面的重要性，以有效解決安全問題。
10. FIPS 200 提供了關於計算機安全主要關注領域的有用摘要，包括技術和管理方面。
11. 前面提到的書籍旨在涵蓋所有這些領域，以提供全面的計算機安全指南。



## 安全功能需求 (Security Functional Requirements (FIPS 200) )

*   技術措施
    *   訪問控制;身份識別和認證；系統及通訊保護；系統和信息完整性
*   管理控制和程序
    *   意識和培訓；審計與問責；認證、認可和安全評估；應急計劃；維護；物理和環境保護；規劃；人員安全；風險評估；系統和服務採購
*   技術和管理重疊
    *   配置管理；事件響應；媒體保護



![](https://t3764800.p.clickup-attachments.com/t3764800/67b3dc42-727b-440e-830b-e157a1fa5dcd/Screen%20Shot%202023-09-17%20at%204.36.13%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/460ba904-fba1-4faf-8338-603d7a758ef3/Screen%20Shot%202023-09-17%20at%204.37.29%20PM.png)



# 1.4 Fundamental Security Design Principles

*   Why do we need principles?
    *   No security design and implementation techniques that can **systematically** exclude security flaws and prevent all unauthorized actions
    *   But, good practices for good design have been documented

note: The National Centers of Academic Excellence in Information Assurance/Cyber Defense, which is jointly sponsored by the _U.S. National Security Agency_ and the U. S. Department of Homeland Security, list the following as fundamental security design principles \[NCAE13\]



## 基礎安全設計原則 (Fundamental security design principles \[NCAE13\] )

*   機制經濟(Economy of mechanism)
    *   設計應該盡可能簡單和小
*   故障安全默認值(Fail-safe defaults)
    *   訪問決策應基於許可而不是排除
*   完整的調解(Complete mediation)
    *   每次訪問(access)都必需根據訪問控制機制(access control mechanism)進行檢查
*   開放式設計(Open design)
    *   設計應該公開而不是秘密（例如，廣泛採用 NIST 批准的算法）
*   特權分離(Separation of privilege)
    *   根據不同級別的信任、需求和權限要求分離用戶和進程(processes)
*   最小特權(Least privilege)
    *   系統的每個進程(process)和每個用戶都應使用執行任務所需的最少權限進行操作
*   最不常見的機制(Least common mechanism)
    *   設計應盡量減少不同用戶共享的功能，以實現共同安全(mutual security)
*   Psychological acceptability
    *   Should not interfere unduly with the work of users or hinder the usability or accessibility of resources

_\----The first eight listed principles were first proposed in \[SALT75\]----_

*   隔離(Isolation)
    *   公共訪問系統的資源
    *   個人用戶的程序(process)和檔案
    *   安全機制
*   封裝(Encapsulation)
    *   基於物件導向功能(object-oriented functionality )的特定隔離形式
*   模塊化(Modularity)
    *   將安全功能開發為單獨的受保護模組(model)
    *   使用模組化架構進行機制設計和實做(implementation)
*   分層(Layering)
    *   使用多種(multiple)重疊(overlapping)的保護方法
*   最少的驚訝(Least astonishment)
    *   程式或使用者界面應始終以最不可能讓用戶感到驚訝的方式做出響應



# 1.5 Surfaces and Attack Trees



在本節中詳細闡述了在評估(evaluating)和分類(classifying)威脅時有用的兩個概念：

*   攻擊面(Attack Surface)
*   攻擊樹(Attack Tree)。



## 攻擊面 (Attack Surfaces)

*   包含系統中可到達和可利用的漏洞\[BELL16、MANA11、HOWA03\]
    *   網路攻擊面 (Network attack surface)
        *   網路協議漏洞 (Network protocol vulnerabilities) ➝ port 開越多 attack surface越大
        *   e.g., 在對外的 Web 和其他服務器上打開端口(port) ➝ DOS
    *   軟體攻擊面 (Software attack surface)
        *   應用程式、實用(utility)程序或操作系統代碼中的漏洞
        *   e.g., 介面(Interface)、SQL 和 Web 表單(web form)
    *   人類攻擊面 (Human attack surface)
        *   人員造成的漏洞
        *   e.g., 有權訪問敏感信息的員工容易受到社交攻擊 (social engineering attack)



為什麼攻擊面分析有用？

*   評估系統威脅的規模和嚴重性
*   讓開發人員意識到哪裡需要安全機制

![](https://t3764800.p.clickup-attachments.com/t3764800/d97ab4f8-d842-4992-b87d-43641a0fbbfd/Screen%20Shot%202023-09-17%20at%205.40.58%20PM.png)



## 攻擊樹 (Attack Tree)

攻擊樹是一種分層的數據結構，用於表示利用安全漏洞的潛在技術。它以安全事件為根節點(root node)開始，分支成子節點(subnodes)，每個子節點(subnode)表示一個子目標(subgoal)，可以有進一步的子目標(subgoal)，導致不同的攻擊方式（葉節點 leaf node）。樹中的節點可以是AND節點(AND-node)或OR節點(OR-node)，具有不同的達成目標條件。攻擊樹的分支可以標有難度、成本或其他攻擊屬性，以進行比較。



攻擊樹的使用目的是有效利用有關攻擊模式的信息，例如由CERT等組織發布的信息。安全分析師可以使用攻擊樹以系統化的方式記錄安全攻擊，揭示關鍵的漏洞。攻擊樹可以指導系統和應用程序的設計，並幫助選擇和實施反制措施。



*   分支(branching)、分層(hierarchical)數據結構：一組利用安全漏洞的潛在技術
    *   Root: 攻擊目標 （最終目標）
    *   Leaf: 不同攻擊發起方式
    *   每個 node (other than a leaf) 是 AND-node 或 OR-node

![](https://t3764800.p.clickup-attachments.com/t3764800/7e07e69b-d0df-4a2c-9d1e-a0ee55ef960e/Screen%20Shot%202023-09-17%20at%205.57.54%20PM.png)



樹上的陰影框是leaf nodes，代表構成攻擊的事件。

白框是由一個或多個特定攻擊事件（leaf nodes）組成的類別。

Note在這棵樹中，除了leaf nodes之外的所有nodes都是 OR-Nodes。



• **User terminal and user (UT/U):** These attacks target the user equipment, including the tokens that may be involved, such as smartcards or other password generators, as well as the actions of the user.

• **Communications channel (CC):** This type of attack focuses on communication links.

• **Internet banking server (IBS):** These types of attacks are offline attack against the servers that host the Internet banking application.



1. 2. **使用者認證資料危害(User Credential Compromise)：**
    *   攻擊者針對使用者認證資料進行攻擊。
    *   方法包括監控使用者操作、盜取、駭客攻擊金鑰令牌、使用惡意軟體，以及竊聽通信渠道。
3. **命令注入(Injection of Commands)：**
    *   攻擊者攔截使用者終端（UT）與網際網路銀行系統（IBS）之間的通信，以冒充合法使用者並未經授權地進入系統。
4. **使用者認證猜測(User Credential Guessing)：**
    *   采用分佈式僵尸個人電腦進行蛮力攻擊，猜測使用者名稱和密碼。
5. **安全政策違規(Security Policy Violation)：**
    *   員工違反銀行的安全政策，結合弱的訪問控制和日誌記錄，可能導致內部安全事件並暴露客戶帳戶。
6. **使用已知認證會話(Use of Known Authenticated Session)：**
    *   攻擊者誘使或強迫使用者使用預設的會話識別碼連接到IBS，允許他們在使用者認證後發送偽造的數據包，冒充使用者身份。



compromise ➝ 資安裡代表攻擊成功（原意為妥協）

![](https://t3764800.p.clickup-attachments.com/t3764800/a48d70d6-5590-4e14-b5af-d670af8c13c8/Screen%20Shot%202023-09-17%20at%206.02.12%20PM.png)







# 1.6 Computer Security Strategy

Involves three aspects :

*   Specification/policy: What is the security scheme supposed to do?
*   Implementation/mechanisms: How does it do it?
*   Correctness/assurance: Does it really work?



## 安全政策(Security Policy)

*   A formal statement of rules and practices
    *   that specify (or regulate) how a system (or organization) provides security services to protect critical system resources (RFC 4949)
*   A security manager needs to consider:
    *   The value of the assets being protected (e.g., critical files)
    *   The vulnerabilities of the system (e.g., the system is open to guests)
    *   Potential threats and the likelihood of attacks (e.g., data leakage)
    *   Trade-off: ease of use vs. security (e.g., remember and type two passwords?)
    *   Trade-off: cost of security vs. cost of failure and recovery

## 安全實作與保證 (Security Implementation and Assurance)

*   Security implementation
    *   預防(Prevention), 偵測(detection) , 反應(response), 回復(recovery)
*   Assurance: provides grounds for having confidence that the system operates such that the system’s security policy is enforced
    *   expressed as a degree of confidence
    *   based on formal models
*   Evaluation: examines a computer product or system w.r.t. certain criteria

e.g., processes (ISO/IEC 21827), products (ISO/IEC 15408),security management (ISO/IEC 27001)





# 1.7 Standards

*   **National Institute of Standards and Technology:** NIST is a U.S. federal agency that deals with measurement science, standards, and technology related to U.S. government use and to the promotion of U.S. private sector innovation. Despite its national scope, NIST Federal Information Processing Standards (FIPS) and Special Publications (SP) have a worldwide impact.
*   **Internet Society:** ISOC is a professional membership society with worldwide organizational and individual membership. It provides leadership in addressing issues that confront the future of the Internet, and is the organization home for the groups responsible for Internet infrastructure standards, including the Internet Engineering Task Force (IETF) and the Internet Architecture Board (IAB). These organizations develop Internet standards and related specifications, all of which are published as Requests for Comments (RFCs).
*   **ITU-T:**TheInternationalTelecommunicationUnion(ITU)isaUnitedNations agency in which governments and the private sector coordinate global telecom networks and services. The ITU Telecommunication Standardization Sector (ITU-T) is one of the three sectors of the ITU. ITU-T’s mission is the production of standards covering all fields of telecommunications. ITU-T standards are referred to as Recommendations.
*   **ISO:** The International Organization for Standardization (ISO) is a worldwide federation of national standards bodies from more than 140 countries. ISO is a nongovernmental organization that promotes the development of standardization and related activities with a view to facilitating the international exchange of goods and services, and to developing cooperation in the spheres of intellectual, scientific, technological, and economic activity. ISO’s work results in international agreements that are published as International Standards.

A more detailed discussion of these organizations is contained in Appendix C. A list of ISO and NIST documents referenced in this book is provided at the end of the book.



# 1.8 Key Terms, Review Questions, and Problems

![](https://t3764800.p.clickup-attachments.com/t3764800/fb5642a5-22dc-4509-8d3c-a4df3406e76c/Screen%20Shot%202023-09-17%20at%206.21.18%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/5a9cf5fa-2d06-4d82-ab3a-559082f28f3c/Screen%20Shot%202023-09-17%20at%206.21.25%20PM.png)





## **Review Questions**

1. **1.1**  What is meant by the CIA triad?.
2. **1.2**  What is the difference between data integrity and system integrity?
3. **1.3**  List and briefly define the kinds of threat consequences and the types of threat actions
4. which cause these consequences.
5. **1.4**  List and briefly define the fundamental security design principles.
6. **1.5**  What is a security policy? What are the actions involved when implementing a security policy?
7. **1.6**  Differentiate between a network attack surface and a software attack surface.



## **Problems**

**1.1**  Consider a student information system (SIS) in which students provide a university student number (USN) and a card for account access. Give examples of confidentiality, integrity, and availability requirements associated with the system and, in each case, indicate the degree of the importance of the requirement.

**1.2**  Repeat Problem 1.1 for a network routing system that routes data packets through a network based on the IP address provided by the sender.

**1.3**  Consider a desktop publishing system used to produce documents for various organizations.

**Give an example of a type of publication for which confidentiality of the stored data is the most important requirement.**

**Give an example of a type of publication in which data integrity is the most important requirement.**

**Give an example in which system availability is the most important requirement.**

**1.4**  For each of the following assets, assign a low, moderate, or high impact level for the

loss of confidentiality, availability, and integrity, respectively. Justify your answers.

**a.** An organization managing public information on its Web server.

**b.** A law enforcement organization managing extremely sensitive investigative

information.

**c.** A financial organization managing routine administrative information (not privacy-

related information).

**d.** An information system used for large acquisitions in a contracting organization

contains both sensitive, pre-solicitation phase contract information and routine administrative information. Assess the impact for the two data sets separately and the information system as a whole.

**e.** A power plant contains a SCADA (supervisory control and data acquisition) sys- tem controlling the distribution of electric power for a large military installation. The SCADA system contains both real-time sensor data and routine administra- tive information. Assess the impact for the two data sets separately and the infor- mation system as a whole.

1.8 / KEY TERMS, REviEw QUESTiONS, AND PROBLEMS **51**

**1.5**  Consider the following general code for allowing access to a resource:

```plain
DWORD dwRet = IsAccessAllowed(...);
 if (dwRet == ERROR_ACCESS_DENIED) {
 // Security check failed.
    // Inform user that access is denied.
    } else {
    // Security check OK.
}
```

**Explain the security flaw in this program.**

**Rewrite the code to avoid the flaw.**

_Hint_: Consider the design principle of fail-safe defaults.

**1.6**  Develop an attack tree for gaining access to the contents of a physical safe.

**1.7**  Consider a company whose operations are housed in two buildings on the same property: one building is headquarters, the other building contains network and com- puter services. The property is physically protected by a fence around the perimeter. The only entrance to the property is through a guarded front gate. The local networks are split between the Headquarters’ LAN and the Network Services’ LAN. Internet users connect to the Web server through a firewall. Dial-up users get access to a par- ticular server on the Network Services’ LAN. Develop an attack tree in which the root node represents disclosure of proprietary secrets. Include physical, social engineering, and technical attacks. The tree may contain both AND and OR nodes. Develop a tree that has at least 15 leaf nodes.

**1.8**  Read all of the classic papers cited in the Recommended Reading document at http://[williamstallings.com/ComputerSecurity/](http://williamstallings.com/ComputerSecurity/) Compose a 500–1000 word paper (or 8–12 slide presentation) that summarizes the key concepts that emerge from these papers, emphasizing concepts that are common to most or all of the papers.
