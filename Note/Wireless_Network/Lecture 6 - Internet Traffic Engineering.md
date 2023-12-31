---
title: "Wireless-Multimedia-Network"
permalink: /Wireless-Multimedia-Network/6-Internet-Traffic-Engineering/
layout: default
---
# Lecture 6 - Internet Traffic Engineering

# **Introduction of Traffic Engineering**

*   Traffic engineering is concerned with the performance optimization of operational networks
*   The objective of traffic engineering is to reduce congestion hot spots and improve resource utilization across the network through carefully managing the traffic distribution inside a network
    *   修飾資料流的路徑，減少網路擁塞

# **Fish Problem**

*   Extremely unbalanced traffic distribution: all traffics from A and B to G go over one of the two paths
*   Reasons
    *   Destination-based IP routing: all packets to the same prefix address have the same next hop （到同一個destination 的packet都會走同一條路 ➝ 造成流量不均）
    *   Local optimization-based decision making in current routing protocols
    *   From the viewpoint of service providers, traffic split is preferred
        *   ATM VCs with IP routing on top of VCs
        *   Traffic distribution is managed by carefully mapping VCs to the physical network topology

![](https://t3764800.p.clickup-attachments.com/t3764800/1074d063-5aa6-45fa-bb96-4cff49066da9/image.png)

# **Solutions of Traffic Engineering**

*   Overlay model
    *   Allowing service providers to build arbitrary virtual topologies over the network’s physical topology （用LSP做tunnel）
    *   Usually build a full mesh of logical connections between all edge nodes
        *   Collecting the info of network topology and traffic demands (蒐集所有拓僕)
            *   讓service provider 提供網路架構，
            *   我們可以建任何logical topology over physical topology
        *   Calculating a set of optimal routes with constraint-based routing （Offline or on line）
        *   These logical connections are setup as MPLS explicit routes
    *   Cooperate with BGP routers
        *   Dotted line:logical connection （A --➝ B）
        *   Solid line: physical connection (A ➝ G ➝ B)
        *   A, B, C, D, E: BGP edge routers
        *   The difference of with and without overlay model
        *   LSPs（規劃好建LSP） vs. IGP-based approach（自己去找一條，只要目的地一樣，IGP intra gateway，小的domain按照最短路徑的方法去找路徑）
    *   (+) Flexibility
    *   (-) Scalability(N-squareproblem) (node的平方最後要最佳話會很難)
    *   (-) Breakdown of a single physical trunk may cause multiple LSPs to fail （有個link斷掉可能造成多個LSP 隧道路由壞掉，因為LSP只看隧道）
    > There are 4 paths from A to C (mesh):
    >
    > A➝G➝H➝C;
    >
    > A➝F➝H➝C;
    >
    > A➝G➝F➝H➝C;
    >
    > A➝F➝G➝H➝C
    >
    > With overlaying, any of 4 paths can be used, and is decided based on traffic between other BGP nodes
    >
    > Without overlaying, path from A to C is determined by an IGP such as OSPF
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/adb067d8-c1d6-45aa-b6fe-67f29d6df659/image.png)
*   Peer model
    *   Achieving balanced traffic distribution by manipulating link weights in OSPF routing protocol ➝ equal sum weight，改變他的weight來讓cost一樣，but loading很多就很難找
    *   Much more scalable than overlay model



# **Optimization Objectives**

*   The objectives could be:
    *   Minimization of congestion and packet loss – Improvement of link utilization
    *   Minimization of experienced delay
    *   Increase of served customers
*   Factors of congestion
    *   Inadequate network resources （網路資源不夠 如頻寬）
    *   Unbalanced traffic distribution （只走捷徑）
        *   The problem can be formulated to “minimize the maximum of link utilization in a network”
    *   Interesting observation: relationship between link utilization and queueing delay
        *   The maximum of link utilization is minimized, the total delay the packets experience is also minimized （讓utilization 的最大值是所有可能性的最小值（最佳化），packet delay 就會最小）
