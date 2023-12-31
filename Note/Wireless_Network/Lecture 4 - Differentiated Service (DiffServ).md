---
title: "Wireless-Multimedia-Network"
permalink: /Wireless-Multimedia-Network/4-DiffServ/
layout: default
---
# Lecture 4 - Differentiated Service (DiffServ)

![](https://t3764800.p.clickup-attachments.com/t3764800/c770f1ab-e8c1-4c85-ae96-4e4fff8d5a57/Screen%20Shot%202023-10-28%20at%208.50.01%20PM.png)

# Comparisons of IntServ and DiffServ

![](https://t3764800.p.clickup-attachments.com/t3764800/052ed15f-889d-4172-ab47-1c66d923d782/Screen%20Shot%202023-10-28%20at%208.52.40%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/508e01e4-2719-4881-b207-8d212a966f3f/Screen%20Shot%202023-10-28%20at%208.52.48%20PM.png)



以下是 DiffServ 和 IntServ 的對比表：

IntServ （每個flow提出自己的需求）:

Service model (Guarantee, control load):

1\. Admission control <➝QOS routing 對新的資料留流提出的需求確認到底OK不OK

2\. Admission control 模擬網路資源還剩多少 ➝ 找路徑的方法 (simple sum, measured sum, Acceptance sum)

3\. RSVP reservation ➝ 沿途把頻寬留下 （FF,WF,SE）

4\. RSVP 登記到 Reservation Table

5\. Flow Indentification = classification : 因為預留的頻寬只有該封包（per flow）的資料留流可以使用，所以要對收到的封包做分類（classification）看封包有沒有再在reservation table做預留資源

6\. 分類完後放到queue裡面再scheduling將他們送出➝ 因為有很多資料流近來，但都要從同個interface出去所以要做scheduling (公平排程WFQ, 截止期限EDF, 基於速率RATE-based)



特點:

1\. Per flow

2\. Receiver initiated

3\. 將路由(routing)與預留(reservation process)分開

| 特性 | DiffServ | IntServ |
| ---| ---| --- |
| 資源分配 | 對aggregated traffic（class）而不是個別flow進行資源分配 | 對個別flow進行資源分配 |
| 流量管制和類別化轉發 | 僅在邊緣的邊界節點(boundary nodes)對流量進行分類(classify)並標記(mark)packet；內部節點(interior nodes)使用packet header 編碼的轉發類別(forwarding classes)來確定相應的處理方式。 | 所有節點都執行packet classification和scheduling。 |
| 定義forwarding behavior 而不是 services | 定義forwarding treatment（i.e. forwarding class），而不是end-to-end services。 | 定義services。packet的處理方式不是標準的一部分。 |
| 通過Provisioning而不是reservation來提供保證 | 通過調配(Provisioning)和優先級(Prioritization)（實現不同level of services）來提供資源保證。 | 通過逐 flow 資源 reservation來實現（實現絕對保證）。 |
| 重點關注服務水平協議而不是動態信令 | 目的是確保客戶和服務提供商之間的長期 SLA。(long term static resource reservation)<br>\-＞ 先定合約 根據合約搭配provision將服務調整到對應的SLA合約 | 相反，IntServ 提供動態資源預留(dynamic resource reservation)。-＞ 不先定合約，per flow進來才做 reservation |
| 關注 single domain 而不是end-to-end | DiffServ 在 Internet 中的部署可以是逐步(incremental)的。 | IntServ 模型本質上是 end-to-end的。 |

#   

# Conceptual Operations

![](https://t3764800.p.clickup-attachments.com/t3764800/b1e17d44-5205-4940-ab96-9dd4d9ebcdc9/Screen%20Shot%202023-10-28%20at%209.11.11%20PM.png)

當流量進入 DiffServ 網絡時，它會：

*   首先被分類
    *   **分類**是指根據流量的某些特徵（例如源 IP 地址、目的 IP 地址、端口號、協議類型等）將流量分組。分類可以幫助網絡管理員識別和管理不同的流量類型。
*   可能會被調整
    *   根據流量的分類結果對流量進行處理，例如限速、丟棄、整形等。調整可以幫助網絡管理員控制流量的行為，防止網絡擁塞。
*   被分配一個 DSCP（類別）
    *   DSCP 值決定了數據包在網絡中的轉發優先級。
*   被轉發
    *   數據包從一個節點發送到另一個節點。轉發過程中，路由器會根據 DSCP 值來選擇合適的轉發路徑。



# Basic Approach of DiffServ Framework

![](https://t3764800.p.clickup-attachments.com/t3764800/ff49a7be-d363-47bb-ad4d-823a77137eda/Screen%20Shot%202023-10-28%20at%209.17.42%20PM.png)

*   **在 DiffServ（差異化服務）中，流量被分為少量稱為轉發類別的組(small numbers of groups called forwarding classes)。**
*   forwarding **class編碼在 IP packet header中。**
*   **每個forwarding class代表預定義的轉發處理。包括****丟棄優先級、**最大延遲**和****帶寬(bandwidth)分配****。➝** Forwarding class 是由 **MF classifier** 來定義的。
*   **Boundary node（edge node）和 interior nodes（core node）具有不同的職責：**
    *   邊界路由器 (boundary router)（出口入口路由器）執行packet classification和流量調整(traffic conditioning)。
    *   內部路由器 (Interior router)（core router）執行基於類別的數據包轉發(class-based packet forwarding)。



MF classifier 和 BA classifier 的關係：

*   MF classifier 是將流量分類到不同forwarding class的第一步。
*   BA classifier 是將具有相同forwarding class的流量聚合到 BA(behavior aggregate具有相同 DSCP 的所有 packet) 中的第二步。
*   假設我們有以下兩個 forwarding class：
    *   **Best Effort (BE)**：盡力而為的轉發類別，沒有任何 QoS 保證。
    *   **Expedited Forwarding (EF)**：加速轉發類別，提供最低帶寬和最低延遲保證。
*   MF classifier 可以使用以下 DSCP 值來定義這兩個 forwarding class：
    *   **BE：00**
    *   **EF：01**
    *   BA classifier 可以將具有相同 DSCP 值的流量聚合到 BA 中。例如，所有 DSCP 值為 00 的流量都將被聚合到 BE BA 中，所有 DSCP 值為 01 的流量都將被聚合到 EF BA 中。



MF classifier 更適合需要高精度分類的應用，例如 VoIP 和視頻流。分類字段可以包括源和目的 IP 地址、port、Protocol等。

BA classifier 更適合需要高分類速度的應用，例如 FTP 和 P2P 流量。

以下是 MF classifier 和 BA classifier 的示例：

*   MF classifier 可以用來對流量進行以下分類：
    *   根據源和目的 IP 地址來分類為內部流量和外部流量
    *   根據端口號來分類為 HTTP 流量、FTP 流量和 DNS 流量
    *   根據協議類型來分類為 TCP 流量和 UDP 流量
*   BA classifier 可以用來將所有流量分為兩類：
    *   Best Effort流量
    *   保證服務流量

以下是 MF classifier 和 BA classifier 的對比：

| 特性 | MF classifier | BA classifier |
| ---| ---| --- |
| 分類字段 | 多個字段 | 單個字段 |
| 分類精度 | 高 | 低 |
| 分類速度 | 慢 | 快 |
| 應用場景 | 需要高精度分類的應用 | 需要高分類速度的應用 |

# Per-Hop Behaviors(PHBs)

![](https://t3764800.p.clickup-attachments.com/t3764800/9dce0ae8-eaa7-48f2-ac6f-734d26ba2964/Screen%20Shot%202023-10-28%20at%209.33.04%20PM.png)

*   PHB（Per-Hop Behavior，逐跳行為）用於描述 DS 節點上外部可觀察的forwarding behavior。
*   每個 PHB 都由一個 6-bit value表示，稱為 DSCP（Differentiated Services Code Point，差異化服務代碼點）
*   具有相同 DSCP 的所有 packet 都被稱為behavior aggregate (BA)，並且它們會收到相同的轉發處理。
*   以下是一些 PHB 的示例：
    *   **保證 BA 的minimal bandwidth 分配為 x%（絕對值）。**
    *   **保證 BA 的minimal bandwidth 分配為 x%，並按比例公平共享任何多餘的鏈路容量(excess link capacity)（相對值）。**

# Services

![](https://t3764800.p.clickup-attachments.com/t3764800/d3c7c469-faad-4259-b281-776c8487cb13/Screen%20Shot%202023-10-28%20at%209.43.12%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/98dadb1f-04d7-40a4-98aa-1760b3d8e186/Screen%20Shot%202023-10-28%20at%209.43.20%20PM.png)

*   **服務對客戶可見，而 PHB 在網絡元素內部隱藏。**
*   **在 DiffServ 中，****服務以customer及其service provider之間的service level agreement (SLA) 的形式定義****。SLA 中的重要元素之一是Traffic Conditioning agreement (TCA)。**
*   **TCA 詳細說明了****流量特徵(traffic profile)****和****控制操作(policing action)****的****服務參數(ser**vice parameter**)****。**
    *   **流量特徵(traffic profile)****，例如每個class的 token bucket parameters**
    *   **性能指標(Performance metrics)，例如吞吐量(throughput)、延遲(delay)和丟棄優先級(drop priority)**
    *   **對不合規(non-conformant) packet 的操作**
    *   **Service Provi**der**提供的額外的標記(additional marking)和整形服務(shaping service)**
*   **除了 TCA 之外，SLA 還可能包含其他服務特性(service characteristics)和商業相關協議(business-related agreement )，例如可用性(availability)、安全性(security)、監控(monitoring)、會計(accounting)、定價(pricing)和計費(billing)。**
*   **SLA 可以是靜態(static )的或動態(dynamic)的。➝ 跟operator說什麼時候要加流量**
*   **Service可以用定量(quantitative)或定性(qualitative)術語來定義。**
    *   **Quatitative 定量：以絕對值指定參數，例如 5 秒的最大延遲**
    *   **Qualitative 定性：使用相對術語，例如更低的延遲**
*   以下是服務和 PHB 的一些區別：

| 特性 | 服務 | PHB |
| ---| ---| --- |
| 可見性 | 對客戶可見 | 在網絡元素內部隱藏 |
| 定義 | 以 SLA 的形式定義 | 由 PHB 組成 |
| 參數 | **traffic profile**、**Performance metrics**、控制操作和**additional marking**和**shaping service** | Forwarding Behavior |
| 範圍 | 端到端 | 每個節點 |

# Differentiated Services Field

![](https://t3764800.p.clickup-attachments.com/t3764800/6d5bde87-e089-4705-b62c-e394ea65eeb3/Screen%20Shot%202023-10-28%20at%2011.47.12%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/68d12825-d96d-4c42-a0bb-fe12bd3949f9/Screen%20Shot%202023-10-28%20at%2011.47.28%20PM.png)

*   **DiffServ 使用 IP packet header 中的** 6 bits **來 encoded forwarding treatment。**
*   當前的 IP 數據包標頭包含一個 8 位的字段，稱為 IP TOS 字段：3 位服務類型（TOS）\[0-2\]、3 位優先級（表示流量的優先級）\[3-5\] 和 2 位未使用的位\[6-7\]。
*   DiffServ 將現有的 TOS 字段重新定義為指示forwarding treatment：
    *   DS 字段的前 6 bits 作 DSCP，以在每個 DS 節點為數據包編碼 PHB。
    *   剩餘的 2 位保留供以後使用。
    *   DSCP 應視為index，DSCP 到 PHB 的mapping必須可配置(configurable)。
    *   code point space 分為 3 個pool：
        *   一組 32 個推薦的codepoints進行標準化。
        *   一組 16 個代碼點用於實驗或本地使用。
        *   一組 16 個代碼點可供實驗和本地使用，但如果池 1 耗盡，可能會進行標準化。

![](https://t3764800.p.clickup-attachments.com/t3764800/1e7365fe-70c8-4e20-bd2f-da1200c7ec9b/Screen%20Shot%202023-10-29%20at%2012.07.33%20AM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/1696c026-3a47-424d-aac9-51c1d2c6e0c6/Screen%20Shot%202023-10-29%20at%2012.07.50%20AM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/10865ede-009a-426c-91d5-bd8370517062/Screen%20Shot%202023-10-29%20at%2012.08.02%20AM.png)

*   **默認 PHB 代碼點**
    *   向後兼容現有的盡力而為轉發處理。
    *   屬於默認轉發類別的數據包可能會被發送到網絡中，而不會進行任何控制，並且網絡將盡可能多地、盡可能快地傳遞這些數據包。
    *   其他轉發類別比默認轉發類別具有更高的網絡資源優先級。
    *   為默認轉發類別保留了一些最低限度的帶寬，以避免飢餓。
    *   分配的代碼點是 000000。
*   **類別選擇器代碼點**
    *   在一定程度上保持與 IP 優先級字段的已知現有使用的向後兼容性。
    *   我們將這組 PHB 命名為 **class selector** PHB。
    *   分配的代碼點：xxx000
    *   eight class selectors PHBs 至少應產生兩個不同的forwarding class。
    *   代碼點數值值較大的 PHB 必須有優於或等於數值值較小的 PHB 的轉發處理。
*   **當前的代碼點分配（已由 IETF 標準化）**
    *   保證轉發 (AF-Assured Forwarding)（RFC 2597 和 RFC 3260）：特定條件下保證交付。
    *   加速轉發 (EF-Expedited Forwarding)（RFC 3246）：專門用於低損耗、低延遲的流量。

# Traffic Classification and Conditioning

![](https://t3764800.p.clickup-attachments.com/t3764800/03b04a8c-c977-41d0-a5d4-0108c8c95a62/Screen%20Shot%202023-10-29%20at%2012.21.28%20AM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/1ace9ffc-eaf2-4dfa-82c7-56d8dd9e913d/Screen%20Shot%202023-10-29%20at%2010.58.47%20AM.png)

*   **邊界路由器(boundary router)的兩個職責是分類(Classification)和調製(conditioning)。➝ MF Classifier**
*   分類模塊(Classification Module)包含一個分類器(classifier)和一個標記器(marker)。
*   Classifier根據一些predefined rules將入 incoming packet stream 分成多個group。
*   有兩種基本類型的Classifier：行為Behavior Aggregate (BA) 或 multi-field (MF) 分類器。
*   BA 是最簡單的 DiffServ 分類器，它僅(solely)根據 DSCP 值選擇數據包。
*   MF 使用 header 中 五 tuple（source address、destination address、source port、destination port、protocol ID）的一個或多個fields的組合進行分類。

![](https://t3764800.p.clickup-attachments.com/t3764800/9022c113-0c6e-423d-9e6a-941c1b9ea304/Screen%20Shot%202023-10-29%20at%2011.05.58%20AM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/3ccbf969-689c-4767-bf23-776fe4923782/Screen%20Shot%202023-10-29%20at%2011.06.14%20AM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/73b6cb92-b28d-4ab5-ac01-16eeb96ec5cb/Screen%20Shot%202023-10-29%20at%2011.06.31%20AM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/cf248cd6-aba6-47d9-b0d6-f28082dfc886/Screen%20Shot%202023-10-29%20at%2011.06.42%20AM.png)

*   **Traffic Conditioner用於強制執行Customer和service provider之間的 TCA。**
*   **Traffic Conditioner**由以下 4 個基本元素組成：測量器(Meter)、標記器(marker)、整形器(shaper)和丟棄器(dropper)。
    *   **測量器(Meter)**：
        *   Meter根據流量特徵(traffic profile)來測量來自客戶的流量(traffic flow)。
        *   符合特徵(In-profile)的packet被允許進入網絡，而超出特徵(out-profile)的packet則根據 TCS 進行調製(conditioned)。
        *   大多數測量器(meters)都以token bucket的形式實現。
    *   **標記器(Marker)**：
        *   Marker將 packet 的 DS field 設置為特定的 DSCP 值，並將 marked packet添加到 forwarding class 中。
        *   Markers可以對 unmarked packet 或已marked packet 進行操作。
        *   Marker 可以由Application本身、LAN 的first-hop Router或服務提供商的Boundary Router 來完成。
        *   在使用不同 DSCP 的兩個管理域(administrative domain)之間進行重新標記(remark)是必要的。
        *   如果用 DSCP 標記的數據包收到 worse forwarding treatment ➝ PHB 降級(PHB demotion)（通常）。
        *   如果收到 better forwarding treatment，➝ PHB 升級 (PHB promotion)。
        *   通常，Boundary Router會將 out-of-profile packet 降級(demote)為具有worse forwarding treatment 的 DSCP。
    *   **整形器(Shaper)**：
        *   **Shaper**會延遲不合規(non-conformant) packet，以便使flow 符合約定(agree-on)的流量特徵(traffic profile)。
        *   Marker 會標記不合規的packet 並讓它們進入網絡，而Shaper則會阻止這些數據包進入網絡，直到流符合流量特徵。
        *   Shaper 是一種比 MArker 更強的控制形式。
    *   **丟棄器(Dropper)**：
        *   丟棄是另一個可以應用於超出特徵的數據包的操作。
        *   對於整形器，它會暫時緩衝數據包，而對於丟棄器，它只會丟棄超出特徵(out-of-profile)的數據包。
        *   drop 比 shape 更容易實現。
    *   流量分類器(traffic classifier)和調製器(conditioner)的位置：![](https://t3764800.p.clickup-attachments.com/t3764800/98384a12-651b-418f-a853-f83bec57f483/Screen%20Shot%202023-10-29%20at%2011.45.18%20AM.png)
        *   通常位於 DS 進出口節點 (ingress & egress nodes)，流量在這些node之間跨越domain。
        *   在 source domain 內：
            *   source domain 的 traffic Source 和 intermediate nodes可以在數據包離開 domain之前（由主機host或第一跳路由器）對其進行分類和標記。這稱為預標記(premarking)。
            *   premarking允許 source domain 根據 local policy（例如，CEO 的 PC 或關鍵任務服務器）對數據包進行分類。
        *   At the boundary of a DS domain：
            *   下游域的入口節點(ingress node of the downstream domain)會執行所有必要的classification和conditioning。
            *   如果兩個domain對 PHB 使用不同的codepoints，則必須在邊界重新標記(remark)任何預標記的數據包，上游域的出口節點或下游域的入口節點都可以執行mapping。
        *   In interior DS nodes：
            *   在一些嚴重擁塞(congested)的熱點(hot spot)，可以應用額外的流量控制或在某抵達模式。

# Assured Forwarding（保證轉發）

![](https://t3764800.p.clickup-attachments.com/t3764800/619167d2-53d5-4477-ab1c-32e29c0f51ac/Screen%20Shot%202023-10-29%20at%2011.47.05%20AM.png)

*   **AF 的基本思想來自 RIO 方案。**
*   什麼是 RIO？
    *   服務特徵(service profile)指定了用户的預期容量(expected capacity)。
    *   Boundary nodes監控流量並將數據包 tag 為 in or out of their profiles。
    *   在擁塞期間，out of profile的數據包將首先被丟棄。
    *   服務提供商應提供其網絡以滿足所有in-profile packet 的預期容量，並且僅在有過剩bandwidth時允許 out-of-profile packet。

![](https://t3764800.p.clickup-attachments.com/t3764800/be0e1242-e263-46dc-a94e-9a781b731afc/Screen%20Shot%202023-10-29%20at%2011.47.19%20AM.png)

RIO 使用以下步驟來管理流量：

1. 邊界節點根據服務特徵將流量分類為符合特徵流量和超出特徵流量。
2. 邊界節點向符合特徵流量的數據包分配高優先級，向超出特徵流量的數據包分配低優先級。
3. 在擁塞期間，邊界節點會首先丟棄超出特徵流量的數據包。

![](https://t3764800.p.clickup-attachments.com/t3764800/5c6e0c8c-24a1-4115-804b-13ca233d64d6/Screen%20Shot%202023-10-29%20at%2012.02.44%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/569ac90f-0e76-4bc6-9f4b-a49d04db7a71/Screen%20Shot%202023-10-29%20at%2012.03.03%20PM.png)

*   **AF 標準將 RIO 中的基本內/外標記擴展為四個轉發類別的結構，並且在每個轉發類別中，有三個丟棄優先級。**
*   **每個轉發類別都分配了一定量的緩衝區和帶寬。**
*   **當 AF 轉發類別中的積壓數據包超過指定閾值時，將首先丟棄具有最高優先級的數據包，然後丟棄具有較低丟棄優先級的數據包。**
*   **請注意，比較兩個 AF 類別中的兩個丟棄優先級可能沒有意義。**
*   **AF 實施示例**
    *   假設鏈路容量為 100 Mbps
    *   四個轉發類別的最小帶寬要求分別為 2、4、8 和 16 Mbps
    *   按比例共享過剩帶寬
    *   權重： (1:2:4:8)
    *   過剩帶寬份額分別為 4 Mbps、8 Mbps、16 Mbps 和 32 Mbps

**AF 實施步驟**

1. 根據服務特徵將流量分類為四個轉發類別中的其中一個。
2. 將每個轉發類別中的數據包分配給三個丟棄優先級之一。
3. 為每個轉發類別分配一定的緩衝區和帶寬。
4. 在擁塞期間，首先丟棄具有最高丟棄優先級的數據包，然後丟棄具有較低丟棄優先級的數據包。
5. 按比例共享過剩帶寬。

# Expedited Forwarding（加速轉發）

![](https://t3764800.p.clickup-attachments.com/t3764800/b2d7318e-9de2-4f0a-bfbd-e1127ee2cbfd/Screen%20Shot%202023-10-29%20at%2012.15.53%20PM.png)

*   **EF 用於創建低損耗、低延遲和保證帶寬服務。**
*   EF 被定義為一種轉發處理，其中聚合的數據包從任何 DS 節點的發包率必須等於或超過可配置的速率。
*   EF 流量應獲此速率，而不管節點嘗試傳輸的任何其他流量的強度。
*   EF 流量可以在一定範圍內搶占其他流量。分配的代碼點是 101110。
*   

F 流量將獲得最低的帶寬和延遲，並且不會受到其他流量的影響。

EF 的一些優點包括：

*   低損耗：EF 流量將被優先處理，因此其丟包率將較低。
*   低延遲：EF 流量將被優先轉發，因此其延遲將較低。
*   保證帶寬：EF 流量將獲得最低帶寬，因此其性能不會受到其他流量的影響。

EF 的一些缺點包括：

*   資源消耗：EF 流量將優先使用網絡資源，因此可能會影響其他流量的性能。
*   配置複雜性：EF 需要仔細配置以確保其有效運行。



# End-to-End Resource Management

## IntServ over DiffServ

![](https://t3764800.p.clickup-attachments.com/t3764800/4b206286-7dbf-43d5-a76b-73053d971d7e/Screen%20Shot%202023-10-29%20at%2012.20.54%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/7c08a2f4-3353-407e-8412-e1ed82167551/Screen%20Shot%202023-10-29%20at%2012.21.15%20PM.png)

*   **DiffServ 上的集成服務**
*   兩層資源分配模式(two-tier resource allocation mode)：DiffServ 將聚合資源(aggregated resources)分配給核心網絡(core networks)中的客戶網絡(customer network)；IntServ 以更細的粒度(granularity)將資源分配給個別用戶或流。
*   **在網絡的邊界，IntServ 請求被映射到底層 DiffServ 網絡，包括以下映射：**
    *   為請求的服務選擇合適的 PHB 或 PHB 組
    *   在 DiffServ 網絡的邊緣執行適當的控制
    *   從 DiffServ 網絡導出 IntServ 參數
*   **IntServ over DiffServ 的示意性示例：**
    *   一個擁有 4 個路由器和 2 個 LAN 的企業網絡
    *   接入路由器將企業網絡連接到其 ISP 並負責流量分類
    *   當發件人發起交易時，它會與接收方交換 RSVP PATH 和 RESV 消息
    *   僅支持 DiffServ 的 ISP 會忽略 RSVP 消息
    *   當 RESV 消息通過接入路由器時，它會諮詢策略服務器以決定是否允許訪問
    *   假設企業已支付了 10 Mbps 的服務，並且已分配了 9 Mbps，則會允許新的預訂少於 1 Mbps
*   **策略服務器可以決定如何將 IntServ 請求映射到 DiffServ 模型。**

## Interdomain bandwidth allocation（**域間帶寬分配**）

![](https://t3764800.p.clickup-attachments.com/t3764800/84d7c856-4b17-416f-a729-4a5a475ccf85/Screen%20Shot%202023-10-29%20at%2012.30.36%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/9ccc6895-925d-4fec-b4db-e6269bbdd25d/Screen%20Shot%202023-10-29%20at%2012.32.06%20PM.png)

**域間帶寬分配（**Interdomain bandwidth allocation**）**

*   不同的domain通常由不同的所有者和管理員單獨擁有和管理，並且任何兩個不同域之間的關係由 SLA（服務水平協議）規定。
*   SLA 可以動態且不頻繁地更改，而帶寬經紀人 (BB, Bandwidth Broker) 方法可以實現動態的域間資源協商(dynamic interdomain resource negotiation)。
*   一個示意性示例：
    *   骨幹網(backbone)由 3 個 ISP 和一個企業網絡組成，該企業網絡可以與任何 ISP 中的許多接收者通信。
    *   企業網絡的 BB 對其自身的用戶發起的預訂請求進行准入控制。
*   本質上，BB 作為其 ISP 的資源管理代理，並執行以下 3 個主要功能：
    *   准入控制(Admission Control)：決策基於網絡的預定義配置算法。
    *   策略控制(Policy Control)：處理行政（例如，優先級和特殊限制）和定價策略。
    *   預訂彙總(Reservation Aggregation)：從用戶收集多個請求，並為資源提出單個請求，以提高系統的可擴展性。
*   BB 方法的缺點是 BB 必須知道新流量的去向才能提出準確的帶寬請求。
