---
title: "Wireless-Multimedia-Network"
permalink: /Wireless-Multimedia-Network/7-Multicasting/
layout: default
---
# Lecture 7 - Multicasting

# Internet Multicasting

*   Fundamental issues in multicast(**多播的基本問題**)
    *   Joining and leaving a group (**加入和離開群組**)
        *   Multicast sessions learning
            *   多播路由器如何了解多播會話的存在？
        *   Group members discovery
            *   多播路由器如何發現多播群組的成員？
        *   Dynamic group membership
            *   多播路由器如何處理群組成員資格的變化，例如成員加入或離開群組時？
    *   Efficient transmission of multicast traffic (有效率的多播傳輸)
        *   Resource optimization
            *   多播路由器如何在傳輸多播流量時優化網絡資源的利用，例如帶寬和緩衝空間？
        *   Delivery tree maintenance
            *   多播路由器如何維護一個交付樹，以便有效地將多播流量傳輸到群組的所有成員？
    *   Time-sensitive delivery of multicast traffic
        *   Data sequence maintenance
            *   多播路由器如何確保多播數據包按正確的順序傳輸到群組的所有成員
        *   Synchronization
            *   多播應用程序如何將其時鐘與多播流量源同步
    *   Guaranteed arrival of multicast traffic
        *   RTP(real-time transport protocol)
            *   RTP 是一種實時傳輸協議，可用於傳輸時間敏感的多播流量。
        *   RMP(reliable multicast protocols)
            *   RMP 是一種可靠的多播協議，可用於確保多播流量到達所有接收端。
    *   Scalability
        *   Feedback implosions
            *   當許多接收端同時向路由器發送反饋信息時，會導致反饋爆炸問題。
        *   The use of groups
            *   多播系統必須能夠支持不同類型的群組，以滿足不同應用的需求。
*   System
    *   Group membership protocol**(組播成員管理協議)**
        *   Inter Group Management Protocol (IGMP)
            *   一種用於在 IP 網路中管理組播成員的協議。
            *   它允許主機加入或退出組播組，並告知路由器哪些主機加入了哪些組播組。
    *   Multicast routing mechanism**(組播路由機制)**

> 用於在網路中傳遞組播數據包的路由機制。常見的組播路由機制包括 DVMRP、MOSPF、CBT、PIM-SM等。

*       *       *   Distance vector multicast routing protocol ([DVMRP](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4762?block=block-8cf32dda-dd0e-4bab-a797-88d688d02f2d), **距離向量組播路由協定**)
            *   一種基於距離向量路由演算法的組播路由協定。
            *   它使用 Reverse Path Forwarding (RPF) 技術來建立組播分發樹。
*       *       *   Multicast open shortest path first (MOSPF, **組播最短路徑優先協定**)
            *   一種基於開放最短路徑優先 (OSPF) 路由協定的組播路由協定。
            *   它使用 Link State Advertisement (LSA) 來建立組播分發樹。
*       *       *   Core-based tree (CBT, **核心樹協定**)
            *   一種基於核心的組播路由協定。
            *   它使用核心節點來建立組播分發樹。
*       *       *   Protocol independent multicast sparse mode (PIM-SM, **協議無關組播稀疏模式**)
            *   一種獨立於單播路由協定的組播路由協定。
            *   它使用 RPF 技術和 Rendezvous Point (RP) 來建立組播分發樹。

# IGMP

*   References
    *   \[RFC-1112\] "Host Extensions for IP Multicasting“
    *   \[RFC-2236\] "Internet Group Management Protocol, Version 2
    *   \[RFC-3376\] "Internet Group Management Protocol, Version 3
*   IGMP v1
    *   Multicast router: periodically sends a query message to the all-hosts address (224.0.0.1)
        *   **多播路由器定期查詢：** 多播路由器會定期向所有主機地址 (224.0.0.1) 發送查詢消息，以了解哪些主機加入了哪些組播組
    *   A host sends a report in reply on a per group basis, thereby refreshing the tentative states
        *   **主機回報組播組：**收到查詢消息後，主機會針對它所加入的每個組播組發送一個報告消息，以刷新路由器中的成員狀態
    *   IGMP v1 supports suppression for periodical refresh report messages
        *   **抑制定期刷新報告：** IGMP v1 支持抑制功能，可以避免主機重複發送定期刷新報告，降低網路流量。
    *   IGMP v1 hosts send unsolicited reports upon joining a group, but leaves the group silently
        *   **主動加入，靜默退出：** 主機在加入組播組時會主動發送報告，但在離開組播組時不會發送任何消息，而是靜默退出。
    > **IGMP v1 的侷限性：**
    >
    > **無法處理主機離開組播組的情況：** 由於主機在離開組播組時 不會發送消息，路由器可能會繼續向已經沒有成員的組播組發送組播數據包，造成資源浪費。
    >
    >   
    >
    > **不支援篩選器模式：** 路由器無法針對特定的源地址或源組播組進行成員查
    >
    >   
    >
    > **後續版本：**
    >
    > **IGMP v2：** 新增了離開組播組的功能，允許主機在離開組播組時發送離開消息。
    >
    > **IGMP v3：** 加入了篩選器模式，增強了組播管理的靈活性。
*   IGMP v2
    *   IGMP v2 maintains two types of query and three types of report
        *   Query
            *   General query
                *   路由器向所有主機地址發送一般查詢，以了解所有組播組的成員情況。
            *   Group-specific query
                *   路由器針對特定的組播組發送特定組查詢，以了解該組播組的具體成員情況。
        *   Report
            *   Join ➝ 主機在加入組播組時發送加入報告。
            *   Leave ➝ 主機在離開組播組時發送離開報告
            *   Refresh ➝ 主機定期發送刷新報告，以刷新路由器中的成員狀態。
    *   **_Periodical refresh report suppression_** is supported as well
        *   與 IGMP v1 相同，支持抑制功能來降低網路流量。
    *   The approach is to lower leave latency
        *   IGMP v2 引入了離開報告，可以更快地通知路由器主機已經離開組播組，從而降低離開延遲。
    > **IGMP v2 的優點：**
    >
    > 解決了 IGMP v1 無法處理主機離開組播組的問題。
    >
    > 降低了離開延遲，提高了組播管理的效率。
    >
    > **IGMP v2 的侷限性：**
    >
    > 仍然不支援篩選器模式，無法針對特定的源地址或源組播組
    >
    > 進行成員查詢。
    >
    > **後續版本：**
    >
    > **IGMP v3：** 加入了篩選器模式，增強了組播管理的靈活性。



