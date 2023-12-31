---
title: "Wireless-Multimedia-Network"
permalink: /Wireless-Multimedia-Network/3-IntServ/
layout: default
---
# Lecture 3 - Integrated Service (IntServ)

![](https://t3764800.p.clickup-attachments.com/t3764800/8c743802-6c6b-49c9-9773-6f6b4ee27a94/Screenshot_20231023_224011_Adobe%20Acrobat.jpg)

![](https://t3764800.p.clickup-attachments.com/t3764800/ad5a8391-ec89-402e-a1ff-91b0f20bde08/Screenshot_20231023_224037_Chrome.jpg)

# Motivation of IntServ (動機)

*   IP 網絡不支援QoS，IP網絡包括：
    *   僅限盡力而為服務（Best effort service）
    *   對所有 FIFO 隊列規律的公平訪問
    *   Windows-based 擁塞控制（Congestion control）
*   **IntServ 的目標是保留 IP 網絡的數據報模型 (**Preserve the datagram model of IP-based networks**)，並支援實時應用程式的****資源預留****。**(reservation for real time application)。
*   **IntServ 的基本方法是****per flow****資源預留 ➝ 實現複雜度高，overhead高**
    *   如果網絡有足夠的資源，則將預留資源並將確認發送給flow。
    *   如果網絡沒有足夠的資源，則將拒絕請求並將通知發送給flow。



# Assumptions of IntServ

![](https://t3764800.p.clickup-attachments.com/t3764800/96de857d-7ed1-4cdf-918d-fee9748e0661/Screenshot_20231023_230731_Adobe%20Acrobat.jpg)

*   **資源預留的一個隱含假設是對頻寬的需求仍然超過供應(exceed supply)。**
    *   在資源預留中，需要假設對頻寬的需求仍然超過供應。這是因為，如果對頻寬的需求小於供應，則不需要資源預留。
    *   **IntServ 架構假設網絡提供的服務質量（QOS）的主要指標是逐包延遲（per-packet delay）（實際上是最悪情況下的延遲界限）。**
    *   以下是一些資源預留的典型應用場景：
        *   Voice over IP (VoIP)
        *   Video streaming
        *   Online gaming
        *   Real-time financial trading
        *   Remote control of industrial equipment

# Key Components of IntServ (關鍵IntServ元件)

![](https://t3764800.p.clickup-attachments.com/t3764800/b94f6122-08e1-4cdd-ab6e-7e88c703851b/Screenshot_20231024_235242_Adobe%20Acrobat.jpg)

*   **IntServ參考模型邏輯上定義了兩個階段(phases)：**
    *   控制階段（control phase）：建立資源預留。
    *   數據階段（Data phase）：根據預留狀態（reservation state）轉發（forward）數據包
*   **IntServ提供3種流量類別**：
    *   **保證服務（Guaranted service）**：IntServ通過資源預留為保證服務流量提供最低帶寬、最大延遲和丟包率等QoS保證。
    *   **受控負載服務（Controlled load service）**：IntServ通過限制服務流量的速率來確保網絡不至於過載，從而為所有流量提供可接受的QoS。 ➝ 最常做
    *   **盡力而為服務（Best-effort）**：IntServ不為**Best-effort**服務流量提供任何QoS保證，但會盡力將其傳輸到目的地。

# How to Setup Resource Reservation in IntServ

![](https://t3764800.p.clickup-attachments.com/t3764800/c26ec87f-f6cd-4e4e-9698-ba15d828493d/Screenshot_20231025_000206_Adobe%20Acrobat.jpg)

*   **Step 1：流規範 (Flow specialization)**
    *   應用程序描述其流量流並指定QoS需求。（etc.平均封包延遲時間）、預留頻寬）
*   Step 2 : **路由選擇**
    *   QoS預留設置(Reservation Setup)請求被發送到網絡（路由器）。
    *   路由器（router）與路由模塊（routing module）交互以確定應將預留請求轉發到的下一個跳轉（Next Hop）。
    *   路由器還會與Admission control協調以確定是否有足夠的資源來滿足請求的資源。
    *   如果預留設置（reservation setup）成功，則將預訂流的信息安裝到資源預留表（resource reservation table）中。
    *   資源預留表（resource reservation table）中的信息用於配置數據平面(data plane)中的流識別模塊（flow identification module）和數據包調度模塊（packet scheduling module）。



## Flow Specification（**流規範）**

## ![](https://t3764800.p.clickup-attachments.com/t3764800/9ad25f8f-38a1-428b-9d63-5f518b5c6076/Screenshot_20231025_001209_Adobe%20Acrobat.jpg)

*   IntServ service contract 的常見參數包括：
    *   峰值速率（Peak rate）
        *   Source可以產生的最高速率。
    *   平均速率（Average rate）
        *   一段時間內的平均傳輸速率。
    *   突發大小（Burst size）
        *   在峰值速率（Peak rate）下可以注入（injected）網絡的最大數據量。
*   在IntServ中，通過令牌桶機制（token bucket）來實現允許的流量速率。
*   token buckt是一種流量控制機制，它使用一個buckt來存儲token。每當發送一個數據包時，都需要從bucket中消耗一個token。如果bucket中沒有token，則數據包將被丟棄。
*   token bucket的參數包括：
    *   Bucket capacity
        *   bucket中可以存儲的最大token數量。
    *   token 生成速率（Token generation rate）
        *   bucket中token生成的速率。
*   token bucket可以確保流量速率不超過bucket capacity。
*   IntServ服務合同的示例：
    *   峰值速率：100 kbps
        *   平均速率：50 kbps
*   突發大小：100 KB
*   這意味著源可以以最高100 kbps的速度發送數據包，但平均速率不得超過50 kbps。此外，源可以在不丟包的情況下注入100 KB的數據。
*   IntServ服務合同可以確保源產生的流量符合網絡的要求，從而為所有流量提供良好的QoS。



![](https://t3764800.p.clickup-attachments.com/t3764800/8f2295bf-a6bf-4a9b-9b13-4a676545bbd5/Screenshot_20231027_180338_Adobe%20Acrobat.jpg)

*   token bucket 是一種具有兩個參數：
    *   Token 到達速率 r（Token arrival rate）
    *   Bucket 深度 b（Bucket depth）：token bucket可以容納的最大token數。
    *   Token以恆定速率(constant rate) r 掉入桶中。
    *   Token被到達的packet消耗。只有在Bucket中有足夠Token，packet才能被發送。如果bucket中沒有token，packet將被丟棄。
    *   當一個packet到達時，Regulator只會在Bucket中有足夠Token的情況下發送該packet。
    *   當一個packet離開token bucket時，Regulator會刪除等於該packet大小的Token數。
    *   bucket depth b 是token bucket可以容納的最大token數的限制。

> **範例：**  
> Token Bucket的Token到達速率為 100 token/秒，bucket depth為 10 tokens。這意味著每秒有 100 個tokens進入bucket中，bucket中最多可以存儲 10個tokens。  
> 當一個packet到達時，Regulator會檢查bucket中是否有足夠的token。如果有，Regulator會發送packet並從bucket中刪除等於該packet大小的token數。如果沒有，Regulator會丟棄packet。  
> Token bucket可以確保流量速率不超過bucket depth。這可以防止網絡過載並確保所有流量都能得到良好的服務質量（QoS）。



## Challenges of Route Selection （路由選擇的挑戰）

![](https://t3764800.p.clickup-attachments.com/t3764800/2451b025-ba5c-4771-b0d3-98bb3ec3c88d/Screenshot_20231027_182258_Adobe%20Acrobat.jpg)

*   目前，Protocols通常使用簡單的指標(metric)，例如delay、hop count或 administrative weight來計算到所有目的網絡的最短路徑（shortest path）-➝ 然而，這種方法缺乏對可用資源 (available resources)的必要信息，無法做出明智 (intelligent)的決定。
*   這個問題進一步變得複雜，因為Application可能有多個要求(requirements)，這是一個 NP 完全問題。
*   未商業化：已經提出了許多有趣的解決方案來解決這個問題，但沒有任何一個解決方案在商業產品中得到實現。
*   因此，IntServ 將路由(routing)與預留(reservation process)分開，並假設路由器中的路由模塊(routing module)將提供next hop。



> 路由選擇是一個複雜的問題，需要考慮多種因素，例如網絡拓撲、鏈路狀態、流量模式和 QoS 要求。簡單的路由算法，例如最短路徑算法，通常不能滿足這些要求。  
> IntServ 將路由與預留分開，可以解決以下問題：  
> **提高路由的靈活性**：IntServ 不需要路由模塊了解網絡中可用資源的狀態。這使得路由模塊可以更靈活地選擇路徑，例如根據網絡負載或 QoS 要求進行選擇。  
> **簡化路由模塊的設計**：IntServ 路由模塊不需要考慮資源預留的問題，這可以簡化其設計。  
> **提高資源預留的效率**：IntServ 可以通過集中資源預留來提高效率。  
> IntServ 的缺點是可能會導致路由與資源預留之間的矛盾。例如，路由模塊可能會選擇一條最短路徑，但該路徑上的資源不足以滿足預留要求。這種矛盾可能會導致丟包或服務質量下降。



### More About Reservation Setup (更多預留設定)

![](https://t3764800.p.clickup-attachments.com/t3764800/7ad39db7-4c64-4c37-ac8e-757002fbf61d/Screenshot_20231027_184003_Adobe%20Acrobat.jpg)

*   我們需要一個protocol來傳輸流量特徵和(traffic characterization) 資源需求(resource requirement)的信息，以便路徑上的每個路由器都可以決定接受或拒絕請求。
*   我們還需要一個預留設置協議(reservation setup protocols)，hop by hop 地沿著path在路由器中安裝預留狀態(install reservation state)。
*   預留設置協議必須能夠處理網絡拓撲(network topology)的變化。
*   在 IntServ 中，RSVP（Reservation Protocol）是被採用的Reservation Setup Protocol。
*   RSVP 的特點包括：
    *   接收者(receiver-initiated)發起的，並且被設計為與 IP 多播(multicast)一起工作
        *   sender 可以告訴規格
        *   receiver 告訴網路裡面的路由器有沒有符合sender規格的路徑，來接收流量
    *   允許不同的預留方式(reservation style) ➝ FF、WF、SE
    *   採用軟狀態(soft-state)方法來處理資源變化(resource change) ➝ 週期性向Router更新，就不會把Table裡的紀錄刪掉，沒有收到更新的話就刪掉



### Admission Control (進入許可控制)

![](https://t3764800.p.clickup-attachments.com/t3764800/c0cc098a-62c2-41f5-b97a-f7378027e082/Screen%20Shot%202023-10-27%20at%2011.13.39%20PM.png)

*   **Admission control 的兩個功能**
    *   根據 admission control policy確定是否可以建立new reservation。
    *   監控(Monitor)和測量可用資源(measure available resources)。
*   **Admission control 的兩種基本方法**
    *   **基於參數****(Parameter based) ➝** 可靠性和性能要求較高
        *   使用一組參數來精確描述流量。例如：
            *   流量模式（例如，突發流量、實時流量、批處理流量）
            *   流量速率
            *   流量持續時間
            *   流量的優先級
        *   但是，很難提供準確、嚴格的流量模型(trafiic model)。
    *   **基於測量****(Measurement Based)**：網路測量實際流量負載並將其用於 admission control。 ➝ 動態性要求較高
        *   基於測量的 admission control 需要額外的計算和通信開銷。此外，基於測量的 admission control 可能會導致網絡出現短暫的擁塞，因為它需要時間來測量網絡的實際流量負載

![](https://t3764800.p.clickup-attachments.com/t3764800/8b97794f-fcec-4810-afac-d4ff9992cdaa/Screen%20Shot%202023-10-27%20at%2011.34.31%20PM.png)

*   **最常用的 admission control 方法**
    *   **簡單求和 (Simple sum)**：所有當前flows和new flows的requested bandwidth之和小於link capacity。這是最保守(conservative)的方法。 ➝ parameter based
    ➝ _SUM(flows's requested bandwidth) < link capacity_
    > 簡單求和方法非常保守，因為它假設所有流都將以其請求的bandwidth進行傳輸。這在實際情況中是不太可能的，因為流量通常會波動。因此，簡單求和方法可能會拒絕一些有效的預留，或者接受一些可能導致網絡擁塞的預留。
    *   **測量求和 (Measured sum)**：測量求和方法使用existing flows的測量負載(load)(measured load)而不是它們requested bandwidth。
    ➝ SUM(existing load)
    > 測量求和方法需要額外的計算和通信開銷。此外，測量求和方法可能需要一些時間來收集現有流的測量負載。在收集測量負載之前，測量求和方法可能無法做出 admission control 決策。
    *   **接受域 (Acceptance region)**：maximize 利用率(utilization)增加和丟包之間的獎勵(reward)。根據流量源的統計模型，可以計算出特定流量類型的接受域。
    > 接受域方法需要收集流量的統計模型，例如流量平均速率、流量峰值速率和流量持續時間。這些統計模型可以使用歷史流量數據或在線流量測量來獲得。
    >
    > 一旦收集了流量的統計模型，接受域方法就可以計算出特定流量類型的接受域。接受域是可以接受新流的資源區域。如果新流的資源需求在接受域內，則接受該新 flow；如果新 flow的資源需求在接受域外，則拒絕該新flow。
    >
    > 接受域方法是一種非常有效的 admission control 方法，但它需要收集和維護流量的統計模型，這可能會增加計算和通信開銷。

| 特徵 | RT-SYN | RT-ASYN | NRT |
| ---| ---| ---| --- |
| 同步性 | 同步 | 異步 | 非同步 |
| 實時性 | 實時 | 實時 | 非實時 |
| 數據包到達時間 | 指定的時間窗口內 | 指定的時間窗口內，允許一定的延遲 | 任意時間 |
| 丟包或延遲的影響 | 嚴重 | 可接受 | 允許 |

![](https://t3764800.p.clickup-attachments.com/t3764800/01077a13-8f5b-4a03-a457-53aac76b1168/Screen%20Shot%202023-10-28%20at%2012.20.24%20PM.png)

*       *   等效帶寬(Equivalent bandwidth)：一組flow的equivalent bandwidth定義為帶寬 C(p)，使得該組流的穩態(stationary)bandwidth requirement 以最多 p 的概率超過此值。
*   **如何測量現有流的流量負載(traffic load of existing flows)？**
    *   對連續測量的指數平均 (exponential averaging over consecutive measurement)
        *   `C = New estimation = (1 - w) * old estimation + w * new measurement`
    *   此方法計算在時間窗口(Time window)內sampling interval的平均到達率(average arrival rate)。在測量週期結束時，使用最高的平均值(average arrival rate)作為估計速率(estimated rate)。假設在測量週期 T 中有 n 個採樣區間，並且 Ci 是在採樣區間 i 測量的平均速率；則 estimated rate 計算如下
        *   `Estimated rate = max[c1, c2, ...,cn]` ➝ highest average arrival rate



### Flow Identification (Flow 識別)

![](https://t3764800.p.clickup-attachments.com/t3764800/aee93c4f-b414-40f6-9cc2-9d64bf6df3f6/Screen%20Shot%202023-10-28%20at%2012.38.31%20PM.png)

*   在packet processing，路由器必須檢查每個incoming數據包，並確定該數據包是否屬於收到的 RSVP flow之一 (belongs to one of the received RSVP flow)
*   此任務由路由器內部的packet分類器(packet classifier)執行。
*   每個packet由packet header中的五個字段(fields)（five tuple）識別：
    *   Source IP address
    *   Destination IP address
    *   Protocol ID (etc. TCP, UDP, ICMP, ARP, IPv4, IPv6)
    *   Source port
    *   Destination port

### Packet Scheduling

![](https://t3764800.p.clickup-attachments.com/t3764800/832a1d52-50e9-4621-9911-8b9a82af60a8/Screen%20Shot%202023-10-28%20at%201.00.14%20PM.png)

*   封包排程負責執行資源分配。
*   常見的排程方法：
    *   公平排程 (Fair queueing)：WFQ
    > 公平排程是一種旨在確保所有流都能獲得公平份額 bandwidth 的排程方法。公平排程通過為每個流維護一個隊列來實現這一點。隊列中的數據包按照先到先得的順序進行排程。
    *   截止期限為基礎的排程 (Deadline-based)：EDF
    > 截止期限為基礎的排程是一種旨在確保所有packet都能在指定時間內被傳輸的排程方法。截止期限為基礎的排程通過為每個數據包分配一個截止期限來實現這一點。數據包按照其截止期限進行排程，截止期限早的數據包具有更高的優先級。
    *   基於速率的排程 (Rate-based)：虛擬時鐘 (virtual clock(timestamp))
    > 基於速率的排程是一種旨在確保每個流都能以其指定速率傳輸的排程方法。基於速率的排程通過為每個流分配一個速率來實現這一點。數據包按照其分配的速率進行排程。
    >
    > 虛擬時鐘是一種基於速率的排程方法，它使用虛擬時鐘來 track每個flow的傳輸速率。虛擬時鐘是每隔一定時間增量遞增的計數器。每個流的虛擬時鐘速率由其分配的速率決定。
    >
    > 速率高 ➝ High Priority

# Service Models Defined in IntServ

![](https://t3764800.p.clickup-attachments.com/t3764800/206c27f3-48d9-41a5-b693-9afc0784433f/Screen%20Shot%202023-10-28%20at%201.25.02%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/3500e76d-9a2f-4e7b-b7e6-a72ad5599c43/Screen%20Shot%202023-10-28%20at%201.36.36%20PM.png)

*   **Guarantee service**
    *   為符合條件的流提供保證的bandwidth 和嚴格的 end-to-end 排隊延遲(queueing delay)（最大）
    *   **_支持 Guarantee service_** **_end-to-end 行為的 path_****_可以視為具有保證 bandwidth 的_** **_virtual circuit_**（比真實電路更靈活）
    *   TSpec（流量規範 traffic specification）
        *   Bucket rate r（bytes/秒）：token 到達 token bucket 的速率，用於控制流的速率的機制。
        *   Peak rate p（bytes/秒）：packets可以傳輸的最大速率
        *   Bucket depth b（bytes）：token bucket的大小
        *   Min policed unit m（bytes）：任何小於 m bytes的 packet 都將被計為 m bytes
        *   Max packet size M（bytes）：可以接受的最大 packet 大小
    *   **RSpec (服務規範)**
        *   服務速率 R（bytes/秒）：bandwidth requirement
        *   鬆弛項 (Slack term) S（microseconds）：節點可以增加的額外延遲，但仍然滿足 end-to-end 延遲要求
    *   **延遲計算 (Delay Calculation)**
        *   最佳情況端到端排隊延遲：b/R（p → ∞，R ≥ r）
            *   b 是 token bucket的大小
            *   R 是 服務速率 = bandwidth
        *   最壞情況端到端排隊延遲：b/R + (p - r)/R（p > R ≥ r）
            *   b 是 token bucket的大小
            *   R 是線路的帶寬
            *   p 是 Peak rate
            *   r 是 token bucket生成速率

> Reference: [https://datatracker.ietf.org/doc/rfc2212/](https://datatracker.ietf.org/doc/rfc2212/)

*       *       *   檢查 b、p、R 和 r 的定義
            *   b（token bucket 的大小）：token bucket 的大小決定了流的突發流量能力。
            *   p（峰值速率）：峰值速率是指流在短時間內可以達到的最大速率。
            *   R（服務速率）：服務速率是指網絡保證為流提供的帶寬。
            *   r（預留速率）：預留速率是指流在任何時候都可以使用的最小帶寬。

![](https://t3764800.p.clickup-attachments.com/t3764800/2a2bc812-7a0b-4586-b9a4-b6e2e3cf910e/Screen%20Shot%202023-10-28%20at%201.45.56%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/7bcc0887-38f4-4e44-b0d2-7e8d8f8cd257/Screen%20Shot%202023-10-28%20at%201.46.08%20PM.png)

*   **受控負載服務 (Control-load serv)**
    *   **iceic**輕度負載 (lightly loaded) 的網絡，適用於請求此服務的應用程序。
    *   通過允許統計多路復用(statistical multiplexing)，比保證服務 (guarantee service)更有效。
    *   非常適合需要一定程度的性能保證但不要求絕對上限(bounds)的自適應應用程序 (adaptive application)。
    *   通過適當的 admission control 和流量隔離機制(traffic isolation mechanism)
    *   ➝ better-than-best-effort service，介於best effort 和保guaranteed service的服務模型。
    *   端到端行為 (End-to-end behavior)
        *   傳輸的 packet 成功傳輸到目的地的概率非常高。
        *   對於絕大多數 packet 測量的 end-toen-d 傳輸延遲不會遠遠超過最小端到端傳輸延遲。
    *   接受controlled load service 的請求意味著網絡有足夠的資源來容納流量而不會引起擁塞。
    *   允許 TSpec 指定這種所需的流量參數(traffic parameter)。
    *   只有當path上的所有node都有足夠的資源來容納新flow時，才能接受新請求。
    *   admission control被留作 local matter。 ➝ 這意味著_每個node都負責決定是否接受新的受控負載流量_。
    *   流量管制 (Traffic Policing)
        *   當非符合規定的數據包到達時，網絡必須繼續向符合規定的流提供約定的服務保證。
        *   網絡應該防止過多的受控負載流量對盡力Best-effort產生不公平的影響。
        *   網絡必須在不違反前兩個要求的情況下嘗試傳輸過多的流量。

# RSVP

![](https://t3764800.p.clickup-attachments.com/t3764800/bcde1390-e7f0-4cd8-a9de-412e8894cd74/Screen%20Shot%202023-10-28%20at%202.02.19%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/b84c7ad7-73fb-4d5a-ad7b-ade7793618a1/Screen%20Shot%202023-10-28%20at%202.03.34%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/7474423e-9afd-415d-804d-922c2b31c474/Screen%20Shot%202023-10-28%20at%202.03.49%20PM.png)

*   ReSerVation Protocol **預約協議 (RFC 2205)**
*   RSVP 用於：
    *   主機(hosts)向網絡傳達服務需求(service requirement)
    *   網路中的路由器在路徑上建立預訂狀態(reservation state)
*   RSVP 不是：
    *   路由協議(is not routing protocol )
    *   提供網絡服務 (is not network services)
    *   唯一 IP 預訂協議 (is not the only IP reservation protocol )
*   RSVP 的兩個關鍵概念是 Flow 和 Reservation：
    *   Flow
        *   從發送方(sender)到一個或多個接收方(receiver)的流量流 (traffic streams)
        *   Flow spec 描述了源發送的流量流的特徵以及流所需的 QoS
        *   適用於單播(unicast)和多播(multicast) flow
    *   Reservation
        *   單向預訂 (Simplex reservation)：RSVP 只在一個方向進行預訂
        *   接收方發起的 (Receiver-initiated)：為了適應多播組(multicast group)中異質(heterogeneous)和動態的接收方(Dynamic Receiver)
        *   與路由無關 (Routing independent)：RSVP 處理過程諮詢forwarding table（由routing protocol 構建）並相應地發送 RSVP 消息
        *   與策略無關 (Policy independent)：RSVP 提供了一種在多播樹(multicast tree)或單播路徑(unicast path)上創建和維護 reservation state 的通用機制；RSVP 消息中攜帶的 control parameter 對 RSVP 而言是不透明的(opaque)
        *   軟狀態(soft state)：通過為每個reservation state設置timer來支持動態成員身份和網絡拓撲變化
        *   預訂樣式(Reservation style)：指定如何應在直接路由器上匯聚(aggregated)同一多播組(multicast group)的reservation

![](https://t3764800.p.clickup-attachments.com/t3764800/b04d9f9f-80b0-43c0-b483-c5f3273b7fd3/Screen%20Shot%202023-10-28%20at%202.04.34%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/4007aeb0-997f-4877-a1c3-9c51b486ec0b/Screen%20Shot%202023-10-28%20at%202.04.51%20PM.png)

*   RSVP 的兩個主要消息 Path message 和 Reservation message
    *   **Pa****Path message**發送方生成
    *   沿著路由方向傳輸，由單播或多播路由協議確定
    *   目的
        *   將源信息分配給接收方
        *   傳遞路徑特性
        *   為接收方提供到達發送方的信息
    *   Pathspec
        *   流 ID（發送方模板）：發送方 IP 地址，以及可選的 UDP/TCP 發送方端口
        *   Flowspec（即發送方 TSpec，不會被中間節點修改）
        *   Adspec：PATH 消息中的一個可選元素，用於承載 OPWA（一次性傳輸帶廣告）。Adspec 被傳遞給每個節點上的本地流量控制，該控制返回一個更新的 Adspec，然後在發送到下游的 PATH 消息中進行轉發
        *   PHop（上一個跳轉）
*   **Re****servation message**
    *   由接收方生成
    *   沿著 Path message 的反向傳輸
    *   RESV spec
        *   流規範：指定在數據包調度中要使用的所需的 QoS 和參數
        *   預訂樣式
        *   NHop（下一個跳轉）
    *   盡可能合併預訂請求

> Path message 和 Reservation message 是 RSVP 中最重要的兩個消息。Path message 用於將發送方信息傳遞給接收方，並建立路徑狀態。Reservation message 用於由接收方向發送方指定所需的 QoS 和參數。

*   如果路徑狀態和預訂狀態存在，則發送方和接收方將定期發送 Path message 和 Reservation message 來刷新現有的狀態。

![](https://t3764800.p.clickup-attachments.com/t3764800/3ee00bee-939e-4d60-9c11-eeae676ddc4b/Screen%20Shot%202023-10-28%20at%202.05.09%20PM.png)

*   **RSVP 操作**
    *   如果Path State 和Reservation State存在
        *   則發送方和接收方將定期發送 Path message 和 Reservation message 來刷新現有的狀態。
    *   否則
        *   發送方將先發送 Path message 在路由器中建立路徑狀態，然後接收方將在反向發送 Resv 請求。
    *   Admission control and policy control
    *   RSVP 是一種一次性預訂模型 (one pass reservation model)
    *   一 ➝ 不夠就不夠種改進是帶廣告的一次性傳輸 (OPWA)
        *   **一次性預訂模型**意味著發送方和接收方只交換一次消息來建立預訂狀態。這使得 RSVP 非常高效。
        > 帶廣告的一次性傳輸 (OPWA)是一種增強，它允許發送方在 Path message 中包含有關其流量流的廣告。這使接收方可以更好地規劃其資源，並提高整體網絡性能。



![](https://t3764800.p.clickup-attachments.com/t3764800/b1b8877c-d344-4d98-84a6-eecd7ca2011f/Screen%20Shot%202023-10-28%20at%202.05.22%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/2e85aaa4-3cdf-4efa-ad17-0dac85e6ab77/Screen%20Shot%202023-10-28%20at%202.05.37%20PM.png)

*   Packet Filtering
    *   與resource reservation分開的功能
    *   選擇可以使用reserved resources的packet的功能
*   Reservation Style：指定如何合併多個請求以及哪些資源請求將被轉發到上游節點
    *   **固定過濾器 (FF)**
        *   Explicit sender selection+ 區分預訂(distinction reservation)
        *   例如，FF(S1{Q1}, S2{Q2},.., Sn{Qn})，其中 Q1、Q2、..、Qn 是相應的流規範，S1、S2、..、Sn 是發送方
    *   **Wildcard過濾器 (WF)**
        *   Wildcard sender selection + 共享預訂(shared reservation)
        *   所有接收方共享一個預訂，其大小是資源請求中最大的
        *   所有上游發送方都可以使用預訂
        *   例如，WF(\*_, {Q})，其中 Q 是流規範，_ \* 表示Wildcard sender selection
    *   **共享顯式 (SE)**
        *   Explicit sender selection + 共享預訂(shared reservation)
        *   例如，SE((S1, S2, S4{Q})，其中 Q 是流規範，S1、S2、S3、S4 是發送方
    *   **共享預訂（WF 和 SE）是為多播應用程序設計的**
        *   在音頻會議中，通常只有兩個人可以同時說話。在這種情況下，為一個發送方請求兩倍帶寬的 WF 或 SE 預訂請求應該足夠了。
*   

![](https://t3764800.p.clickup-attachments.com/t3764800/652a1033-4e18-44d3-9d22-8f73e4d8a43f/Screen%20Shot%202023-10-28%20at%202.05.47%20PM.png)

**Explicit vs. wildcard server selection**

*   Explicit：預訂只對 RESV 消息中明確列出的發送方有效。
*   Wildcard：對任何發送方有效。

**Distinct vs. shared reservation**

*   Distinct：每個發送方都有自己的 RSVP flow。
*   Shared：使用相同的 RSVP flow來為多個發送方提供服務。

以下是一個表格，總結了 Explicit vs. wildcard server selection 和 Distinct vs. shared reservation：

| Server selection | Reservation | Fixed filter (FF) | Wildcard filter (WF) | Shared explicit (SE) |
| ---| ---| ---| ---| --- |
| Explicit | Distinct | √ | × | √ |
| Explicit | Shared | × | × | √ |
| Wildcard | Distinct | × | √ | × |
| Wildcard | Shared | × | √ | √ |

![](https://t3764800.p.clickup-attachments.com/t3764800/21922a15-52f8-4f5e-b40c-1d479595b92c/Screen%20Shot%202023-10-28%20at%202.06.09%20PM.png)

**示例**

有一個路由器，具有兩個輸入接口 I1 和 I2，以及兩個輸出接口 O1 和 O2。有 3 個發送方 S1、S2 和 S3，以及 3 個接收方 R1、R2 和 R3。設 B 是要預留的資源的基本單位。

```plain
                         ________________
                     (a)|                | (c)
      ( S1 ) ---------->|                |----------> ( R1 )
                        |     Router     |      |
                     (b)|                | (d)  |---> ( R2 )
      ( S2,S3 ) ------->|                |------|
                        |________________|      |---> ( R3 )
                                                |


```



#### WF-style reservations

```plain
                             |
               Sends         |       Reserves             Receives
                             |
                             |       _______
         WF( *{4B} ) <- (a)  |  (c) | * {4B}|    (c) <- WF( *{4B} )
                             |      |_______|
                             |
      -----------------------|----------------------------------------
                             |       _______
         WF( *{4B} ) <- (b)  |  (d) | * {3B}|    (d) <- WF( *{3B} )
                             |      |_______|        <- WF( *{2B} )
```

Wildcard sender selection + 共享預訂(shared reservation)

showing the WF style, illustrates two distinct situations in which merging is required.

(1) Each of the two next hops on interface (d) results in a separate RSVP reservation request, as shown; these two requests must be merged into the effective flowspec, 3B, that is used to make the reservation on interface (d).

(2) The reservations on the interfaces (c) and (d) must be merged in order to forward the reservation requests upstream; as a result, the larger flowspec 4B is forwarded upstream to each previous hop.



* * *

(c) <- WF( **{4B} ) :** \* {4B}



(d)<- WF( \*{3B} ) : -|

| ➝ \* {3B} #two requests merged into effective flowspec 3B

(d)<- WF( \*{2B} ) : - |



(c) and (d) merged ➝ **{4B} #** {4B} > \* {3B}, so larger flowspec 4B is forwarded

* * *

####   

#### FF-style reservations

![](https://t3764800.p.clickup-attachments.com/t3764800/f0c44511-2a40-4ae4-bac6-dcc2769128e0/Screen%20Shot%202023-10-28%20at%205.21.29%20PM.png)

```plain
            Sends         |       Reserves             Receives
                          |
                          |       ________
     FF( S1{4B} ) <- (a)  |  (c) | S1{4B} |  (c) <- FF( S1{4B}, S2{5B} )
                          |      |________|
                          |      | S2{5B} |
                          |      |________|
     ---------------------|---------------------------------------------
                          |       ________
                  <- (b)  |  (d) | S1{3B} |  (d) <- FF( S1{3B}, S3{B} )
     FF( S2{5B}, S3{B} )  |      |________|      <- FF( S1{B} )
                          |      | S3{B}  |
                          |      |________|

              Figure 6: Fixed-Filter (FF) Reservation Example
```

Explicit sender selection+ 區分預訂(distinction reservation)

Figure 6 shows Fixed-Filter (FF) style reservations. For each outgoing interface, there is a separate reservation for each source that has been requested, but this reservation will be shared among all the receivers that made the request.

The flow descriptors for senders S2 and S3, received through outgoing interfaces (c) and (d), are packed (not merged) into the request forwarded to previous hop (b). On the other hand, the three different flow descriptors specifying sender S1 are merged into the single request FF( S1{4B} ) that is sent to previous hop (a).



S2 and S3 only one flow descriptors ➝ packed into the request forwarded to previous hop (b)

S1 three different flow descriptors ➝ merged into the single request FF( S1{4B} ) and sent to previous hop (a)



#### SE reservations

![](https://t3764800.p.clickup-attachments.com/t3764800/e301f90c-9c72-4dd7-912f-76ce083c3a1d/Screen%20Shot%202023-10-28%20at%205.40.28%20PM.png)

```plain
            Sends         |       Reserves             Receives
                          |
                          |       ________
     SE( S1{3B} ) <- (a)  |  (c) |(S1,S2) |   (c) <- SE( (S1,S2){B} )
                          |      |   {B}  |
                          |      |________|
     ---------------------|---------------------------------------------
                          |      __________
                  <- (b)  | (d) |(S1,S2,S3)|  (d) <- SE( (S1,S3){3B} )
     SE( (S2,S3){3B} )    |     |   {3B}   |      <- SE( S2{2B} )
                          |     |__________|

            Figure 7: Shared-Explicit (SE) Reservation Example
```

Explicit sender selection + 共享預訂(shared reservation)

Figure 7 shows an example of Shared-Explicit (SE) style reservations. When SE-style reservations are merged, the resulting filter spec is the union of the original filter specs, and the resulting flowspec is the largest flowspec.



S1 最大是 S1{3B}

(S2,S3)最大是 {3B}



> [RFC 2205:](https://www.rfc-editor.org/rfc/rfc2205) [**Resource ReSerVation Protocol (RSVP)**](https://www.rfc-editor.org/rfc/rfc2205)[](https://www.rfc-editor.org/rfc/rfc2205)

# Disadvantage of IntServ

![](https://t3764800.p.clickup-attachments.com/t3764800/05f365b3-e122-443d-b9d8-d0178bddda1c/Screen%20Shot%202023-10-28%20at%202.07.13%20PM.png)

*   **流終止時不會立即釋放資源。** 這是因為 IntServ 需要跟踪所有流的狀態，以便在流需要時可以立即提供資源。但是，這也會導致資源浪費，因為即使流已經終止，但資源仍然被預留。
*   **缺乏可擴展性。** IntServ 需要在網絡中的每個路由器上維護流狀態。這使得 IntServ 在大型網絡中難以部署和管理。
*   **刷新Signaling會消耗bandwidth。** IntServ 需要定期發送刷新**Signaling**來維持 flow state。這會消耗大量的**bandwidth**，尤其是在網絡負載較高時。

# More About Adspec

![](https://t3764800.p.clickup-attachments.com/t3764800/a06ab4a3-ccae-4042-ab14-d53afe1e89d2/Screen%20Shot%202023-10-28%20at%205.48.17%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/243f3968-db30-451e-b929-391c9a6b4968/Screen%20Shot%202023-10-28%20at%205.48.25%20PM.png)

*   Adspec object 是 RSVP 中的一種數據結構，用於在發送方和接收方之間傳遞有關端到端路徑特性的信息。
*   Adspec object 由三個部分組成：
    *   **Default general parameters fragment**：包含以下信息：
        *   最小路徑延遲 (Minimum path latency)
        *   路徑帶寬 (Path Bandwidth)
        *   支持集成服務的跳轉總數 (Integrated Services hop count)
        *   全局中斷位 (Global Break bit)：由發送方(sender)設置。如果路徑上的任何節點都不支持集成服務，則該位設置為 1，並且信息會傳遞給接收方 (receiver)。
        *   Path MTU：路徑的最大傳輸單元 (maximum transmission unit)
    *   **Guaranteed service fragment**：包含以下信息：
        *   Ctot：路徑上速率相關延遲（rate和packet length）的總和
        *   Dtot：路徑上速率無關延遲（例如Router pipeline延遲）的總和
        *   Csum：shaping points 之間 C 的部分總和 (partial sum)
        *   Dsum：shaping points 之間 D 的部分總和(partial sum)
    *   **Controlled load service fragment**：Adspec 中沒有額外的數據



Adspec object 在 RSVP 中用於以下目的：

*   幫助接收方確定端到端路徑的特徵
*   允許路由器修改 Adspec object 以反映路徑的實際特性
*   幫助接收方確定是否接受 RSVP 流

以下是一個 Adspec object 的示例：

```plain
Adspec object {
  Default general parameters fragment {
    Minimum path latency: 10ms
    Path bandwidth: 100Mbps
    Integrated Services hop count: 5
    Global break bit: 0
    Path MTU: 1500 bytes
  }
  Guaranteed service fragment {
    Ctot: 1ms
    Dtot: 5ms
    Csum: 0.5ms
    Dsum: 2.5ms
  }
  Controlled load service fragment {
    // No extra data
  }
}
```



# One Pass v.s. One Pass with Advertising(OPWA)

![](https://t3764800.p.clickup-attachments.com/t3764800/1a37cb17-bc69-4472-a5b1-9e88e73e1762/Screen%20Shot%202023-10-28%20at%206.56.48%20PM.png)

*   **一次性傳輸模型(One pass model)**不支持**確定****path特徵****(determine the characteristics of path)或****path是否能夠支持所需 QoS 的功能****。**
*   **使用 OPWA，發送方在其 PATH 消息中包含一個 Adspec 來收集有關路徑的信息。**



一次性傳輸模型是一種 RSVP 預訂模型，其中發送方和接收方只交換一次消息來建立預訂狀態。這種模型的優點是高效，但它不支持確定路徑特徵或路徑是否能夠支持所需 QoS 的功能。



OPWA（One Pass With Advertising）是一種增強功能，它允許發送方在其 PATH 消息中包含一個 Adspec。Adspec 是一種數據結構，用於在發送方和接收方之間傳遞有關端到端路徑特性的信息。



通過在 PATH 消息中包含 Adspec，發送方可以收集有關路徑的信息，包括路徑帶寬、路徑延遲和路徑是否支持集成服務。這些信息可以幫助發送方確定路徑是否能夠支持所需 QoS。

以下是 OPWA 工作原理的一個概述：

1. 發送方發送一個 PATH 消息，其中包含一個 Adspec。
2. 路由器在 PATH 消息中修改 Adspec，以反映路徑的實際特性。
3. 接收方收到 PATH 消息後，檢查 Adspec，以確定路徑是否能夠支持所需 QoS。
4. 如果路徑能夠支持所需 QoS，則接收方發送一個 RESV 消息來建立預訂狀態。
5. 如果路徑無法支持所需 QoS，則接收方發送一個 REJECT 消息。



# Slack Term (**鬆弛因子**)

![](https://t3764800.p.clickup-attachments.com/t3764800/5272009f-56ae-45ca-a7b0-888cff67ccac/Screen%20Shot%202023-10-28%20at%207.01.52%20PM.png)

*   Slack term 是一種用於補償增加的延遲的參數。它用於保證服務（Guaranteed Service），並在 RSVP 消息的 RSpec 中指定。
*   假設一個流需要 2.5 Mbps 的bandwidth。slack term可用於補償(compensate)當前bandwidth reservation（即delay credit）下的增加的延遲。
*   slack term 是理想延遲(desired delay)與實際延遲(actual delay)之間的差值。
    *   desired delay：指flow所需的最大延遲，
    *   actual delay：flow在當前bandwidth reservation 下的實際延遲。

```plain
Slack term = desired delay - actual delay
```



Slack term可以用於以下目的：

*   允許 Router 在不影響流 QoS 的情況下進行緩衝和整形。
*   允許 Router 在網絡負載較高時降低flow bandwidth，以防止擁塞。
*   允許 Router 在網絡故障時重新路由 flow，而不會影響流的 QoS。

Slack term的值通常以微秒為單位指定。Slack term越大，路由器就越有靈活性來處理延遲變化。但是，Slack term越大，Flow的bandwidth就越低。

Slack term是一個重要的 RSVP 參數，可用於為保證服務流提供 QoS 保證。以下是一個鬆弛因子的示例：

```plain
RSpec {
  Flowspec {
    Bandwidth: 2.5 Mbps
    Delay: 10ms
  }
  Slack term: 5ms
}
```

這個示例指定了 2.5 Mbps 的帶寬和 10ms 的延遲。鬆弛因子為 5ms，這意味著路由器最多可以增加 5ms 的延遲，而不會影響流的 QoS。
