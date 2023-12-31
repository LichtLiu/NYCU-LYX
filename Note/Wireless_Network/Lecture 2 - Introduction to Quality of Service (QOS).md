---
title: "Wireless-Multimedia-Network"
permalink: /Wireless-Multimedia-Network/2-Introduction-to-Quality-of-Service/
layout: default
---
# Lecture 2 - Introduction to Quality of Service (QOS)

![](https://t3764800.p.clickup-attachments.com/t3764800/03db74b4-a70b-4121-9def-f474f0324dd8/Screen%20Shot%202023-10-21%20at%2010.16.32%20PM.png)



![](https://t3764800.p.clickup-attachments.com/t3764800/c00a8da4-836d-46c9-93c8-acf2b81995ac/Screen%20Shot%202023-10-21%20at%2010.17.14%20PM.png)

# QoS - Quality of Service

*   **兩個主要目標**
    *   在託管網絡中提供性能保證
    *   支持用戶/流之間的服務差異化
*   QoS 的正式定義
    *   在網絡中提供資源保證和服務差異化的能力通常稱為服務質量
*   如何提供 QoS？
    *   正確定義所採用的 QoS 指標 （QOS index）
    *   資源分配機制（即用戶/資源調度）

![](https://t3764800.p.clickup-attachments.com/t3764800/70900d98-5904-4c6a-a0b4-f0874757d297/Screen%20Shot%202023-10-22%20at%2012.13.19%20PM.png)

IPTD、IPDV、IPLR 和 IPER ([https://doc.clickup.com/d/h/3jwj0-4402/42076b1e495a1cc](https://doc.clickup.com/d/h/3jwj0-4402/42076b1e495a1cc))是四個用於衡量 IP 網絡性能的指標，越低，表明網絡性能越穩定。

擁塞或延遲等問題：

*   IPTD: IP packet transfer delay （IP 數據包傳輸延遲）
*   IPDV: IP packet delay variance（IP 數據包延遲變化率）

丟包或錯誤等問題：

*   IPLR: IP packet loss ratio （IP 數據包丟失率）
*   IPER: IP packet error ratio （IP 數據包錯誤率）

![](https://t3764800.p.clickup-attachments.com/t3764800/570c22c7-fc9b-451a-999a-f3c06c445187/Screen%20Shot%202023-10-22%20at%201.30.44%20PM.png)

Delay variance/Delay jitter（延遲變化/延遲抖動）：表示為網絡平均延遲的偏差平均值。

減少延遲變化/延遲抖動的方法：

*   使用專用網絡：專用網絡可以避免與其他用戶共享資源，從而減少延遲變化/延遲抖動。
*   使用 QoS 機制：QoS 機制可以為高優先級流量分配更多的資源，从而減少延遲變化/延遲抖動。
*   使用帶寬緩衝：帶寬緩衝可以吸收流量波動，从而減少延遲變化/延遲抖動。

![](https://t3764800.p.clickup-attachments.com/t3764800/fb074cf0-9035-4423-9714-cb0177f51c2e/Screen%20Shot%202023-10-22%20at%201.37.17%20PM.png)

# 5QI（5G QoS 識別碼）

5G-ASIA Defined 5QI 是由 5G-ASIA（5G 亞洲）組織定義的一套 5G QoS 識別碼（5QI）標準。5G-ASIA Defined 5QI 定義了 16 個 5QI，用於為不同的服務提供不同的 QoS。



GBR 是 Guaranteed Bit Rate 的縮寫，表示保證比特率。在 5G 網路中，GBR 是一種資源類型，它可以保證用戶或流獲得特定的比特率。

![](https://t3764800.p.clickup-attachments.com/t3764800/0132bf6b-009d-4bf1-a270-79c3e8901e6c/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/bbf99866-6759-47a1-8d9c-ad83a3e5b9c3/Screen%20Shot%202023-10-22%20at%201.50.55%20PM.png)

# What's Resource Allocation 什麼是資源分配？

*   **網絡元素執行以滿足用戶/應用需求的過程**
    *   網絡元素執行以滿足用戶/應用需求的過程通常稱為 **資源管理**。資源管理是指網絡元素用於分配和管理網絡資源（例如帶寬和緩存）的過程。

**提到的資源是什麼？**

提到的資源是：

*   Bandwidth of the links（連結的頻寬）
*   Buffers at the routers and switches（路由器和交換機上的緩存）

**為什麼？**

*       *   路由器/交換機上的數據包會爭奪鏈路的連接使用權。
    *   這些爭用的數據包會被放在佇列中等待通過鏈路傳輸。

> 網絡元素執行資源管理以確保網絡能夠滿足用戶/應用對網絡資源的需求。  
> 例如，如果鏈路上的數據包太多，則網絡元素會將數據包放在隊列中等待傳輸。  
> 這會導致數據包傳輸延遲的增加。  
> 為了減少數據包傳輸延遲，網絡元素可以使用各種資源管理技術，例如：  
> **優先級**：為高優先級的數據包分配更高的優先級，以便它們在隊列中獲得優先處理。  
> **預留**：為高優先級的數據包預留一定的帶寬。  
> **限速**：限制低優先級的數據包的帶寬。  
> **緩存**：使用緩存來存儲數據包，以便在隊列中等待的數據包能夠更快地傳輸。  
>   



![](https://t3764800.p.clickup-attachments.com/t3764800/290a2e36-5557-4169-9c46-8c279aa98536/Screen%20Shot%202023-10-22%20at%201.58.03%20PM.png)

# **資源分配 (Resource Allocation) vs 擁塞控制 (Congestion control)**

資源分配：指根據用戶和應用程序的需求，分配和管理網絡資源（例如帶寬和緩存）的過程。

擁塞控制：指通過限制發送到網絡中的流量來防止網絡擁塞的過程。

*   **當太多數據包爭奪同一個鏈路時會發生什麼**
    *   佇列將會溢出（overflow），封包丟棄（packets drop）
    *   封包丟棄將觸發重傳（retransmission）
    *   惡性循環導致網絡擁塞和無響應
*   **網絡應提供擁塞控制機制來應對這種情況**
    *   **TCP 擁塞控制**：TCP 擁塞控制是一種用於控制 TCP 連接中數據流的機制。TCP 擁塞控制使用多種技術（例如慢啟動和擁塞避免）來確保發送方不會以比網絡所能處理的速度更快地將數據發送到網絡中。
    *   **顯式擁塞通知 (ECN)**：ECN 是一種允許路由器通知主機擁塞的機制。當路由器檢測到擁塞時，它可以設置 IP 標頭中的 ECN 標誌。當主機收到帶有 ECN 標誌的數據包時，它可以降低其傳輸速率。
    *   **隊列管理**：隊列管理是一種用於管理路由器和交換機中隊列的機制。隊列管理技術可以用於對數據包進行優先級排序並在必要時丟棄數據包。

![](https://t3764800.p.clickup-attachments.com/t3764800/79c597ec-0cda-431c-ae66-10565667392d/Screen%20Shot%202023-10-22%20at%202.19.31%20PM.png)

*   在整個網絡中分配資源具有很高的難度，因為資源是分佈式的。
*   傳統互聯網的策略是：
    *   允許源端盡可能多地發送數據（send as much as it can）
    *   在擁塞發生時進行恢復（recover when congestion）
    *   這種方法比較簡單，但可能會造成網絡丟棄大量數據包，從而導致網絡中斷（disruptive）。
        *   丟棄大量數據包：在擁塞發生時，路由器會丟棄大量數據包。這會導致重傳，從而降低網絡性能。
        *   網絡中斷：丟棄大量數據包可能會導致網絡中斷，因為許多服務和應用程序需要可靠的數據流。

![](https://t3764800.p.clickup-attachments.com/t3764800/8d9c1c69-5da5-46c8-accd-05b3062648f2/Screen%20Shot%202023-10-22%20at%202.24.41%20PM.png)

是否有更好的合作方式？

*   在網絡元素中（network elements）
    *   可以使用各種佇列管理（queuing disciplines）策略來控制數據包的傳輸順序和丟棄哪些數據包。
        *   EX. 可以對高優先級的數據包（例如語音通話和視頻流）進行優先傳輸，並在擁塞發生時丟棄低優先級的數據包（例如文件傳輸）。
*   在主機端（hosts’ end）
    *   擁塞控制機制（congestion control mechanism）控制源端允許發送數據包的速度。
        *   EX.來源端可以根據從網絡收到的反饋來調整其傳輸速率。



傳統互聯網：策略主要依靠路由器在擁塞發生時丟棄數據包來進行擁塞控制。然而，這會導致源端收到的數據包丟失，從而降低網絡性能。

現代互聯網：正在努力在網絡元素和主機端之間進行更好的合作，以提高擁塞控制的效率。



![](https://t3764800.p.clickup-attachments.com/t3764800/7fc85a01-2b60-4b31-a4dd-2f74ae631218/Screen%20Shot%202023-10-22%20at%202.34.39%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/6217b373-535c-4aa8-9f14-e5cbec8452d1/Screen%20Shot%202023-10-22%20at%202.49.42%20PM.png)

# **資源分配的分類**

*   **路由器中心化（Router-centric） vs 主機中心化（ host-centric）**
    *   _傳統_ \- 路由器中心化：路由器負責決定何時發送數據包、選擇要丟棄哪些數據包，並通知主機允許發送多少數據包。
        *   缺點：路由器附載可能導致網絡擁塞
    *   _現代_ \- 主機中心化：主機觀察網絡狀況並相應地調整其行為。
        *   缺點：主機需要進行複雜的計算，可能導致主機之間的不公平j
    *   這兩種方式並不互斥。
*   **基於預留（**Reservation-based**） vs 基於反饋（**Feedback-based**）**
    *   基於預留：主機➝網絡請求為流分配一定的容量。
        *   缺點：網絡資源的浪費
    *   基於反饋：主機在不預留任何容量的情況下開始發送數據，然後根據收到的反饋調整其發送速率。反饋可以是“顯式”的或“隱式”的。
        *   缺點：可能會導致主機之間的不公平
*   **基於窗口（**Window-based**）vs. 基於速率（**rate-based**）**
    *   **基於窗口**：最著名的基於窗口的資源分配方式是 TCP。在 TCP 中，接收方（receiver）會向發送方（sender）發送一個窗口。該窗口限制了發送方（sender）可以傳輸多少數據。
        *   **基於窗口的資源分配方式**：TCP、UDP
    *   **基於速率**：基於速率的資源分配方式控制發送方（sender）每秒可以發送多少比特，以便接收方或網絡可以吸收。基於速率的控制對於多媒體應用來說很有意義。
        *   **基於速率的資源分配方式**：ATM、CBR、VBR

![](https://t3764800.p.clickup-attachments.com/t3764800/f9d571e0-c7d8-437a-b127-64bfebcd91aa/Screen%20Shot%202023-10-22%20at%202.57.58%20PM.png)

# 評估標準（Evaluation Criteria）

*   **我們期望資源分配機制做些什麼？**
    *   期望資源分配機制能夠有效和公平地分配網絡資源。
*   **如何****評估****已採用的資源分配機制的****有效性****？**
    *       *   可以使用吞吐量（throughput）和延遲性（delay）能來評估已採用的資源分配機制的有效性。
        *   但是，吞吐量和延遲會相互矛盾。
        *   我們希望向網絡中發送盡可能多的數據包，以將所有鏈路的利用率提高到 100%。
        *   但是，這將導致網絡中佇列中數據包的數量增加，從而導致佇列長度和排隊延遲也增加。



![](https://t3764800.p.clickup-attachments.com/t3764800/1471399d-549d-4487-bc0b-090f39021966/Screen%20Shot%202023-10-22%20at%203.03.59%20PM.png)

*   評估資源分配方案有效性的常見指標之一是吞吐量與延遲的比率，即：

```plain
Power = (Throughput) / (Delay)
```

*   目標是最大化此比率（最大為 1）。
*   下圖顯示了一個具有代表性的功率曲線。
*   功率曲線（power curve）與分時計算系統（timesharing computer system）中的系統吞吐量曲線（throughput curve）非常相似。
    *   x 軸表示延遲，y 軸表示吞吐量。
        *   曲線的起點表示沒有擁塞，延遲為 0，吞吐量為最大。
        *   隨著擁塞（load）的增加，延遲（delay）會增加，吞吐量會減少。
    *   功率曲線的曲率越陡，表明在吞吐量和延遲之間的權衡越大。在這種情況下，為了提高吞吐量，需要接受更高的延遲。

![](https://t3764800.p.clickup-attachments.com/t3764800/7ca14fde-21fe-4ed1-9f39-b1ded0561c0b/Screen%20Shot%202023-10-22%20at%203.12.08%20PM.png)

*   **如何評估資源分配的公平性？**
    *   公平性（Fairness）是指每個流都能獲得平等的帶寬份額
    *   但是，平等分可能不平等。
*   **本地公平份額（**Locally fair share**）vs 全局公平份額（**globally fair share**）**
    *   本地公平份額：指根據局部信息（例如鏈路容量）來分配資源。
    *   全局公平份額：指根據全局信息（例如流的長度）來分配資源。

![](https://t3764800.p.clickup-attachments.com/t3764800/67bd3d25-75c0-43f8-8a4e-c314eaa4baa7/Screen%20Shot%202023-10-22%20at%203.19.07%20PM.png)

假設有三個流：流 A、流 B 和流 C。流 A 始於路由器 1，流 B 始於路由器 2，流 C 始於路由器 3，所有三個流都到達路由器 4。鏈路 1-4 和鏈路 2-4 的容量均為 100 Mbps，鏈路 3-4 的容量為 50 Mbps。

如果使用本地公平份額分配資源，則每個流將獲得 33.3 Mbps 的帶寬。但是，流 C 的長度比流 A 和流 B 的長度短得多。因此，使用本地公平份額分配資源並不公平。

如果使用全局公平份額分配資源，則流 C 將獲得更多的帶寬，而流 A 和流 B 將獲得更少的帶寬。這是因為全局公平份額考慮了流的長度。

![](https://t3764800.p.clickup-attachments.com/t3764800/d89e7567-2139-4718-875f-d1798fdc97bc/Screen%20Shot%202023-10-22%20at%203.21.09%20PM.png)

## Jain's Fairness Index

*   Jain’s公平性指數是一種用於衡量資源分配公平性的指標。
*   該指數的範圍在 0 到 1 之間，1 代表最公平。
*   Jain’s公平性指數
    *   Formula：J = (Σ(Ri)^2) / (n \* (ΣRi)^2)
        *   J 是 Jain 公平指數。
        *   Ri 表示第 i 個用戶的資源分配或利用率。
        *   n 是用戶的總數。
    *   假設有 n = 3 個流，每個流的吞吐量都為 1，則 Jain’s公平性指數為：
    ```plain
    Jain's fairness index = ( (1 + 1 + 1)^2 ) / (3 * 1^2 + 3 * 1^2 + 3 * 1^2) = 1
    ```
    *   如果有一個流的吞吐量增加到 1 + 口 則 Jain’s公平性指數將變為：
    ```plain
    Jain's fairness index = ( (1 + 1 + 1 + )^2 ) / (3 * 1^2 + 3 * 1^2 + 3 * 1^2 + 3 * ^2) < 1
    ```

## Weighted Jain's Fairness Index

*   formula：J\_weighted = (Σ(wi **Ri)^2) / (n** (Σwi \* Ri)^2)
    *   J\_weighted 是加權 Jain 公平指數。
    *   Ri 仍然是第 i 個用戶的資源分配或利用率。
    *   n 是用戶的總數。
    *   wi 是分配給第 i 個用戶的權重。
*   EX：三個不同的用戶添加權重 1.5、3.5 和 1。讓我們假設這些用戶被標記為用戶 1、用戶 2 和用戶 3，並且它們各自的分配是 R1、R2 和 R3。以下是計算加權 Jain 公平指數的方法：

```plain
J_weighted = [(1.5 * R1)^2 + (3.5 * R2)^2 + (1 * R3)^2] / [n * (1.5 * R1 + 3.5 * R2 + 1 * R3)^2]/
```



![](https://t3764800.p.clickup-attachments.com/t3764800/07c3e08a-5a8b-44f0-aab6-d372950d0bd8/Screenshot_20231022_215631_Adobe%20Acrobat.jpg)

# Queueing Disiplines（排隊管理）

*   排隊管理是一種用於控制路由器在轉發數據包之前如何緩存數據包的機制。
    *   分配帶寬（哪些數據包將被傳輸）
    *   緩存空間（哪些數據包將被丟棄）
    *   排隊管理算法直接影響數據包的延遲，因為它決定了數據包等待傳輸的時間。
*   **兩種常見的排隊管理算法是先進先出 (FIFO) 和公平排隊 (FQ)**
    *   **先進先出 (FIFO)**：FIFO 算法是一種簡單的排隊管理算法。FIFO 算法根據數據包到達路由器緩存的順序依次傳輸數據包。FIFO 算法的優點是簡單易行，但缺點是可能會導致高優先級數據包被延遲。
    *   **公平排隊 (FQ)**：FQ 算法是一種更複雜的排隊管理算法。FQ 算法會根據數據包的優先級來決定傳輸數據包的順序。FQ 算法的優點是可以確保高優先級數據包不會被延遲，但缺點是可能會導致低優先級數據包的延遲。
        *   語音通話和視頻流：高優先級的應用，通常會使用 FQ 算法
*   **排隊管理的重要性**
    *   影響網絡的性能和可靠性。
    *   合理的排隊管理算法可以提高網絡的吞吐量、降低延遲和丟包率。

## FIFO

![](https://t3764800.p.clickup-attachments.com/t3764800/c2c71529-7f85-4386-9905-15696bb47e7d/Screenshot_20231022_220722_Adobe%20Acrobat.jpg)

*   到達路由器的第一個數據包將被首先傳輸。
*   到達 FIFO 隊列尾端的所有數據包將被丟棄（尾部丟棄）。
*   不論數據包屬於哪個流或有多重要，都會被丟棄（忽略Priority）。
*   請注意，排程規律（scheduling discipline）（此指FIFO）不同於丟棄策略（drop policy）。
    *   排程規律決定了哪些數據包將被傳輸，而丟棄策略決定了哪些數據包將被丟棄。
    *   排程規律（scheduling discipline）：
        *   **先進先出 (FIFO)**：按照數據包到達路由器的順序依次傳輸數據包。
        *   **優先級排序 (PQ)**：根據數據包的優先級來決定傳輸數據包的順序。
        *   **輪詢 (RR)**：每個數據包輪流傳輸一次，直到所有數據包都傳輸完畢。
    *   丟棄策略（drop policy）：
        *   **尾部丟棄 (tail drop)**：當隊列已滿時，丟棄隊列尾端的數據包。
        *   **隨機丟棄 (random drop)**：從隊列中隨機丟棄數據包。
        *   **分類丟棄 (class-based drop)**：根據數據包的類型或屬性來丟棄數據包。

## Priority Queueing（**優先級隊列**）

![](https://t3764800.p.clickup-attachments.com/t3764800/e7f7a158-bdb9-4cff-9c1f-467d3fbc0539/Screenshot_20231022_221757_Chrome.jpg)

*   優先級隊列是一種改進的基本 FIFO 排程規律。其基本思想是：
    *   為每個數據包分配一個優先級。
    *   路由器實現多個 FIFO 隊列，每個優先級類別一個隊列。
    *   路由器總是從優先級最高的隊列中傳輸數據包（如果該隊列是非空的），然後再移到下一個優先級隊列。
    *   在每個優先級內，數據包仍然以 FIFO 的方式管理。
*   優先級隊列也存在一個問題：雖然可以確保高優先級數據包不會被延遲，但**高優先級數據包可能會過度佔用資源，導致****低優先級數據包被延遲或丟棄****。**
    *   Solution：
        *   將高優先級數據包的優先級進一步細分，以確保不同高優先級數據包之間能夠公平地獲得資源。
        *   使用加權公平隊列 (WFQ) 算法來為不同優先級的數據包分配資源，以確保所有優先級的數據包都能公平地獲得資源。

## Fair Queueing（**公平排隊**）

![](https://t3764800.p.clickup-attachments.com/t3764800/8a268106-a034-43ed-b3e4-ff84b8c11dc3/Screenshot_20231022_222718_Chrome.jpg)

*   **FIFO 排程規律的主要問題：**
    *   FIFO 排程規律沒有區分不同的流量來源，也沒有根據數據包所屬的流（flow）來分隔數據包。
*   **公平排隊 (FQ) 的理念：**
    *   FQ 路由器會為每個當前正在處理的流維護一個獨立的隊列。
    *   路由器會根據數據包所屬的隊列來決定傳輸數據包的順序。
*   FQ 通常使用以下方法來實現：
    *   每個數據包都會分配一個隊列 ID，該隊列 ID 表示數據包所屬的隊列。
    *   路由器會根據數據包的隊列 ID 來決定傳輸數據包的順序。
    *   如果某個隊列中的數據包已全部傳輸完畢，則路由器會從具有最高優先級的非空隊列中傳輸數據包。

![](https://t3764800.p.clickup-attachments.com/t3764800/06a89704-7c7a-4c92-b660-bc7b156cec16/Screenshot_20231022_223245_Chrome.jpg)

*   公平排隊 (FQ) 面臨的主要挑戰是，在路由器中處理的數據包長度不一定相同。
*   為了以公平的方式分配出站鏈路的帶寬，有必要考慮數據包長度。
*   舉例來說，如果一個路由器正在管理兩個流，一個流的數據包大小為 1000 bytes，另一個流的數據包大小為 500 bytes（可能是因為在這個路由器上游upstream發生了分片fragmentation），那麼簡單地從每個流的隊列中輪詢（Round Robin）服務數據包會使第一個流獲得鏈路帶寬的三分之二，而第二個流只獲得鏈路帶寬的三分之一。

![](https://t3764800.p.clickup-attachments.com/t3764800/d36be875-ac25-4eb4-b1c8-928bb175360d/Screenshot_20231022_224050_Adobe%20Acrobat.jpg)

*   我們真正想要的是逐位輪詢（bit-by-bit round robin），也就是說，路由器會從流 1 傳輸一個位元，然後從流 2 傳輸一個位元，依此類推。
*   顯然，將不同數據包中的位元交織在一起是不切實際的。
*   因此，FQ 機制通過首先確定一個給定的數據包在使用 bit-by-bit round robin 傳輸時將完成傳輸的時間，然後使用此完成時間來對數據包進行排序以進行傳輸，來模擬此行為
*   對於一個 流，令：
    *   _Pi_​ 表示第 _i_ 個數據包的長度
    *   _Si_​ 表示路由器開始傳輸第 _i_ 個數據包的時間
    *   _Fi_​ 表示第 _i_ 個數據包完成傳輸的時間
    *   F\_i = S\_i + L\_i

![](https://t3764800.p.clickup-attachments.com/t3764800/5cb39be1-3f99-4098-9578-29c32e197fc1/Screenshot_20231022_224655_Chrome.jpg)

*   **我們什麼時候開始傳輸數據包？**
*   這取決於該數據包（packet i）是否完成傳輸前一個數據包（packet i-1）的傳輸。
*   假設Ai表示第 _i_ 個數據包到達路由器的時間
    *   _Si_​ 表示路由器開始傳輸第 _i_ 個數據包的時間
    *   _Fi_−1​ 表示第 _i_−1 個數據包完成傳輸的時間
    *   _Ai_​ 表示第 _i_ 個數據包到達路由器緩存的時間
    *   故 Si = max(Fi-1，Ai) + Pi
*   對於每個流，我們使用上述公式計算 F_i_​ 值。
*   然後，我們將所有 F_i_​ 值視為時間戳
*   並從完成時間戳最小（lowest finish timestamp）的數據包開始傳輸。

![](https://t3764800.p.clickup-attachments.com/t3764800/6ade4159-1d9a-49dd-a5fb-0b6e201d3940/Screenshot_20231022_230156_Adobe%20Acrobat.jpg)

*   **公平排隊的兩個注意事項**
    1. 只要工作隊列中至少有一個數據包，鏈路將永遠不會閒置（我們稱之為工作守恆）。
    2. 如果鏈路已滿載並且有 _n_ 個流正在發送數據，則任何一個流都不能使用超過 _n_1​ 的鏈路帶寬。如果一個流嘗試發送超過此值，則它本身將會遇到長時間的延遲。
*   加權公平隊列 (WFQ) 是 FQ 的一種變體。
    *   每個流（隊列）都分配一個權重。
    *   該權重在邏輯上指定了路由器在為該隊列提供服務時每次傳輸多少位元。
    *   因此，該權重控制了該流將獲得的鏈路帶寬的百分比。
    *   舉例來說，如果兩個流被分配的權重分別為 1 和 2，則流 2 將獲得鏈路帶寬的 2/3。

## Proportional Fair Resource Allocation（**比例公平性**）

![](https://t3764800.p.clickup-attachments.com/t3764800/d4834c0d-2933-4dd3-ba7c-f4385c7592df/Screenshot_20231022_230510_Adobe%20Acrobat.jpg)

*   **比例公平性的動機**
    *   **最大化無線網絡的總吞吐量，同時允許所有用戶獲得至少最低水平的服務。**
*   **形式定義**
    *   令 _T_ 表示觀察時間持續時間
    *   _Ti_​ 表示 flow _i_ 使用的時間
    *   _Ri_​ 表示流 _i_ 的 datarate
    *   則流 _i_ 的吞吐量為 _Si_​=(_Ti_​_Ri_​)/_T_。
    *   比例公平性是指實現以下目標： ![](https://t3764800.p.clickup-attachments.com/t3764800/2e88b268-1543-457a-80bc-e0f927521ac8/Screenshot_20231022_230827_Chrome.jpg)
    *   _U_(⋅) 是效用函數
    *   常用的效用函數是 log(⋅)

## Max-Min Fair Resource Allocation

![](https://t3764800.p.clickup-attachments.com/t3764800/644da614-2b33-48d0-80c2-5e51b7b261be/Screenshot_20231022_231013_Adobe%20Acrobat.jpg)

*   最大化所有用戶獲得的最小資源量。
*   **示例：**
    *   瓶頸鏈路（bottle neck）是 link AC。
    *   首先在鏈路 AC 上進行資源分配。
    *   由於已確定分配給深綠色流的資源，因此下一個瓶頸鏈路是鏈路 AB。因此，分配給黃色流的速率是 1-1/3 = 2/3
    *   分配給藍色流的速率是 2 - 2/3 = 4/3。
*   通過首先為每個用戶分配最低所需的資源，比例公平性可以確保所有用戶都能獲得至少最低水平的服務。然後，比例公平性會將剩餘的資源分配給各個用戶，以使其吞吐量最大化。