*   IGMP v3

> **IGMP v3 是 IGMP v2 的進一步升級版本，它主要新增了源篩選（source filtering）功能，讓主機可以更精細地控制它所要接收的組播數據流量。**
>
> *   IGMP v3 maintains three types of query:
>     *   general query ( IGMP v2 )
>     *   group specific query( IGMP v2 )
>     *   group-and-source specific query
>         *   路由器針對特定的組播組和源地址發送查詢，以了解該組播組中是否有主機要接收來自該源地址的數據流量。
> *   IGMP v3 maintains four reports:
>     *   join ( IGMP v2 )
>     *   leave ( IGMP v2 )
>     *   state change
>         *   主機在其組播組成員狀態發生變化時發送狀態變更報告，例如加入新的組播組或離開現有的組播組。
>     *   refresh( IGMP v2 )
> *   **_No_** periodical refresh report suppression(壓制) is supported
>     *   與 IGMP v1 和 v2 不同，IGMP v3 不支持抑制定期刷新報告，以確保路由器能更準確地掌握組播組成員的最新狀態。
> *   The approach to support source filtering:
>     *   (group-id, filter mode, source list)
>     *   主機可以指定它要接收來自哪些源地址的組播數據包，或排除它不想接收的源地址。
>     *   主機在發送報告消息時，會附帶源篩選器（source filter），其中包含組播組 ID、篩選模式（include 或 exclude）以及源地址列表。
> *   General query
>     *   Multicast routers send General Queries periodically to request group membership information from an attached network （多播路由器定期向所連接的網路發送一般查詢，以請求網路上的主機報告它們所加入的組播組）
>     *   These queries are used to build and refresh the group membership state of systems on attached networks (路由器使用這些報告來建立和更新網路上主機的組播組成員狀態)
> *   Group-specific query
>     *   A Group-specific query is sent to verify there are no systems that desire reception of the specified group or to "rebuild" the desired reception state for a particular group. (路由器針對特定的組播組發送特定組查詢，以確認該組播組中是否還有成員，或重新建立該組播組的所需接收狀態)
>     *   Group-Specific Queries are sent when a router receives a State-Change record indicating a system is leaving a group (這通常是在路由器收到狀態變更報告（State-Change Record）時發送，表明有主機要離開該組播組)
> *   Group-and-source-specific query
>     *   Used to verify there are no systems on a network which desire to receive traffic from a set of sources (路由器針對特定的組播組和源地址發送查詢，以確認該組播組中是否有主機要接收來自該源地址的數據流量)
> *   Source filtering is the ability for an individual host to specify the reception of packets sent to a multicast group only from a list of source addresses or to explicitly identify a list of the sources the host does not want to receive from a multicast group
>     *   源篩選是 IGMP v3 新增的功能，允許主機指定它要接收來自哪些源地址的組播數據包，或排除它不想接收的源地址。
>     *   主機在發送報告消息時，會附帶源篩選器（source filter），其中包含組播組 ID、篩選模式（include 或 exclude）以及源地址列表。
>     *   Eg.
>         *   include{x, y, z}: 只接收來自源地址 x、y、z 的數據包
>         *   exclude{x}: 排除源地址 x 的數據包
>         *   exclude{}: 排除所有源地址的數據包（相當於不接收任何數據包）
>         *   include{}: 接收所有源地址的數據包（IGMP v1 和 v2 的默認行為）
>     *   IGMP v1/v2 → exclude{}
>
> > **IGMP v3 的優點：**
> >
> > 支持源篩選，增強了組播管理的靈活性和效率。
> >
> > 可以更精細地控制組播數據流量，降低網路負載。
> >
> > **IGMP v3 的侷限性：**
> >
> > 配置和管理相對複雜。
> >
> > 並非所有網路設備都支持 IGMP v3。



# Introduction-Routing

在網路中，路由是指將數據包從源端傳送到目的端的過程。路由器是用於在網路中傳送數據包的特殊設備，它們會根據路由表決定數據包的最佳傳送路徑。

*   Requirements of routing protocols
    *   Routing table space minimization
        *   **路由表空間最小化：** 路由器的記憶體空間有限，因此路由協議需要盡可能減少路由表的大小，以節省記憶體資源
    *   Control message minimization
        *   **控制消息最小化：** 路由器之間會交換控制消息以更新路由資訊，路由協議需要減少控制消息的數量，以降低網路流量
    *   Robustness
        *   **健壯性（Robustness）：** 路由協議要能夠應對網路中斷或故障，並快速找到替代路徑，以保持網路連通性
    *   Optimal path construction
        *   **最佳路徑構建：** 路由協議要能夠根據網路狀況選擇最佳的路徑，以提高數據傳輸的效率和可靠性
*   Two fundamental routing algorithms
    *   Distance-vector
        *   **距離向量（Distance-Vector）算法：** 每個路由器只知道鄰居路由器的距離資訊，通過與鄰居交換距離資訊來計算到目的地的距離
    *   Link-state （full mesh）
        *   **鏈路狀態（Link-State）算法：** 每個路由器都掌握整個網路的拓撲結構，通過計算所有可能路徑的成本來選擇最佳路徑
*   Scalability
    *   Exterior gateway protocol (EGP)
        *   Applied in the backbone (interconnecting multiple Autonomous Systems)
    > EGP 用於連接不同自治系統（Autonomous Systems，AS）的骨幹網，例如在 Internet 上連接不同 ISP 的網路。
    *   Interior gateway protocol (IGP)
        *   Applied in an autonomous system (AS)
        *   Routers in an AS are controlled by a single administrative authority
    > IGP 用於自治系統內部的路由，自治系統是指由單一管理機構控制的網路。
*   Routers exchange information to construct multicast delivery tree (**多播傳遞樹**)
    *   在多播傳送中，路由器之間會交換資訊以構建多播傳遞樹，以便將多播數據包高效地傳送到所有接收者。