*   Assume all links have the same capacity
*   Node A can split traffic from itself to node C
*   What’s the optimal allocation among the 2 paths?
    *   Queueing delay increases more rapidly as the utilization increases (delay比utilization增加的還快，搬百分之1%可能會造成5%的delay)
    *   The increase of the delay on path A➝D➝C is always larger than
    the decrease of the delay on path A➝B➝C
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/c8ee1bb4-0896-4ee7-be86-974cd1c5ff34/image.png)



# Building Blocks of Internet TE

*   Data repository: a central database and persistent storage for all shared data objects (e.g., network topology, link state, and traffic demand)
    *   每個router都會彼此蒐集其他Router的資訊
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/26fd333e-3291-46e5-bb73-41af6076e269/Screenshot_20231222_234911_Microsoft%20365%20(Office).jpg)



*   Topology and state discovery: monitor topology and link state changes
    *   Possible approaches
        *   Static information: network configuration（網路設定）
        *   Dynamic information: residual bandwidth, link utilization (SNMP & polling)
        *   Routing protocol extension (to broadcast link state periodically in OSPF)
*   Traffic demand estimation
    *   Service agreement between service providers and customers
    *   ISP跟用戶的agreement 看能用多少流量
    *   Traffic measurement
        *   Aggregated traffic statistics (ex., traffic load between any pair of ingress and egress nodes)
*   Route computation
    *   Calculated based on traffic demands
    *   Constraint-based routing (= QOS routing)
        *   Off-line mode （背景做）
            *   Route computation is performed for all routes periodically with current info （週期性根據現在的info重新算路徑）
            *   The network cuts over to the new routes during maintenance periods （算完切換到最佳路徑會造成斷線）
                *   (+) Yielding optimal results
                *   (-) Traffic flow disruption
                *   (-) Extra delays for adding new traffic demands
        *   On-line mode （前台做）
            *   Route computation is performed in an incremental fashion and only calculates for new demands （基於當下最佳化找路徑）
            *   (+) Minimizing rerouting of existing flows
            *   (-) Inefficient resource utilization
    *   Utilizing both modes at different time scales alternatively
*   Network interface
    *   Configuring network elements in the network accordingly （設定網路由器透過network interface）
    *   Two approaches
        *   Web-based user interface (usually vendor specific)
            *   (+) Highly flexible
            *   (-) Vender-specific
        *   Standard-based approach: SNMP/Common open policy server protocol (COPS)
            *   COPS: proposed as a standard for a traffic-engineering system to instruct an edge node to set up MPLS explicit routes （RFC規範，承接指令並傳送到路由器）

# Constraint-Based Routing

*   Consist of two basic elements
    *   Route optimization: selecting routes for traffic demands subject to a given set of constraints
    *   Route placement: implement the selected routes in the network so that the traffic flows will follow them
