---
title: "Wireless-Multimedia-Network"
permalink: /Wireless-Multimedia-Network/5-MPLS/
layout: default
---
# Lecture 5 - MultiProtocol Label Switching (MPLS)

![](https://t3764800.p.clickup-attachments.com/t3764800/9d957922-9137-4299-93a6-5a9426f762f0/Screen%20Shot%202023-10-29%20at%203.22.03%20PM.png)

# History of Label Switching

![](https://t3764800.p.clickup-attachments.com/t3764800/c7554bf9-7b50-46f6-978d-0962520e90cc/Screen%20Shot%202023-10-29%20at%203.22.30%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/b0e79d61-65fc-4874-b426-c969473fc0d1/Screen%20Shot%202023-10-29%20at%203.22.39%20PM.png)

*   **Internet 中的** **IP forwarding****基於datagram model。**
    *   **datagram model**是一種無連接的通信模型，其中packet是獨立的，不需要在發送之前建立連接。
*   ATM 在 Internet 骨幹網中廣泛部署，並且是connection-oriented（virtual circuit）。
    *   ATM 指的是Asynchronous Transfer Mode（異步傳輸模式）。ATM 是一種connection-oriented的通信技術，其中packet在發送之前需要建立連接。ATM 使用虛擬電路（VC）來標識連接。
*   MPLS 代表了數據網絡中兩種截然不同的方法（datagram 和 virtual circuit）的融合。
    *   MPLS = datagram + virtual circuit
*   已經標準化了多種在 ATM 網絡上運行 IP 的方法，但這些方法都很繁瑣(cumbersome)。
*   對更無縫(seamless)的 IP/ATM 集成的需求導致了label switching的部署。
*   Label Switching 使用插入在 packet header 中的短、fixed label 來forward packet。
*   標籤交換路由器 (LSR, Label Switching Router) 使用 Label 作為索引(index)來查找下一個跳躍和相應的新label。
*   packet 在網絡中穿越的路徑由標籤值(labeb values)的轉換來定義，該路徑稱為標籤交換路徑 (LSP)。
*   IETF MPLS 工作組成立的目的就是標準化封裝格式(encapsulation format)和標籤分發協議(label distribution protocols)。



Label Switching 的優點：

*   高性能：標籤交換比傳統 IP 路由更快，因為它不需要在每跳都查找路由表。
*   可擴展性：標籤交換可以支持比傳統 IP 路由更大的網絡。
*   靈活性：標籤交換可以提供各種 QoS 服務，例如流量隔離、優先級和帶寬保證。

Label Switching 的缺點：

*   複雜性：標籤交換的配置和管理比傳統 IP 路由更複雜。
*   資源消耗：標籤交換需要在每個 LSR 上維護一個標籤轉換表，這可能消耗大量內存和 CPU 資源。



# MPLS Motivations

![](https://t3764800.p.clickup-attachments.com/t3764800/2b4a9736-30ec-4258-8fad-d8bd34f1113a/Screen%20Shot%202023-10-29%20at%203.42.16%20PM.png)

*   **雖然 IP/ATM 集成是 label switching 發展的主要驅動力，但 IETF 工作組認識到標籤交換可能有可能：**
    *   **簡化 packet forwarding process**
        *   LSR 只需查找Label Switching Table 即可確定 next hop，而不需要查找routing table 。這可以提高數據包轉發的速度和效率。
    *   **支持標籤交換中的顯式路徑**
        *   LSR 可以使用標籤來指定數據包的顯式路徑。這對於需要 QoS 保證的應用程序（例如 VoIP 和視頻流）很有用。

# Simpler Forwarding Paradigm

![](https://t3764800.p.clickup-attachments.com/t3764800/3a94d0f3-09e2-4acd-9da6-df18d772ebbf/Screen%20Shot%202023-10-29%20at%203.47.31%20PM.png)

*   **更簡單的轉發機制**
    *   傳統的 IP packet forwarding ：classification和route查找
    *   Label Switching：對label進行簡單的精確匹配，從而提高可擴展性(scalability)
    *   **與協議無關(Protocol-independent)的轉發 ➝ label switching** 可以用於轉發任何協議的數據包，包括 IP、TCP、UDP 等。
        *   在現有的 IP 架構中，路由和轉發是緊密耦合的
        *   IPv4 → IPv6，我們需要更改轉發方案
    *   **轉發粒度(granularity)**
        *   當前的 IP 路由是基於目的地的(destination based)：所有具有相同網絡號的數據包都被分組並以相同的方式處理
        *   label switching允許通過設置具有不同轉發處理的 LSP 來支持當前基於目的地的粒度之外的更多粒度

> 在傳統的 IP 路由中，路由器需要根據數據包的協議來決定如何轉發數據包。  
> 例如，路由器需要知道數據包是 IP 數據包還是 ATM 數據包，才能確定數據包的下一跳。  
> 標籤交換通過將數據包封裝成一個通用的標籤交換數據包來解決這個問題。  
> 標籤交換數據包中包含一個標籤，該標籤用於識別數據包。  
> 標籤交換路由器只需要根據標籤來決定如何轉發數據包，而不需要知道數據包的協議。



# Label Switching (Concept Label Switching**概念)**

![](https://t3764800.p.clickup-attachments.com/t3764800/4a95d472-e57b-4112-8397-27d41057b0c5/Screen%20Shot%202023-10-29%20at%203.58.50%20PM.png)

*   控制組件(control component)通過構建轉發表 (construction of forwarding table)可以被建模為構建一組 FEC 和每個 FEC 的下一個跳轉。
*   **轉發等價類 (FEC, Forward Equivalence Class)**
    *   將數據包劃分為一組類別。
    *   每個類別稱為 FEC。
    *   同一 FEC 中的數據包具有相同的處理。
    *   例如，基於目的地的 IP 路由。

FEC 是 Forward Equivalence Class 的縮寫，意思是轉發等價類。它是標籤交換技術中一個重要的概念。FEC 是將數據包劃分為具有相同轉發處理的組。這允許 LSR 僅根據 FEC 來轉發數據包，而不需要知道數據包的協議或其他詳細信息。

FEC 可以基於不同的維度進行劃分。例如，FEC 可以基於以下因素進行劃分：

*   目的地 IP 地址
*   服務質量 (QoS) 要求
*   安全策略
*   應用程序類型

FEC 的示例：

*   所有具有相同目的地的 IP 數據包都屬於同一個 FEC。
*   所有 VoIP 數據包都屬於同一個 FEC。
*   所有具有高優先級的安全數據包都屬於同一個 FEC。

REFERENCE:

[Multi-Protocol Label Switching (MPLS)](https://www.jannet.hk/multi-protocol-label-switching-mpls-zh-hant/)

![](https://t3764800.p.clickup-attachments.com/t3764800/ab501376-202e-4509-8e61-a14caa9974fc/Screen%20Shot%202023-10-29%20at%204.33.33%20PM.png)![](https://t3764800.p.clickup-attachments.com/t3764800/bb643eb3-6253-4a72-b791-e63765443e4d/Screen%20Shot%202023-10-29%20at%204.33.45%20PM.png)

# MPLS

![](https://t3764800.p.clickup-attachments.com/t3764800/dbea5178-5956-4c2c-9bd5-cd027bc14254/Screen%20Shot%202023-10-29%20at%204.35.25%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/0b01f0df-1b9d-491b-8075-32eefdfaa0e1/Screen%20Shot%202023-10-29%20at%204.35.48%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/e95cd1c5-68b7-4489-b2b1-5823f33f4bf0/Screen%20Shot%202023-10-29%20at%204.36.14%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/a68ddc91-a4b7-446b-bdbf-9a85b92e0122/Screen%20Shot%202023-10-29%20at%204.36.21%20PM.png)

*   **標籤（Label）**
    *   一個短的、固定長度的、邏輯上有意義的識別符(identifier)，用於識別 FEC 並 forward packet。
    *   沒有內部結構。
*   **標籤和 FEC 之間的綁定**

![](https://t3764800.p.clickup-attachments.com/t3764800/ee3287ef-a24e-4298-a841-6ad7788ae84b/Screen%20Shot%202023-10-29%20at%205.02.11%20PM.png)

*   一對一映射 (One-to-One mapping)
*   上游 LSR（標籤交換路由器）：例如，路由器 A
*   下游 LSR：例如，路由器 B
*   出站標籤：例如，F
*   入站標籤：例如，L
*   label由下游(downstream)分配，並且綁定從下游分發到上游。

*   **標籤分發協議 (LDP, Label distribution protocol)\[LSP setup\]**
    *   兩台 LSR 學習彼此的 MPLS 功能並交換標籤映射信息(label-mapping info)的procedure。
*   **Label Switching Table（ILM, incoming label map）**
    *   維護 incoming label 到 outgoing interface 和 outgoing label 之間的mapping。
    *   incoming label 指向的條目稱為下一跳標籤轉發條目 (NHLFE, Next Hop label-forwarding entry)。
*   **FEC 到 NHLFE 映射 (FTN, FEC-to-NHLFE map)**
    *   將每個 FEC 映射到一組 NHLFE。
    *   在轉發未標記數據包時使用。
    *   這些未標記的數據包在轉發之前必須被標記。
*   **標籤交換 (Label Swapping)**
    *   LSR 檢 packet 的Label。
    *   使用 label 作為 index 來獲取 NHLFE。
    *   使用此 NHLFE 中的信息，替換數據包的標籤並確定下一跳。
*   **標籤分配和分發 (label assignment and distribution)**
    *   下游標籤分發的兩種不同模式：
        *   按需下游模式(downstream-on-demand-mode)：LSR 明確向其鄰居請求特定 FEC 的標籤綁定。➝ LSR 只有在需要時才會從其鄰居學習標籤信息。
            *   按需下游模式的優點是：
                *   降低了標籤交換的開銷，因為 LSRR 只會從其鄰居學習它們需要的標籤信息。
                *   提高了標籤交換的靈活性，因為 LSRR 可以根據需要動態地請求標籤信息。
            *   按需下游模式的缺點是：
                *   可能會增加數據包的轉發延遲，因為 LSRR 需要等待其鄰居響應標籤請求。
        *   非請求下游模式(Unsolicited downstream mode)：LSR 會主動向其鄰居分發標籤綁定，即使這些鄰居並未明確請求它們。➝ LSR 會定期向其鄰居發送標籤信息更新。
            *   非請求下游模式的優點是：
                *   可以減少數據包的轉發延遲，因為 LSRR 不需要等待其鄰居響應標籤請求。
                *   可以提高標籤交換的效率，因為 LSRR 可以一次性向其所有鄰居分發標籤信息。
            *   非請求下游模式的缺點是：
                *   可能會增加標籤交換的開銷，因為 LSRR 需要定期向其鄰居發送標籤信息更新。
            *   
*   **標籤合併（相同 FEC）**
    *   兩個或多個 LSP 合併為一個。
    *   例如，對於来自 LSP 2 和 LSP 3 的所有Packet，LSR B 都可以對 LSR B 和 LSR D 之間使用相同的標籤。
    *   如果 LSR 已將多個入站標籤(incoming label)綁定到特定 FEC，則該 LSR 可能對 all packets 有一個出站標籤(outgoing label)。
    *   請注意，一旦packet使用相同的出站標籤(outgoing label)轉發，它們來自不同接口和/或具有不同入站標籤的信息將會丟失。
    *   標籤合併減少了對標籤空間的需求。![](https://t3764800.p.clickup-attachments.com/t3764800/9d93dd6d-3b63-4bca-88b6-49c6c78ae7b9/Screen%20Shot%202023-10-29%20at%204.58.01%20PM.png)

## Hierarchical Label Stack

![](https://t3764800.p.clickup-attachments.com/t3764800/17585aae-ad63-4010-b47f-ce72b8a80830/Screen%20Shot%202023-10-29%20at%205.23.15%20PM.png)

*   **分層標籤棧 (Hierarchical Label Stack)**
    *   將多個標籤編碼到一個數據包中以形成標籤棧
    *   用於構建嵌套 LSP，類似於 IP-in-IP 隧道
    *   操作：後進先出

![](https://t3764800.p.clickup-attachments.com/t3764800/8325d0a7-ebd5-4a96-8846-6a9008f905b6/Screen%20Shot%202023-10-29%20at%208.22.37%20PM.png)

*   **倒數第二跳標籤彈出 (Penultimate hop popping)**
    *   允許出口進行單次查找
    *   egress 根據 network layer destination address 轉發 packet
    *   當進行**Penultimate hop**時，LSP 出口甚至不需要是 LSR
    *   倒數第二跳標籤彈出是一種標籤交換技術，它允許在最後一跳路由器之前移除標籤棧中的最後一個標籤。這可以提高數據包轉發的效率，因為最後一跳路由器不需要進行標籤交換。
*   **兩種交換堆棧標籤的對等機制 (peering for exchanging stack label)**
    *   明確：在遠程 LDP 對等體之間建立 LDP 連接。這允許 LSR 在建立 LSP 時交換堆棧標籤。
    *   隱含：
        *   當在隱含對等 LSR 之間建立較低級別的 LSP 時，Stack Label 會附加（piggybacked）到 LDP 消息中。這允許 LSR 在不建立 LDP 連接的情況下交換 Stack label。
        *   較低級別 LSP 的中間 LDP 對等體將 **stack label** 作為較低級別標籤的屬性進行傳播

![](https://t3764800.p.clickup-attachments.com/t3764800/f981f479-909b-41cd-b2b4-70112f561944/Screen%20Shot%202023-10-29%20at%208.43.35%20PM.png)

*   **路徑選擇和顯式路由**
    *   跳轉路由 (Hop-by-hop routing) ➝ 不指定路徑
        *   依靠 IP 路由信息(routing information)來建立 LSP
        *   每一跳的控制模塊(control module)調用(call)路由模塊(routing module)來獲取下一跳(next hop)
    *   顯式路由 (Explicit routing) ➝ 指定static路徑
        *   MPLS 中最重要的功能之一
        *   LSP 的 ingress 或 egress 指定了整個路由
        *   通常，路由被確定為實現某些預先指定的目標（基於約束的路由, constraint-based routing）
        *   兩種類型的 explicit routing
            *   嚴格顯式路由 (Strictly explicit routing)：指定 LSP 的整個路由
            *   鬆散顯式路由 (Loosely explicitly routing)：只指定 LSP 路由的一部分

![](https://t3764800.p.clickup-attachments.com/t3764800/1682cb72-091a-4d36-b1ac-433844334518/Screen%20Shot%202023-10-29%20at%208.50.04%20PM.png)

*   **缺少出站標籤 (Lack of Outgoing label)**
    *   常規轉發 (Conventional Forwarding)
    *   丟棄數據包(Discard)（首選）
    > 如果路由器沒有出站標籤，則可以選擇使用常規轉發或丟棄數據包。常規轉發將使用 IP 路由信息來轉發數據包，但會降低數據包轉發的效率。丟棄數據包是最簡單的解決方案，但會導致數據丟失。
*   **缺少入站標籤 (lack of incoming label)**
*   攜帶標籤 (carry label)
    *   鏈路層標頭 (Link-layer header)
        *   例如，ATM、Frame Relay
    *   填充標頭 (shim label header)
        *   位於鏈路層L2和網絡層L3之間
        *   例如，Ethernet、token ring、PPP 等
        > 如果路由器收到一個沒有入站標籤的數據包，則可以使用攜帶標籤來解決此問題。攜帶標籤是一種將標籤添加到數據包鏈路層標頭或填充標頭的方法。攜帶標籤可以提高數據包轉發的效率，但會增加數據包的大小。

![](https://t3764800.p.clickup-attachments.com/t3764800/90381d6d-12c7-4a76-8d80-2c31a0980313/Screen%20Shot%202023-10-29%20at%204.16.49%20PM.png)

An MPLS packet has a 4-byte MPLS header: a 20-bit label field, a 3-bit experimental (EXP) field, a bottom-of-the-stack flag, and an 8-bit time to live (TTL) field, as shown in Figure 6.23(a). The TTL is an indicator of how long the packet has been in the network; when it expires, the packet is discarded. This helps to remove packets that are being misrouted and are lingering in the network. A possible application of the 3-bit experimental field is to implement quality of service, as discussed in Section 6.6.2

![](https://t3764800.p.clickup-attachments.com/t3764800/d52c5993-2f9f-4e26-98f1-65395b9b5b57/Screen%20Shot%202023-10-29%20at%209.58.54%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/3932c48e-31e8-4fa4-ba5b-6b555e02ed9a/Screen%20Shot%202023-10-29%20at%2010.05.21%20PM.png)

**環路檢測（loop detection）**

*   生存時間 (TTL) 是一種抑制(suppress) loop 的方法
*   處理 TTL 的兩種方法
    *   “shim” label header (L3)
        *   TTL 值 = L3 header中的 TTL 值
        *   在每個 LSR 跳轉時遞減
        *   當數據包從其 LSP 中出來時，將其複製到網絡層標頭的 TTL 字段
    *   Link-layer header (L2)
        *   非 TTL LSP 段（L2 交換機且沒有 TTL 字段）
        *   在將數據包轉發到非 TTL LSP 段之前，入口會遞減 TTL 值
        > 一個數據包從路由器 A 發送到路由器 D。該數據包的 TTL 值為 10。路由器 A 在轉發數據包之前將 TTL 值遞減為 9。路由器 B 和 C 在轉發數據包時也將 TTL 值遞減。當數據包到達路由器 D 時，其 TTL 值為 7。路由器 D 將數據包轉發給路由器 E。由於路由器 E 是一個 L2 交換機，並且不包含 TTL 字段，因此路由器 D 在轉發數據包之前將 TTL 值遞減為 6。
        >
        > 如果數據包在路由器 E 之後遇到了環路，則數據包的 TTL 值將減為零。路由器 E 將丟棄數據包並發送 ICMP 錯誤消息以通知路由器 A。

**在 ATM 標籤上轉發 MPLS 數據包的情況下的環路檢測（ATM 標頭中沒有 TTL 字段）**

*   **使用路徑向量 (path vector)**：如果沒有 TTL，則將路徑向量（LSR ID）放入標籤分發消息中。如果出現兩次，則表示存在 loop。
    *   path vector 是 label distribution message 中的一個字段。
    *   path vector 包含消息已通過的 LSR 列表。
    *   當 LSR 傳播包含路徑向量的消息時，它會將其 LSR ID 添加到列表中。
    *   LSR 通過接收包含其 LSR ID 的 path vector 的消息來檢測環路。
*   **跳轉計數器(HoP count)**：跳轉計數器用於記錄消息已通過的 LSR 數量。
    *   傳播消息時，LSR 會增加計數。
    *   當此計數達到配置的最大值時，LSR 會考慮 LSP 存在 loop。

# Label Distribution Protocols (**標籤分佈協議**)

![](https://t3764800.p.clickup-attachments.com/t3764800/3ebaf574-10c1-4cc8-aab2-0c8a964405d0/Screen%20Shot%202023-10-29%20at%2010.13.47%20PM.png)

*   **標籤分佈協議 (LDP, Label Distribution Protocols)**
    *   由 IETF MPLS 工作組提出，最初是唯一考慮的協議
    *   設計用於支持逐跳路由(hop-by-hop routing)
*   使用 LDP 進行基於約束的 LSP 設置 (Constraint-based LSP setup using LDP)
    *   設計用於支持顯式路由(explicit routing)
    *   向 LDP 添加了一組擴展以支持顯式路由 (explicit routing)
    *   稱為 CR-LDP（約束路由標籤分佈協議）
*   擴展 RSVP 以支持 LSP 隧道 (Extensions to RSVP for LSP tunnels)
    *   設計用於支持顯式路由 (explicit routing)
    *   擴展 RSVP 協議以執行 label distribution
    *   稱為 RSVP-TE（帶有流量工程擴展的 RSVP）



## LDP

![](https://t3764800.p.clickup-attachments.com/t3764800/8ab8c210-9530-4278-9d94-38c3e445249e/Screen%20Shot%202023-10-30%20at%2010.02.31%20AM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/6c48543f-4dcd-446a-bf33-8a12256f3d1e/Screen%20Shot%202023-10-30%20at%2010.01.51%20AM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/8bca6086-e67c-48fc-a5ec-bf25c2dd8ec4/Screen%20Shot%202023-10-30%20at%2010.02.07%20AM.png)

*   由於 LDP 支持hop-by-hop routing，因此使用 LDP exchange label /FEC mapping information的兩個 LSRs 稱為 LDP peers。
*   LDP peer exchange 4 categories of messages：
    *   **發現消息(Discovery messages)**：定期發送 Hello 消息來宣布和維護 LSR 在網絡中的存在
    *   **會話消息 (Session messages)**：在 LDP peer 之間建立(establish)、維護(maintain)或終止(terminate) message
    *   **通告消息 (Advertisement messages)**：為 FEC 創建(creating)、更改(changing)或刪除(deleting) label mapping
    *   **通知消息 (Notification message)**：分發警示信息(advisory info)和錯誤信息(error info)
*   **LDP 會話管理 (LDP session management)**
    *   兩個 LSR 通過 Hello 交換建立通信通道(communication table)和標籤空間(label space)
    *   然後遵循初始化過程(Initialization process)（Protocol version、label distribution method、time value 等）
    *   LSR 僅接受與其交換過 Hello 消息的 LSR 發送的初始化消息(initialization messages)
    *   Peer 和 Session 關係通過定期發送 Hello 和 Keep alive 消息來維護
    *   如果在收到新消息之前相應的 time expire，LSR 會認為 peer 或 session 已停止
*   **標籤分佈和管理 (Label distribution and management)**
    *   LDP 支持 downstream on demand 和 downstream unsolicited label distribution
    *   兩種方法都可用於同一網絡中，而對於任何給定的 LDP session，只能使用一種方法
    *   路徑上的 LSR 之間的 LSP 設置是獨立的
        *   任何 LSR 都可以隨時根據自己的需要向其鄰居通告(advertise) label mapping
        *   在收到 downstream label之前通告upstream label是可能的
    *   從出口(egress)到入口(ingress)順序設置 LSP
        *   LSR 只能發送 FEC 的 label mapping ，如果它有該 FEC 的 next hop 的標籤映射，或者該 LSR 是 出口
        *   否則，LSR 必須等到收到來自下游 LSR 的標籤，然後才能將相應的標籤傳遞給上游 LSR

## CR-LDP

![](https://t3764800.p.clickup-attachments.com/t3764800/2a9fdcf2-aae3-46d2-99cc-5648ded38ffa/Screen%20Shot%202023-10-30%20at%2010.36.42%20AM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/94ca872b-808d-4ebf-a556-62957418ac97/Screen%20Shot%202023-10-30%20at%2010.36.52%20AM.png)

*   CR-LDP 是基於 LDP 規範的，並帶有一組用於承載 explicit route 和 resource reservation 的擴展。
*   它支持 strict 和 loose 兩種 explicit route。
*   explicit route 在標籤請求消息中(Label request message)表示為沿 explicit route 的 node 或 list of node。
*   LSP 建立的步驟如下：

![](https://t3764800.p.clickup-attachments.com/t3764800/7a508a3c-91ec-4095-a52f-8d89a19e0390/Screen%20Shot%202023-10-30%20at%2010.43.02%20AM.png)

*   資源預留(reservation) 和 類別(class)
    *   CR-LDP 允許為explicit routes 預留資源。
    *   類型提供
        *   基於參數的規範 (Parameter-based specifications )（例如，peak rate 和 committed rate）
        *   基於協商的 (Negotiate-based)（如果 LSR 不能滿足現有資源，它可以為參數指定更小的值）
        *   基於類別的 (Class-based)（網絡資源被分類到resource class中）
*   路徑搶占(path preemption)和優先級(priority)
    *   每個 LSP 有兩個參數：設置優先級(priority)和保持優先級(holding priority)
    *   設置 priority 反映了添加新 LSP 的 priority
    *   保持 priority 反映了保留現有 LSP 的 priority
    *   如果新 LSP 的設置 priority 高於現有 LSP 的保持 priority，則新 LSP 可以搶占現有 LSP
    *   優先級的值範圍：0（最高）~ 7（最低）



## RSVP-TE

![](https://t3764800.p.clickup-attachments.com/t3764800/b51ef5c4-721c-4201-8677-54f9627a0dac/Screen%20Shot%202023-10-30%20at%2010.48.50%20AM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/aeb2c731-aad1-48d0-9406-a2f52888b313/Screen%20Shot%202023-10-30%20at%2010.48.59%20AM.png)

*   RSVP-TE 擴展了原始的 RSVP 協議以執行標籤分佈並支持顯式路由。
*   RSVP-TE 中的 LSP 稱為 LSP tunnel。
*   顯式路徑設置的步驟如下：
    *   將 explicit route 添加到 PATH message 中
    *   label request 通過 PATH message 發送，label binding 通過 RESV 消息發送
*   預留樣式：
    *   僅支持 FF 和 SE 預留樣式
    *   FF 為每個 LSP 創建一個獨立的預留
    *   SE 對於僅在相應的活動 LSP 失敗時使用的 backup LSP 很有用
*   Rerouting LSP tunnel ：
    *   目標：優化網絡中的資源利用率(resource utilization)或在網絡故障後恢復連通性
    *   使用的技術是“make-before-break”
        *   首先(1)建立替換 LSP tunnel ，然後(2)切換流量，最後(3)拆除舊 LSP 隧道
        *   在過渡期間，舊的和新的 LSP 隧道可能會共存，因此會爭奪它們共有的資源
        *   “make-before-break”可能會導致競賽條件，其中新 LSP 隧道無法建立，因為舊 LSP 隧道尚未釋放資源，但舊隧道在新的隧道建立之前無法釋放資源
        *   這個問題通過使用 SE 預留樣式來解決：舊的和新的 LSP 在它們共有的鏈路上共享資源