*   Pruning(**修剪**)
    *   Due to dynamic membership
    *   Removing one branch from the delivery tree
    *   Important to tree maintenance
    *   由於多播組成員的動態變化，有時需要修剪多播傳遞樹，即移除不再需要的樹枝，以保持樹的效率和避免浪費網路資源
*   Dense mode（密集模式） vs. sparse mode multicast routing（**稀疏模式多播路由**）
    *   Definition: number of networks with group members
    *   Dense mode multicast routing: data-driven
        *   適用於組播成員分散在大多數網絡中的情況。它採用數據驅動的方式構建多播樹，即當源端發送數據時，路由器會將數據包傳送到所有網絡，然後在沒有組播成員的網絡上進行修剪
    *   Sparse mode multicast routing: receiver-initiated
        *   適用於組播成員集中在少數網絡中的情況。它採用接收方啟動的方式構建多播樹，即只有當接收者表明要加入組播組時，路由器才會建立到該接收者的路徑
*   Categories
    *   Multicast tree constructed
        *   Shortest path tree
            *   最短路徑樹（Shortest Path Tree）：以最短路徑為基礎構建多播樹
        *   Constrained tree (for QoS purpose)
            *   約束樹（Constrained Tree）：考慮 QoS 需求，在滿足 QoS 條件的情況下構建多播樹
    *   Multicast tree rooted
        *   Source-based
            *   A tree rooted as a source node is constructed and connected to every member in the multicast group
            *   E.g., DVMRP, MOSPF, PIM-DM

> 為根節點構建多播樹，連接到組播組中的所有成員。例如 DVMRP、MOSPF、PIM-DM 等協議

*       *       *   Centered-based (shared tree共享樹)
            *   One node for each group is selected as the core (or termed a rendezvous point, RP) for the group. A tree rooted at the core is then constructed to span all the group members
            *   E.g., CBT and PIM-SM

> 個節點作為所有組播組的核心（或稱為集合點，Rendezvous Point，RP），然後以核心為根節點構建多播樹，連接到所有組播組成員。例如 CBT、PIM-SM 等協議

# DVMRP

*   [Source-based](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4762?block=block-a585d79c-34fc-4c70-b12e-4f9ce169c25f) multicast delivery tree
    *   基於源的多播路由協議
*   Distance vector routing
    *   Bellman-Ford algorithm
        *   使用距離向量路由算法（Bellman-Ford 算法）來構建多播樹
    *   Multicast extension from DVRP (RIP)
        *   DVMRP 是基於 DVRP（Distance Vector Routing Protocol，距離向量路由協議，如 RIP）的多播擴展
    *   Based on RPM
        *   採用 RPM（Reverse Path Multicasting，反向路徑多播）技術
        *   For the first multicast packet: send over the tree anyway
            *   當源端發送第一個多播數據包時，路由器會將數據包傳送到所有網絡
        *   Send “ prune message” if none wanna receive packets
            *   如果沒有主機想要接收數據包，則會發送「修剪消息」來修剪多播樹
        *   Send “graft message” when a new group member joins in
            *   當有新的組播組成員加入時，會發送「嫁接消息」來擴展多播樹



*   DVMRP router functions
    *   The problem of redundant links
        *   **冗餘鏈路問題：** 在距離向量路由中，可能存在冗餘鏈路，即多條路徑通向相同的目的網絡。DVMRP 使用「主導路由器」和「從屬路由器」的概念來解決這個問題
    *   Dominant router
    *   Subordinate router
        *   對於每個源端，DVMRP 會選取一個路由器作為主導路由器，其他路由器則作為從屬路由器。主導路由器負責向源端傳送多播數據包，從屬路由器則不傳送數據包
    *   How to determine （**如何確定主導路由器**）?
        *   With less metric or lower IP address
            *   主導路由器通常是指到源端的距離（跳數）較小或 IP 地址較低的路由器
        *   Poison-reverse routing updates(**毒性反轉路由更新**)
            *   為了避免路由環路，DVMRP 使用毒性反轉路由更新。當從屬路由器向鄰居路由器發送路由更新時，它會將到達源端的距離設置為無窮大，以防止鄰居路由器將數據包傳回給它
    *   It’s possible that a different router may be the dominant router for each source(**不同的源端可能有不同的主導路由器**)