*   Mathematical formulation
    *   Assumptions include
        *   Network links and capacities are directional (directed graph)
        *   Average traffic demand is known (either through measurement or through configuration parameters)
        *   Traffic demand is directional
    *   Objectives
        *   All traffic demands are fulfilled (所有traffic demand都能滿足)
        *   Minimizing the maximum of link utilization
    *   Notations
        *   ![](https://t3764800.p.clickup-attachments.com/t3764800/5d06c485-dfe2-4b2e-ac63-816c7a2afc25/Screenshot_20231223_072406_Microsoft%20365%20(Office).jpg)
            *   G: Graph; topoogy就是一張圖，裡面有link有連線，節點就是router，連線就是網路線Router 跟 Router之間沒線就不在 E 裡 （E是集合）
            *   V: 所有路由器成的集合
            *   E： Physical Link 所成的集合
        *   ![](https://t3764800.p.clickup-attachments.com/t3764800/7f6be486-907e-404a-b8cc-e5ec2b911811/Screenshot_20231223_072429_Microsoft%20365%20(Office).jpg)
            *   c: router i 到router j 這條link的頻寬
        *   ![](https://t3764800.p.clickup-attachments.com/t3764800/d49914be-ad2f-4417-9c1e-90d335ec1bee/Screenshot_20231223_072501_Chrome.jpg)
            *   K: 所有traffic demand的集合
            *   100個資料流就有100 traffic demand
            *   bw : k這個資料流需要多少的頻寬
            *   ![](https://t3764800.p.clickup-attachments.com/t3764800/55f3bbee-fa6a-4b2c-b86d-3d3b805b1e75/Screenshot_20231223_072556_Chrome.jpg)
            *   Note that demand may be split over multiple paths
        *   ![](https://t3764800.p.clickup-attachments.com/t3764800/f071062e-a897-4122-baf9-bc100d4dc843/Screenshot_20231223_072704_Chrome.jpg)
            *   X : 分配多少比例給多條path (80% + 20% = 1)
        *   ![](https://t3764800.p.clickup-attachments.com/t3764800/8c3cadd9-f049-4fff-8824-e1f3c1ee9ff8/Screenshot_20231223_072743_Chrome.jpg)
            *   所有link最大的Link utilization就是
            *   minimize maximun alpha
    *   Linear-programming formulation (LPF)
        *   Objective is to minimize the maximum of link utilization, i.e.,
        *   Constraints:
            *   The traffic flowing into a node must equal the traffic flowing out of the node for any node other than the source node and the destination node for each demand, i.e.,
                *   k這個資料流 j 不是頭 且j不是尾，多少進來就要多少出去 ➝ 中間節點 `i'` 不等於`i`
                *   進20%-出20%=0
                *   ![](https://t3764800.p.clickup-attachments.com/t3764800/caedcbe8-bedc-44e0-82e1-89cf5035e26c/Screenshot_20231223_081535_Microsoft%20365%20(Office).jpg)
            *   The net flow out of the source node is 1 (the assumed total required bandwidth), i.e
                *   分配進來的loading sum = 1
                *   i是起頭，j 是好幾分流加總起來等於1
                *   ![](https://t3764800.p.clickup-attachments.com/t3764800/edd8cd12-1a9c-4bd4-8846-1c0f268f6301/Screenshot_20231223_081628_Microsoft%20365%20(Office).jpg)
            *   The total bandwidth consumed by all logical connections on a link should not exceed the max utilization rate times the total capacity of the link, i.e.,
                *   logical connections on a link 不該大於alpha
                *   ![](https://t3764800.p.clickup-attachments.com/t3764800/6d7809b4-d9db-4ac7-8210-4036d93fbb4c/Screenshot_20231223_081727_Chrome.jpg)
            *   All variables are nonnegative real numbers and no more than 1, i.e.,
                *   ![](https://t3764800.p.clickup-attachments.com/t3764800/fadea395-2700-4833-b19c-627811bd58e8/Screenshot_20231223_081758_Microsoft%20365%20(Office).jpg)



*   Constraint-based routing in overlay model
    *   Shortest path (SP)
        *   When there is a demand, the shortest-path algorithm is used to set up an LSP to the destination
        *   Link metric for link (i,j) is inversely proportional to the bandwidth
        *   LSP, 最短路徑 頻寬反比 weight總和最小，如果直接把頻寬當權重加起來就不會選到大水管 （100 ➝ 1/100）
    *   Minimum hop (MH)
        *   Link metric is set to 1 uniformly for each hop
        *   Still run shortest path algorithm
    *   Shortest-widest path (SWP)
        *   Link metric is set to as bandwidth
        *   Always selecting the path with largest bottleneck bandwidth
        *   The one with minimum hops or shortest distance is chosen when multiple paths are available
        *   先選擇為寬，一樣寬再選擇最短
    *   Hybrid algorithm
        *   Concerning the basic tradeoff between avoiding bottleneck links and taking a longer path, and trying to balance the two objectives
        *   How? Assigning appropriate weights for them
        *   Weight: link utilization, instead of residual bandwidth
        *   Metric combines the cost of a path and the contribution to the maximum of link utilization
        *   Notation
            *   ![](https://t3764800.p.clickup-attachments.com/t3764800/d3fb7959-9e04-4fcc-b8ec-069570eee5eb/Screenshot_20231223_083738_Chrome.jpg)
                *   fi,j: 現在link（i,j）的loading
            *   ![](https://t3764800.p.clickup-attachments.com/t3764800/7e51f727-75a7-4a4e-a3d0-37c057d3cbde/Screenshot_20231223_083821_Chrome.jpg)
                *   ci,j: fi,j 加到最後的最大值
            *   ![](https://t3764800.p.clickup-attachments.com/t3764800/bd911af7-2e6b-4447-a64b-58568425d7e6/Screenshot_20231223_083842_Chrome.jpg)
            *   ![](https://t3764800.p.clickup-attachments.com/t3764800/7641e7b0-bbf6-4fbc-bc04-2d41f790f7df/Screenshot_20231223_083902_Chrome.jpg)
                *   alpha i,j : 就是 link(i, j)的utilization
                *   如果- alpha是負值就是0 ➝ T\*max\[0\] = 0
                *   如果- alpha是正值就是變排頭，會讓網路不均衡 T\*max\[0.2\] > 0
                *   T： 如果max\[\]變正，就用T讓他影響大一點，也就是不想發生這個狀況
*   Constraint-based routing in peer model
    *   The basic idea behind peer model is link cost adjustment
    *   Challenge: how to find a systematic approach of link weight assignment
    *   An example
        *   Traffic demands: (A➝B, 4), (A➝F, 4), (B➝F, 4), (A➝E, 4)
        *   Link utilization: 36/45=80%
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/8a464c12-a4e8-436e-84de-ff9350b8db56/Screenshot_20231223_085023_VLC.jpg)



# Multipath Load Sharing

*   Load-balancing system: distribute traffic equally or proportionally （分流最後按照sequence number組起來）
*   Basic requirements
    *   Traffic splitting is in the packet-forwarding path, and executed for every packet
    *   To reduce implementation complexity, the system should preferably keep no or little state info
    *   Traffic-splitting schemes produce stable traffic distribution across multiple outgoing links with minimum fluctuation
    *   Traffic-splitting algorithms must maintain per-flow packet ordering （重組）
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/27a0979c-f971-4afa-b537-4cdfeb7827f6/Screenshot_20231223_085322_Microsoft%20365%20(Office).jpg)
*   Packet-by-packet round robin
    *   (+) Low overheads
    *   (+) Good performance
    *   (-) Per-flow ordering (sequence numbers/states) （重組）
*   Hashing-based traffic-splitting schemes
    *   (+) Stateless
    *   (+) Easy to implement
    *   (+) Even traffic load distribution
*   Direct hashing
    *   Hashing of destination address
        *   ![](https://t3764800.p.clickup-attachments.com/t3764800/aece8153-402d-4661-893a-d357492be5e6/Screenshot_20231223_085627_Chrome.jpg)
        相同目的地走相同路徑
    *   Hashing using XOR folding of source/destination addresses
        *   ![](https://t3764800.p.clickup-attachments.com/t3764800/9a8239ce-af89-487b-b74b-1d59080413d6/Screenshot_20231223_085652_Microsoft%20365%20(Office).jpg)
        考慮source及 destination 來mod interface(路徑數量)
        source 跟 destination一樣就会走相同路徑
*   Table-based hashing
    *   Split a traffic stream into M bins.
    *   The M bins are mapped to N outgoing links based on an allocation table, i.e., compute the corresponding hash value
    *   By changing the allocation of the bins to the outgoing links, we can distribute traffic in a predefined ratio
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/8b40d393-c43d-4b98-b4c2-574449638154/Screenshot_20231223_085803_Chrome.jpg)
    *   表格式哈希（Table-based hashing）是一種負載平衡的算法，它使用一個哈希表來存儲伺服器或服務器的 IP 地址和負載平衡鍵。當有流量需要被負載平衡時，會使用負載平衡鍵來查找哈希表，然後將流量發送到對應的伺服器或服務器。
    *   表格式哈希的具體工作原理如下：
        1. 負載平衡器會在啟動時生成一個哈希表，哈希表中存儲了所有伺服器或服務器的 IP 地址和負載平衡鍵。
        2. 當有流量需要被負載平衡時，負載平衡器會使用負載平衡鍵來查找哈希表。
        3. 負載平衡器會將流量發送到哈希表中找到的伺服器或服務器。
    *   注意的是，哈希表的大小會隨著伺服器或服務器的數量增加而增加，可能會占用大量的記憶體