![](https://t3764800.p.clickup-attachments.com/t3764800/b14ffaa0-ab9c-45cc-9fd5-c9222d55805d/image.png)

*   When needed, will a subordinate router send a prune message to the dominate router?
    1. **觸發修剪消息的情況：**
        *   當從屬路由器發現其所有直連網絡中都沒有組播成員時，它會發送修剪消息。
        *   當從屬路由器收到來自所有直連網絡的修剪消息時，它也會發送修剪消息。
    2. **修剪消息的作用：**
        *   修剪消息用於告知主導路由器，該從屬路由器不再需要接收來自該源端的多播數據包。
        *   主導路由器收到修剪消息後，會更新其多播樹，將該從屬路由器從樹中移除，從而避免不必要的數據包傳送
*   Routing and forwarding
    *   Routing table: periodically exchange routing table update messages with multicast capable neighbors
        *   路由器會定期與鄰居路由器交換路由表更新消息，以保持路由表的最新狀態。
        *   路由表包含到達各個目的地的距離（跳數）和下一跳路由器的信息
    *   Forwarding table: multicast routing table + known groups + received prune messages
        *   轉發表是基於路由表、已知組播組和收到的修剪消息生成的。
        *   轉發表用於指導路由器如何轉發多播數據包
    > Ref. [http://www.cs.emory.edu/~cheung/Courses/558/Syllabus/14-Multicast/DVMRP.html](http://www.cs.emory.edu/~cheung/Courses/558/Syllabus/14-Multicast/DVMRP.html)
    >
    > [http://www.cs.emory.edu/~cheung/Courses/558/Syllabus/syl.html#CURRENT](http://www.cs.emory.edu/~cheung/Courses/558/Syllabus/syl.html#CURRENT)
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/9106f978-84e3-41ea-98c9-c4a7408e9a46/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/e837ce49-3912-40f8-8860-e4c1519ae4d9/image.png)



![](https://t3764800.p.clickup-attachments.com/t3764800/c0ff3e63-5b05-42b3-9ea3-1181e280b71d/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/23e630d6-17c3-41ca-bf58-195c39a49a71/image.png)







# MOSPF



*   Su[rce-based mu](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4762?block=block-a585d79c-34fc-4c70-b12e-4f9ce169c25f)lticast delivery tree
*   Link state routing
    *   Dijkstra algorithm
    *   Multicast extension to LSA (OSPF)
        *   Group-membership-LSA (link-state advertisement)
        *   它使用了組播成員 LSA（Group-Membership-LSA）來傳播組播成員的信息
    *   Trees are built on-demand to conserve CPU and memory resources

![](https://t3764800.p.clickup-attachments.com/t3764800/f18edc22-d973-4d2b-b870-0313a35fd25b/image.png)![](https://t3764800.p.clickup-attachments.com/t3764800/8f8f89d5-f125-4a4f-8c48-c42825a40660/image.png)

**MOSPF 的工作原理：**

1. **收集拓撲信息：** 路由器會定期相互交換鏈路狀態通告（LSA），以收集整個網路的拓撲信息。
2. **構建鏈路狀態數據庫（LSDB）：** 每個路由器都會基於收集到的 LSA 構建自己的 LSDB，其中包含網路中所有路由器和鏈路的狀態信息。
3. **生成組播成員 LSA：** 當某個網絡中有主機加入組播組時，該網絡的指定路由器（Designated Router，DR）會生成一個組播成員 LSA，並將其泛洪到整個網路。
4. **計算多播樹：** 當路由器收到組播數據包時，它會根據自己的 LSDB 和組播成員 LSA 計算出到達所有組播組成員的最短路徑樹，並將數據包轉發到這些成員所在的網絡。
5. **按需構建樹：** MOSPF 會根據需要動(on-demand)態構建多播樹，而不是預先構建所有可能的多播樹。這樣可以節省 CPU 和記憶體資源。

**MOSPF 的優點：**

*   可以快速適應組播組成員的變化。
*   可以根據網路拓撲的變化動態調整多播樹。
*   可以有效地利用網路資源。

**MOSPF 的缺點：**

*   需要所有路由器都支持 MOSPF。
*   需要所有路由器都維護 LSDB，這會增加路由器的負擔。
*   在大型網路中，LSA 泛洪可能會造成較大的開銷。



*   Basic operations
    *   MOSPF routers maintain a local group database (MOSPF 路由器維護本機群組資料庫)
    *   For a given multicast datagram, all routers within an OSPF area calculate the same sourcebased shortestpath delivery tree (對於給定的多播資料報，OSPF 區域內的所有路由器都會計算相同的基於來源的最短路徑傳遞樹)
    *   No need to flood the first multicast datagram to all routers in an area (無需將第一個多播資料封包洪氾到區域內的所有路由器)
    *   “On demand” construction spreads calculations over time (「按需」建設隨著時間的推移分散運算)



*   Protocol mechanisms
    *   Link state database
        *   每個路由器都會基於收集到的 LSA 構建自己的 LSDB，其中包含網路中所有路由器和鏈路的狀態信息。
    *   Local group database: labeling the serving MOSPF router
        *   Reduce the size of the link state database
        *   Streamlining the MOSPF routing calculation
        *   MOSPF 在 LSDB 中加入了「本地組播數據庫（Local Group Database）」，用於標記可以為特定組播組提供服務的 MOSPF 路由器。這可以減少 LSDB 的大小，並簡化 MOSPF 的路由計算。
    *   Forwarding cache
        *   (source, group)
        *   Upstream interface, downstream interface
        *   轉發表是基於 (源端, 組播組) 來存儲上游接口和下游接口的信息Only the routers that are parts of a particular tree maintain such info
        *   只有屬於特定多播樹的路由器才會維護轉發表This cache is not aged or periodically refreshed until
            *   Topology changes
            *   Group member has changed
            *   轉發表不會定期刷新，只有在拓撲變化或組播組成員變化時才會更新

![](https://t3764800.p.clickup-attachments.com/t3764800/f4878748-fef6-45a6-abb3-744073efc73e/image.png)

*   Protocol operation
    *   Joining a multicast group
        *   Host: IGMP → Designated router (DR) + backup DR
        *   DR主機發送 IGMP 報告消息到其所在網絡的指定路由器（DR）和備份 DR: group-membership-LSA → flooding
        *   DR 生成組播成員 LSA，並將其泛洪到整個網路other routers: update local group database, and may update forwarding cache
        *   其他路由器收到 LSA 後，會更新其本地組播數據庫，並可能更新轉發表
    *   Leaving the multicast group
        *   Host: IGMP → DR → LSA → update
            1. 主機發送 IGMP 離開消息到 DR
            2. DR 生成新的組播成員 LSA 來表示該主機已離開組播組，並泛洪 LSA 以更新其他路由器
    *   Inter-area multicast forwarder (**區域間多播轉發**): OSPF area border router (ABR)
        *   OSPF 的區域邊界路由器（ABR）充當區域間多播轉發器
    *   wild-card multicast receiver
        *   ABR 會使用通配符多播接收器（Wild-card Multicast Receiver）來接收来自所有源端的多播數據包
    *   Data forwarding
        *   Global topology (**構建全局拓撲**)
            *   Link state database + group membership LSA
                *   路由器根據 LSDB 和組播成員 LSA 構建全局拓撲視圖
        *   Shortest path tree computation
            *   Computation on demand
            *   Based on source network and destination multicast group
                *   最短路徑樹的計算是按需進行的，而不是預先計算所有可能的樹
                *   路由器根據計算出的最短路徑樹構建轉發表，用於指導數據包的轉發
        *   Forwarding cache construction

![](https://t3764800.p.clickup-attachments.com/t3764800/13f9709c-823f-4c55-a41b-29f0be846373/image.png)

# MOSPF – Complementary

*   Area v.s. AS
    *   In OSPF, a single autonomous system (AS) can be divided into smaller groups called areas（AS = area + area + area...）
    *   (+ ) Reduce the number of link-state advertisements (LSAs) and other OSPF overhead traffic sent on the network
        *   減少鏈路狀態通告（LSA）和其他 OSPF 開銷流量
    *   (+) Reduce the size of the topology database that each router must maintain
        *   減小每台路由器需要維護的LSB的大小
*   Area border router (ABR)
    *   Routing devices that belong to more than one area and connect one or more OSPF areas to the backbone area are called area border routers (ABRs)
        *   ABR 是指連接一個或多個 OSPF 區域到骨幹區域（Backbone Area）的路由器
    *   At least one interface is within the backbone while another interface is in another area
        *   ABR 至少有一個接口位於骨幹區域，而另一個接口位於其他區域
    *   ABRs also maintain a separate topological database for each area to which they are connected
        *   ABR 會為每個連接的區域維護一個單獨的拓撲數據庫，並負責在區域area間轉發路由信息
*   Autonomous system boundary router (ASBR)
    *   Routing devices that exchange routing information with routing devices in non-OSPF networks are called AS boundary routers
        *   ASBR 是指與非 OSPF 網路交換路由信息的路由器。
        *   ASBR 負責將 OSPF 網路中的路由信息導入到其他路由協議中，或將其他路由協議中的路由信息導入到 OSPF 網路中

![](https://t3764800.p.clickup-attachments.com/t3764800/5c70dd14-ef13-40c3-a742-b4b8573ca327/image.png)

*   Wild-card multicast receiver
    *   是 OSPF 和 MOSPF 中用於接收來自所有源端的多播數據包的特殊接口。ABR 和 ASBR 通常會使用Wild-card multicast receiver來接收來自外部 AS 或其他 area 的多播數據包
        *   **使用多播組播地址：** 通配符多播接收器可以使用多播組播地址來接收來自所有源端的多播數據包。例如，如果通配符多播接收器使用多播組播地址 `224.0.0.0/4`，則它將接收來自所有源端的多播數據包，這些數據包的組播組地址在 `224.0.0.0/4` 範圍內。
        *   **使用通配符接口：** 通配符多播接收器可以使用通配符接口來接收來自所有源端的多播數據包。例如，如果通配符多播接收器使用通配符接口 `*.0.0.0/0`，則它將接收來自所有源端的多播數據包，這些數據包的源地址在 `*.0.0.0/0` 範圍內。
*   Inter-area multicast forwarder
    *   指位於不同 OSPF area 之間的路由器。ABR 是Inter-area multicast forwarder的一種特殊類型。Inter-area multicast forwarder負責在不同 area 之間轉發多播數據包
        *   **使用通配符多播接收器：** 區域間多播轉發器可以使用通配符多播接收器來接收來自所有源端的多播數據包，然後將這些數據包轉發到其他區域。
        *   **使用組播成員 LSA：** 區域間多播轉發器可以使用組播成員 LSA 來獲取特定組播組的組播成員信息。然後，它可以根據組播成員信息來轉發多播數據包。



*   Inter-AS multicast forward
    *   指位於不同自治系統（AS）之間的路由器。ASBR 是 Inter-AS multicast forwarder的一種特殊類型。Inter-AS multicast forwarder負責在不同 AS 之間轉發多播數據包



*   One AS consists of several areas
*   Within an area, routers flood Group Membership-LSA

通常使用組播成員 LSA 來獲取特定組播組的組播成員信息。然後，它可以根據組播成員信息來轉發多播數據包

*   MOSPF is an extension to teh OSPF unicast routing protocol and hence requires OSPF as the underlying routing protocol. As such, it uses a new type of OSPF LSA called Group-Membership LSA to advertise teh existence of Group members on networks. These Group Membership LSAs are periodically flooded throughout an area in the same fashion as othe OSPF LSA's. It uses the Dijkstra algorithm to computer the shortest path tree for every source-network group pair.
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/5bd359e6-fc42-4abf-80f9-a6f3b3b00f08/image.png)
*   Routers within an area construct source-network trees for the multicast traffic forwarding
    *   Area 1 members Group A and B
    *   Area 2 members of Group A .
*   Routers with directly connected members originate Membership LSA's is announcing the existence of these members on their networks. These LSA's are flooded throughout the area. These Group Membership LSA's do not travel between Area 1 and Area 2（具有直接連接成員的路由器發起成員資格LSA，宣布這些成員在其網路上的存在。這些 LSA 被淹沒在整個地區。這些團體成員 LSA 不會在區域 1 和區域 2 之間行駛)
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/53d420a2-1086-4ea8-aed3-3b0efda861d8/image.png)
*   Inter-area traffic deliveries through MABRs (wildcard multicast receiver)
    *   (區域內的路由器建構來源網路樹以進行組播流量轉發)
    *   Once all routers within the area have learned where all the members are in teh network topology, it is possible to construct Source-network trees for the multicast traffic forwarding (一旦區域內的所有路由器都了解了所有成員在網路拓撲中的位置，就可以建立用於多播流量轉送的來源網路樹)
        *   In the above example, Source S1 in Area 1 begins sending multicast traffic to Group B (S1,B). As this data reaches the routers in the area, each runs a Dijkstra calculation and computes a shortest path tree rooted at the network for S1. This tree spans all members of Group B, and used for forward all multicast traffic for said group.
        *   In area 2, Source 2 S2, begins sending multicast traffic to Group A. Again the routers in the area use the Group Membership information in their MOSPF database to run calculations to find the SPT for the source network where S2 resides. The traffic is then forwarded to (S2,A) as shown.
        *   However, the routers in Area 2 are not aware of the member of Group A in Area 1 as Membership LSA's are not flooded between these two areas. This Inter-Area traffic is handled by another mechanism.

## wildcard multicast receiver

*   In order to transfer multicast traffic between Areas, the concept of 'Wildcard Receivers' is used by MOSPF Area Border Routers (MABR). Wildcard receivers set the 'Wildcard Receiver' Flag in the Router LSA's that they inject into the Area. This flag is equivalent to a whildcard Group Membership LSA that effectively says, I have a directly connected member for every group
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/25ce7f16-ad59-4374-a8aa-4c07925fbee9/image.png)
*   Multicast data delivered to MABRs
*   These MABRs connect Areas to the backbone area (Area 0), always set the wildcard receiver flag in their Router LSA's that they are injecting into a non-backbone area. This causes the MABR to be always be added as a branch of hte Shortest Path Tree of any active source in the non-backbone area.(這些 MABR 將區域連接到骨幹區域（區域 0），始終在它們注入非骨幹區域的路由器 LSA 中設定通配符接收器標誌。這導致MABR總是被添加為非骨幹區域中任何活動源的最短路徑樹的分支。)
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/c88161bc-c87f-49dc-b915-bc222cbdc9b3/image.png)
*   Area’s summary group membership LSA
*   Routers in backbone area (area 0) calculate the shortest path accordingly
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/27d4e68b-08b6-4139-8c6a-23ad75fa3451/image.png)
    *   In the example this results in MABR1 being added to the SPT for (S1,B) traffic and MABR2 added to that for (S2,A). This pulls the source traffic in the area to the border router so that it can be sent into the backbone area.(在範例中，這會導致 MABR1 加到 (S1,B) 流量的 SPT，而 MABR2 則會加到 (S2,A) 流量的 SPT。這會將區域中的來源流量拉至邊界路由器，以便將其傳送到骨幹區域。)
    *   In addition, there is also definition for a new Summary Membership LSA that is used to summarize an area's group membership information. These are inhected into the backbone area, Area 0 so that routers in the backbone area are made aware of the existence of members in other areas.(此外，還定義了一個新的Summary Membership LSA，用於總結區域的組成員資訊。這些被感染到骨幹區域 Area 0，以便骨幹區域的路由器知道其他區域中成員的存在。)
    *   the existence of members of group A and B in area 1 is being injected into the backbone area by MABR1 via Summary Membership LSA. In addition, MABR2 is injecting a Summary Membership LSA into the backbone area that indicates that Area 2 has members of Group A. Routers int he backbone area now use the information in these Summary Membership LSA's in their Dijkstra calculations to know which MABR's to include in the backbone SPT for which sources. (區域 1 中 A 組和 B 組成員的存在正由 MABR1 透過匯總成員 LSA 注入骨幹區域。此外，MABR2 正在將摘要成員 LSA 注入骨幹區域，表明區域 2 具有群組 A 的成員。骨幹區域中的路由器現在在其 Dijkstra 計算中使用這些摘要成員 LSA 中的信息來了解要包含在哪些 MABR 中其來源的主幹SPT。)ter-area multicast forwarder
*   Inter-area multicast data delivery
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/a2040f5b-b555-47be-bd67-50ebe4473a0d/image.png)
    *   (S2,A) traffic is now flowing from Area 2 into the backbone area (Area 0) via MABR2. The routers in the backbone are forwarding this traffic to MABR1 who is sending the traffic into Area 1. Routers inside of Area 1 run the Dijkstra calculation on (S2,A) traffic to construct a (S2,A) SPT inside of Area 1 to route the traffic to members of Group A as shown ((S2,A) 流量現在透過 MABR2 從區域 2 流入骨幹區域（區域 0）。主幹網路中的路由器將此流量轉送到 MABR1，MABR1 將流量傳送到區域 1。區域 1 內部的路由器對 (S2,A) 流量運行 Dijkstra 計算，以在區域 1 內部建置 (S2,A) SPT將流量路由至A 組成員，如圖所示)
*   When there are no members for a multicast group, traffic is still pulled to the MABRs as a result of the Wildcard Receiver mechanism
*   This can result in unnecessary bandwidth consumption
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/f82c9e0d-63b4-4507-a717-bb112ee4c04e/image.png)

## Inter-AS multicast forwarder

*   Inter-AS multicast data delivery
    *   When traffic arrives from outside the domain via the Multicast AS Border Router (MASBR), this traffic is forwarded across the backbone to the MABRs as necessary based on the Summary Membership LSAs
    *   Inter-domain traffic flow is basically the same as that for inter-area traffic
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/10978af8-8beb-4ff1-afd6-41b0767701a1/image.png)
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/c144b2c4-7280-4e32-8b3a-f62cc6355a49/image.png)
*   Sill have the problem of unnecessary bandwidth waste
    *       *   ![](https://t3764800.p.clickup-attachments.com/t3764800/25c67f51-702e-4bcd-85ab-a6a81beb7350/image.png)
            *   This causes the multicast traffic for Group A and B arriving from outside the AS to be forwarded as shown above. The wildcard receiver mechanism to automatically pull all source traffic in the area to them is also present. This allows MASBR;s to forward traffic as needed to the outside world(這會導致從 AS 外部到達的群組 A 和 B 的多播流量被轉發，如上所示。還有自動將區域中的所有來源流量拉到它們的通配符接收器機制。這允許 MASBR;s 根據需要將流量轉發到外部世界)
            *   As such, there are significant scaling problems as the flooding of link-state/membership hinders performance and the recalculation of the Dijkstra algorithm is necessary on every single multicast source. Hence, MOSPF is not appropriate for networks with unstable links, too many simultaneous active source-network/group pairs (因此，存在嚴重的擴展問題，因為鏈路狀態/成員資格的氾濫會影響效能，並且需要在每個組播源上重新計算 Dijkstra 演算法。因此，MOSPF 不適用於鏈路不穩定、同時活動的來源網路/群組對過多的網絡)

> REF.[https://www.hep.ucl.ac.uk/~ytl/multi-cast/mospf\_01.htm](https://www.hep.ucl.ac.uk/~ytl/multi-cast/mospf_01.htm)



# CBT

*   Core Based Trees
*   Center-based multicasting
*   Design goals
    *   Scalability: S\*N vs. N
        *   CBT 旨在解決大型網路中的多播路由問題，它可以有效地支持大量的組播組和成
    *   Tree creation
        *   Receiver-based formation
            *   CBT 樹是基於接收者的需求而構建的，只有當有接收者加入組播組時，才會構建相應的樹枝。這可以節省網路資源
        *   Significant benefit to all routers on the SP non-receiver senders and the multicast tree
    *   Unicast routing separation
        *   **單播路由分離（Unicast Routing Separation）：** CBT 將多播路由與單播路由分離，這使得它可以與不同的單播路由協議一起使用。
*   Components
    *   Core
        *   Pimary Core (CBT 樹的根節點，負責接收來自所有組播組成員的加入請求，並構建多播樹)
        *   Secondary Core : 默認的核心
            *   在主核心失效時接管的核心
        *   Designated Router (DR)
            *   The same as IGMP querier for the subnet
            *   每個網絡中的一台路由器，負責收集該網絡中組播組成員的信息，並將加入請求轉發給核心
*   Function
    *   Every member of the group sends an explicit Join towards the primary core resulting in either creation of a branch ending in the primary core or ending in an existing branch of the tree (群組的每個成員向主核心發送明確連接，從而創建以主核心結束的分支或以樹的現有分支結束)
        1. **加入組播組：** 當主機加入組播組時，它會向 DR 發送 IGMP 加入消息。
        2. **DR 轉發加入請求：** DR 會將加入請求轉發給主核心。
        3. **核心構建樹枝：** 主核心會根據加入請求構建樹枝，並將樹枝延伸到組播組成員所在的網絡。
        *   **數據包轉發：** 當源端發送多播數據包時，數據包會沿著 CBT 樹轉發到所有組播組成員。
*   Weakness of CBT
    *   Core placement and shortest path(**核心位置和最短路徑問題**)
        *   核心的位置會影響 CBT 樹的效率，如果核心的位置不合適，可能會導致數據包走非最短路徑，增加延遲Longer latency compared to SPT
    *   Traffic concentration (**與最短路徑樹（SPT）相比延遲更長**)
        *   CBT 樹不一定是最短路徑樹，因此可能會導致更長的延遲
    *   Th e core as a point of failure(**流量集中**)
        *   所有多播流量都會經過核心，可能會導致核心成為瓶頸
*   Cores and core placement(**核心是單點故障**)
    *   如果核心失效，整個 CBT 樹就會癱瘓
    *   Core list
    *   Priority/ranking
        *   所有核心的列表，包含核心的優先級或排名。
        *   主核心是列表中優先級最高的核心。
        *   當主核心失效時，備用核心會接管。
    *   Explicit ordered list
    *   Primary core, secondary core, …
    *   Placement schemes
        *   Statically configured
            *   核心可以靜態配置，也可以動態選舉
        *   Any router can become a core when a host on one of its attached subnets wished to initiate a group
            *   在動態選舉模式下，任何路由器都可以成為核心，當其連接的網絡中有主機加入組播組時，它就會成為核心。
*   Protocol operations
    *   Tree creation
        *   Joining a primary core **加入主核心**
            *   Unicast Join-Request (with active bit=1) and Join-ACK hop-by-hop + create forwarding entry backwards
                *   DR 會發送單播 Join-Request 消息（帶有 active bit=1）給主核心
            *   “join pending” state
            *   “CBT-non-core” state
            *   In pending state and get a better path,…
            *   One parent link and multiple child links
        *   Joining a secondary core
            *   As joining a primary core but split to two parts:
                *   DR joins a secondary core → the secondary core joins a primary core → may hit an on-tree router before reaching the primary core(DR 加入備用核心➝備用核心加入主核心)
        *   Leave
            *   Conditions
                *   » No members for that group on any directly attached subnets
                *   » It has received a QUIT-REQUEST on each of its child interfaces for that group (當主機離開組播組或 DR 收到所有子接口的 Quit-Request 消息時，DR 會向其父節點發送單播 Quit-Request 消息)
            *   Operations
                *   » Unicast Quit-Request (to its parent router)
                    *   子接口的 Quit-Request 
                *   » Quit-Ack (reply by the parent router) hop-by-hop
                    *   (父節點會發送 Quit-Ack 消息回給 DR，並刪除轉發表項)
                *   » Delete forwarding entry
    *   Data forwarding
        *   Two phase routing
            *   Unicast routing to send multicast packets to a multicast tree, allowing multicast groups and multicast packets to remain invisible to routers on the tree(單播路由將多播數據包發送到多播樹)
            *   Once on the multicast tree, multicast data packets to all group members based on group id (一旦進入組播樹，根據組id向所有組成員組播資料包)
                *   » FIB (Forwarding Information Base)
    *   Core router discovery
        *   Bootstrap
            *   For intra-domain (**用於域內**)
            *   Some domain’s routers are configured to be CBT candidate core routers, and periodically advertises themselves to the domain’ s Bootstrap Router (BSR), using “Core Advertisement” messages
                *   **候選核心路由器：** 域內的部分路由器被配置為 CBT 候選核心路由器，它們會定期使用 Core Advertisement 消息向域的 Bootstrap Router（BSR）宣傳自己
            *   BSR is elected dynamically from all domain’s routers
                *   **BSR 選舉：** BSR 是從域內所有路由器中動態選舉出來的，負責收集 Core Advertisement 消息並構建候選核心集（CC-set）
            *   BSR collects these “Core Advertisement” messages and periodically advertises a candidate core set (CC-set) by hop-by-hop unicast forwarding, by using “Bootstrap Messages”
                *   **Bootstrap 消息：** BSR 會定期使用 Bootstrap Messages 通過單播轉發的方式向域內所有路由器宣傳 CC-set
        *   Manual configuration
            *   除了 Bootstrap 機制外，還可以手動配置核心路由器的 IP 地址。

![](https://t3764800.p.clickup-attachments.com/t3764800/bb9c05e9-6da2-434c-935b-ba4196c1f010/image.png)





# PIM

*   Protocol Independent Multicast
*   Function: DVMRP + CBT

# PIM-DM

*   Source-rooted tree
*   When a source starts sending, all downstream hosts want to receive multicast datagrams
*   Explicit prune message with a timer
*   Graft message
*   Similar to DVMRP

# PIM-SM

**PIM-SM（Protocol Independent Multicast - Sparse Mode，協議無關組播 - 稀疏模式**

*   Design goals
    *   Efficient sparse group support
        *   Sparse means
            *   The ratio of the number of networks/domains with members is significant smaller than the total number of networks/domains in a region（意味著組播組成員分佈在相對較少的網絡或域中）
            *   Group members are widely distributed
            *   Flooding and pruning overhead of non-member is significant high
                *   PIM-SM 專門針對稀疏組進行優化，避免在非成員網絡中泛洪數據包，節省網路資源
            *   Sparse-mode does not imply that the group has a few members
    *   High quality data distribution
        *   Supporting low-delay data distribution if needed （支持低延遲數據分佈）
        *   Avoiding imposing a single shared tree
            *   避免使用單一共享樹，而是為每個源端構建最短路徑樹（SPT），以降低延遲
            *   Multiple sources send data simultaneously
            *   Path lengths between sources and destinations in SPT’s are significantly shorter than in shared tree
    *   Unicast routing independence
        *   PIM-SM 可以與任何單播路由協議（例如 OSPF、IS-IS、BGP）一起使用。
    *   Robustness
        *       *   Soft state mechanism
                *   定期刷新路由信息，防止路由信息過期
            *   Avoiding a single point of failure
    *   Interoperability (**互操作性**)
        *   可以與其他組播路由協議互操作
*   Components
    *   Rendezvous Point (RP, **會合點**)
        *   所有組播源端和組播組成員都會在 RP 上會合，RP 負責構建共享樹（Shared Tree）並轉發多播數據包
    *   Designated Router (DR)
        *   每個網絡中的一台路由器，負責收集該網絡中組播組成員的信息，並將加入請求轉發給 RP
        *   Senders: PIM Register
            *   發送多播數據包的路由器
            *   Piggybacked
        *   Receivers: PIM Join-Request
            *   接收多播數據包的路由器
        *   PIM-Register-Stop
    *   BootStrap Router (BSR)
        *   負責在域內宣傳 RP 信息，讓所有路由器都能找到 RP
*   Creating the PIM framework
    *   An RP sends C-RP-Advs to BSR → BSR announces the RP-set using bootstrap message (BSM) to all routers → every router can uniquely identify the RP for the group
        1. RP 發送 C-RP-Advs 消息給 BSR
        2. BSR 使用 Bootstrap Message（BSM）向所有路由器宣傳 RP-set
        3. 每台路由器根據 BSM 找到對應組播組的 RP
*   Creating a RP-rooted PIM tree
    *   Receiver join
        *   當接收者加入組播組時，會發送 PIM Join-Request 消息給 DR，DR 會將加入請求轉發給 RP，RP 會構建 RP 根樹並將數據包轉發給接收者
    *   Source join (join request piggybacked in multicast data packet)
        *   當源端加入組播組時，會將加入請求（PIM Register）附加在多播數據包中發送給 RP，RP 會構建 RP 根樹並將數據包轉發給組播組成員
        *   If none potential receivers, the RP router simply drop received data packets or inform the source stopping transmissions
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/2b86a9be-fe44-4f19-8e60-d7827979c515/image.png)
*   Protocol operations
    *   Local host joining a group
        1. **本地主機加入組播組：** 本地主機向 DR 發送 IGMP 加入消息，DR 會將加入請求轉發給 RP
    *   Establishing the RP-rooted shared tree (a.k.a. RP tree, RPT)
        *   **建立 RP 根樹：** RP 會根據加入請求構建 RP 根樹，並將數據包轉發給組播組成員
    *   Switching from shared tree to SPT (shortest path tree)
        *   **切換到最短路徑樹（SPT）：** 如果源端和組播組成員之間存在更短的路徑，則可以切換到 SPT，以降低延遲
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/86bf33e9-c2e6-4788-bf1b-0f37e4a32c4e/image.png)



![](https://t3764800.p.clickup-attachments.com/t3764800/771abe17-e7c1-4b63-a249-d2b44ba23505/image.png)



# Comparison of DVMRP and CBT Router States

![](https://t3764800.p.clickup-attachments.com/t3764800/4a0a7f64-7ef9-449c-b06e-315d39566434/image.png)

## Problem Set 2

![](https://t3764800.p.clickup-attachments.com/t3764800/cfca6905-0af2-4b4d-900c-5b5ad9c1c41b/image.png)



## Problem Set 5

*   Considering the following network topology

Flow 1 is from A to E (path is A→B→D→E) ![](https://t3764800.p.clickup-attachments.com/t3764800/7b7bd8c7-6b4b-4c4a-bb52-020d54e4becf/image.png)

*       *   Flow 2 is from A to F (path is A→B→D→F)![](https://t3764800.p.clickup-attachments.com/t3764800/4fdff87b-4a2d-412a-8323-af7f17f0c558/image.png)
    *   Flow 3 is from G to B (path is G→E→D→B)![](https://t3764800.p.clickup-attachments.com/t3764800/0baab43e-1467-4e31-af03-49596aabe9cd/image.png)
    *   Flow 4 is from G to C (path is G→E→D→C) ![](https://t3764800.p.clickup-attachments.com/t3764800/91467343-4ef5-4cd3-81d2-96b0c8b17fbd/image.png)
*   Q1: What are the rate allocations for these flows, respectively, when utilizing max-min resource allocation?
    *   Flow 1: 0.5
    *   Flow 2: 0.5
    *   Flow 3: 1
    *   Flow 4: 1
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/49b94af5-d930-40dd-9a9c-31f20bdac7c5/image.png)



*   Q2: We further assume that the rate demands of flows 1-4 are 1, 1, 2, and 2. How will you manage these flows through traffic engineering to achieve the least total delay?

\[hint: assign different routes to flows\]

*   The maximum of link utilization is minimized, the total delay the packets experience is also minimized
    *   Flow 1 is from A to E ![](https://t3764800.p.clickup-attachments.com/t3764800/156ce9c4-cc6d-4547-9137-9ca99ddda8be/image.png)
    *   Flow 2 is from A to F![](https://t3764800.p.clickup-attachments.com/t3764800/cbfe03ad-a9f6-4755-ad9a-1767ef9147b7/image.png)
    *   Flow 3 is from G to B![](https://t3764800.p.clickup-attachments.com/t3764800/670837f7-954a-45f8-8ac3-6373631c79bf/image.png)
    *   Flow 4 is from G to C![](https://t3764800.p.clickup-attachments.com/t3764800/62f95018-fdc3-483c-859e-bcc9a1a1b4df/image.png)

*   ![](https://t3764800.p.clickup-attachments.com/t3764800/a4b5c4a3-539d-46a8-8b07-515e0c8c1b37/image.png)
