---
title: "Wireless-Multimedia-Network"
permalink: /Wireless-Multimedia-Network/9-Dynamic-Reuse-of-Unlicensed-Spectrum/
layout: default
---
# Lecture 9 - Dynamic Reuse of Unlicensed Spectrum

# LTE-Unlicensed Program and Standardization

*   Motivation?
    *   Drastic increase in mobile network traffic(license band NOT ENOUGH) → operators consider offloading(卸載) their traffic to the unlicensed band (運營商考慮將流量卸載到未授權頻段)
*   Approaches
    *   Carrier WiFi: Wifi APs are deployed by operators as an integral part of network structure(將 WiFi AP 部署為網路結構的組成部分)
        *   Advantage: reduce the congestion and provide better Internet access to customers(降低擁塞，為客戶提供更好的上網體驗)
        *   Disadvantage: carrier WiFi adopts different access and management mechanisms from the LTE network (control and authentication), and this leads to inefficiency in network management and spectrum usage(Carrier WiFi 採用與 LTE 網路不同的接入和管理機制（控制和身份驗證），這導致網路管理和頻譜利用率低效)



*       *       *   LTE 要有資訊送給基地台，wifi 不用
        *   LTE 主要使用授權頻段，由政府機構分配給運營商，確保運營商可以提供可靠的服務



➝ Operators are looking to access the 5 GHz unlicensed band using a unified LTE network \[e.g., LTE-U, LAA, LWA\]



![](https://t3764800.p.clickup-attachments.com/t3764800/6cb8bb1f-99e1-4f01-b1b7-81a953ba0ee4/image.png)

LTE-U, LAA, LWA 將行動通訊跟 unlicensed band 結合再一起，讓行動通訊用，不是Wifi用

> \[1\] Zhengyu Zhou, et al., “Cloud Miracles: Heterogeneous Cloud RAN for Fair Coexistence of LTE-U and WiFi in Ultra Dense 5G Networks,” IEEE Communications Magazine, June 2018, pp. 64-71.

wifi是分散式系統



# Quick Overview

*   不同spectrum 射頻電路設計要不一樣
*   高頻容易衰減
*   小基站補coverage hole (黃色) 要花錢
*   4G才有，carrier aggregation 載波聚合，射頻電路要改 所以2G 3G那時沒有這個功能
*   2.4GHz忙碌



*   LTE-U是在ISM band上直接傳輸LTE的訊號
    *   設計一種特有的頻譜共享機制, 和Wi-Fi一起競爭5GHz的通訊頻帶
    *   所收到的兩個不同頻帶訊號在手機上在合成為一個訊號
    *   LTE宣稱其設計的機制能比Wi-Fi更有效率，但也面臨Wi-Fi陣營的抵制與挑戰
*   LTE-H ➝ LTE Wi-Fi Link Aggregation (LWA)
    *   無線接取也使用Wi-Fi的技術
    *   封包的整合
        *   LWA將Wi-Fi只是為一組無線傳輸的介面，而其中的資料, 將再通過LTE的PDCP層\* (Packet Data Convergence Protocol Layer)和透過LTE通訊協定所接收的封包結合
        > 你用手機看影片時, 原本影片只會藉由Wi-Fi或是LTE傳送,而透過LWA的技術, 影片封包將透過Wi-Fi以及LTE一起傳送
        >
        >   
        >
        > \*PDCP層在LTE架構中, 屬於第二層架構, 在MAC層和RLC層之上,
        >
        > 主要負責: 資料封包的標頭 (header) 壓縮與解壓縮, 資料加密/解密, 資料完整性的保護,

# ![](https://t3764800.p.clickup-attachments.com/t3764800/3d08e1d1-7a21-4fef-bf29-bb3007910062/image.png)

> Source:[https://note-on-clouds.blogspot.com/2017/02/lte-lwa-1.html](https://note-on-clouds.blogspot.com/2017/02/lte-lwa-1.html)

# LTE-Unlicensed (LTE-U)

*   Developed by the LTE-U Forum, formed in 2014 by Verizon, Alcatel-Lucent, Ericsson, Qualcomm, and Samsung, based on 3GPP Releases 10, 11, and 12
*   The goal is to use the existing features in the LTE 3GPP spec. and adapt them to unlicensed operation that do not mandate LBT (Listen-before-talk) (其主要目標是利用現有的 LTE 3GPP 規範並加以調整，使其適用於未授權頻段操作，不需要 LBT (聆聽-再傳輸) 機制)
*   Frequency bands are 5,150-5,250 MHz and 5,725-5,850 MHz
*   Mechanisms used for LTE-U to better coexist with WiFi
    *   Carrier selection
        *   LTE-U 可以選擇與 Wi-Fi 互不干擾的載波頻段，減少彼此之間的競爭
    *   On-off switching
        *   LTE-U 基站可以在感知到 Wi-Fi 活動時暫停傳輸，避免干擾正在進行的 Wi-Fi 通信
    *   Carrier-sensing adaptive transmission (CSAT)
        *   LTE-U 基站可以監測 Wi-Fi 信號強度，調整自己的發射功率，降低對 Wi-Fi 的干擾



*   Carrier selection
    *   在 LTE-U 系統中，載波選擇是指 eNB（基站）選擇合適的載波頻段（channel）進行傳輸的過程，目的是找到干擾最少的頻段，以保障 LTE-U 與其他系統的和諧共存



*       *   An eNB（基站）performs carrier selection at startup, periodically, and based on performance triggers
        *   Carrier selection **運作時機：**
            *   eNB 開機啟動時
            *   定期執行（例如每隔一段時間）
            *   基於性能觸發（例如當檢測到干擾過高時）
*       *   Carrier selection is to find the channel that is free of interference
        *   **優先選擇無干擾的頻段：** eNB 會掃描可用的頻段，尋找沒有其他系統在使用的頻段
*       *   If all channels are occupied by other systems, an eNB chooses the channel with the lowest detected signal power level
        *   **選擇干擾最少的頻段：** 如果所有頻段都被占用，eNB 會選擇檢測到的訊號功率最低的頻段，以降低對其他系統的干擾
*       *   Carrier selection algorithm was left to be implementation-specific
        *   載波選擇算法並未在標準中強制規定，而是留給各廠商自行實現，以適應不同的網路環境和需求
*   On-off switching
    *   When the traffic demand is low, the eNB can stop transmitting in the unlicensed spectrum and relies only on the licensed spectrum
        *   在 LTE-U 系統中，開關控制是指 eNB（基站）在交通需求較低時，可以暫停在未授權頻段的傳輸，只依靠授權頻段進行傳輸。此機制可以降低 LTE-U 對其他系統（如 Wi-Fi）的干擾，並節省未授權頻譜資源
    *   LTE-U spec defines two states for the LTE-U secondary cell (SC)
        *   Off-state: the SC stop any type of transmission（SC 停止任何類型的傳輸，完全釋放未授權頻段）
        *   On-state: the SC is either transmitting full LTE frames or transmitting the LTE-U discovery signal (LDS)（SC 會傳輸完整的 LTE 幀或 LTE-U 發現信號（LDS））
        *   LDS is transmitted by the SC at a certain subframe (subframe number 5) and with fixed time intervals (which can be either 40, 80, or 160 ms)
        *   LDS contains the physical signals and channels required for the LTE UE to obtain time and frequency synchronization and to perform SC measurements
        *   **LDS（LTE-U Discovery Signal）：**
            *   是一種特殊的信號，用於通知 UE（用戶設備） SC 的存在並提供同步資訊。
            *   傳輸時間：在特定的子幀（子幀編號 5）和固定的時間間隔（可以是 40、80 或 160 毫秒）。
            *   包含 UE 進行同步和測量所需的物理訊號和通道
*   Carrier-sensing adaptive transmission (CSAT)
    *   The mechanism that allows an eNB to share the spectrum with other systems using the same channel in a time-division multiplex (TDM) manner
        *   在 LTE-U 系統中，CSAT 是一種允許 eNB（基站）以時間分割多工（TDM）的方式與其他使用相同頻道的系統共享頻譜的機制。它類似於一種自適應靜音算法，旨在降低 LTE-U 對其他系統（如 Wi-Fi）的干擾
    *   Conceptually CSAT is a sort of adaptive muting algorithm, where the eNB initially and periodically senses the channel for relatively long time periods (in the range between 0.5 and 200 ms)
        *   **頻道感知：** eNeNB 會定期（0.5 至 200 毫秒之間）感知頻道的使用情況，偵測是否有其他系統在使用相同的頻道
    *   SC adjusts its duty cycle and define a time cycle for transmission according to the channel activity and WiFi signal detection
        *   **調整占空比：** 根據頻道活動和 Wi-Fi 訊號偵測結果，SC（次級小區）會動態調整其占空比（Duty Cycle），即傳輸時間與靜默時間的比例
    *   Constraint values in LTE-U
        *   Min off-state period: 1 ms
        *   Max off-state period: 40, 80, or 160 ms
        *   Min on-state period: 4 ms in case of available user data, and 1 ms otherwise
        *   Max on-state period: 20 ms
        *   Energy detection threshold: -62 dBm
*   In Feb. 2017, the FCC certified the 1st LTE-U device
*   In June 2017, T-Mobile launches LTE-U on its network in 6 cities in the US
*   Recent coexistence results showed that the throughput of WiFi usually decreases when sharing the same channel with any LAA/LTE-U
    *   近期研究表明，當 Wi-Fi 與 LAA/LTE-U 共享同一頻道時，Wi-Fi 的吞吐量通常會下降

> 1\. Through sensing the usage of neighboring nodes and adjust the frequency in the unlicensed frequency band to avoid interference (job of CSAT)
>
> 2\. On-off switching is to achieve fair sharing with other devices on the same channel



# Licensed-Assisted Access (LAA)

*   LAA was approved by 3GPP within Release 13 in June 2015 and it specifies the utilization of unlicensed spectrum to boost downlink through a process of carrier aggregation via supplemental downlink (LAA (Licensed Assisted Access) 是一種技術，允許 LTE 網路利用未授權頻段 (5150-5925 MHz) 來提升下行數據吞吐量，它主要通過載波聚合 (CA) 的方式，將授權頻段 (PCell) 和未授權頻段 (SCells) 的載波進行組合，以提供更大的頻寬和更高的傳輸速率。)
*   At the same time, 3GPP approved an enhanced LAA (eLAA) Work Item in Release 14, which aims at identifying uplink transmission in the 5 GHz band
*   All control and signaling information is carried onto licensed carrier (PCell) and other carriers from unlicensed bands (SCells) can be used to increase data throughput
    *   控制和信號信息仍然在授權頻段 (PCell) 傳輸，未授權頻段 (SCells) 僅用於數據傳輸
*   Which bands and what bandwidth do the LAA utilize?
    *   Bands 46 & 47, 5,150 MHz – 5,925 MHz
    *   Band 47 is within 5,855 MHz ~ 5,925 MHz, a subset of band 46
    *   10 MHz & 20 MHz bandwidth

> Interference avoidance technology: LTE-U is CSAT; LAA is LBT

*   Functionalities being added in LAA
    *   Listen Before Talk (LBT): started by Sony, Intel, Huawei, Nokia, Qualcomm, ETSI, and so on. The adopted interference avoidance technology of LAA(LBT (Listen Before Talk) 監控未授權頻段的使用情況，避免與其他系統 (如 Wi-Fi) 產生干擾)
    *   Frame structure type 3: new frame structure designed to make LTE signal similar to WLAN burst and make the LTE signal to better coexist with the existing WLAN operation (優化與 Wi-Fi 等系統的共存)
    *   Discovery reference signals (DRS): introduced in 3GPP Release 12 as part of a feature set for enhancement towards small cell operation

> \[2\] Youjia Chen et al., “Dynamic Reuse of Unlicensed Spectrum: An Inter-Working of LTE and WiFi,” IEEE Wireless Communications, Oct. 2017, pp. 52-59.



**LAA 和 LTE-U 的區別:**

*   LAA 和 LTE-U 都使用未授權頻段，但干擾避免技術不同。LAA 使用 LBT，而 LTE-U 使用 CSAT。
*   LAA 主要提升下行數據吞吐量，而 LTE-U 可以提升上下行數據吞吐量





*   LBT
    *   在未授權频段中，為了避免不同設備之間的相互干擾，LBT 機制要求所有設備在傳輸數據之前先進行「監聽（Listen）」，確認頻道是否空閒。如果頻道空閒，則可以開始「傳輸（Talk）」
    *   Any device who wants to transmit in unlicensed radio channel has to first sense the channel (Listen)
    *   Once a clear channel is available, it can start transmission (Talk)
    *   The data transmission is limited by a max channel occupancy time (MCOT) for fairness purpose
        *   **最大頻道占用時間（MCOT）：** 即使頻道空閒，設備的傳輸時間也受到 MCOT 的限制，以確保其他設備也能有機會使用頻道
    *   Sensing the channel through energy detection (ED) is called clear channel assessment (CCA)
        *   If the detected energy is below the ED threshold, the LAA node begins transmission immediately; otherwise, the LAA node performs extended CCA (eCCA)
            1. **頻道感知（CCA）：** 設備通過能量偵測（ED）來感知頻道是否有其他設備正在使用。如果偵測到的能量低於閾值，則表示頻道空閒。
        *   Extended CCA (eCCA): when detecting channel busy during the initial CCA, the LAA node waits for a duration consisting of a defer duration and a backoff period which contains a random number of additional extended CCA time slots, and then performs CCA again
            1. **擴展頻道感知（eCCA）：** 如果初始 CCA 偵測到頻道繁忙，設備會進入等待狀態，包括一個延遲時間（defer duration）和一個退避期（backoff period）。退避期內，設備會隨機選擇一個額外的 eCCA 時段再次進行 CCA。
        *   Backoff is within the contention window (W) which is impacted by HARQ
*   Frame Structure Type 3
    *   Frame Structure Type 3 是 LAA 專用的幀結構，旨在使 LTE 信號更類似於 Wi-Fi 突發信號，從而更好地與 Wi-Fi 共存
    *   Frame duration is of 10 ms, and consists of 20 slots
        *   (幀長度為 10 毫秒，由 20 個時隙（slot）組成)
    *   Each slot duration is 0.5 ms, and each two adjacent slots form one subframe
        *   每個時隙長度為 0.5 毫秒，每兩個相鄰時隙組成一個子幀（subframe）
    *   Any subframe may be available for DL transmission
        *   任何子幀都可以用於下行傳輸（DL transmission）
    *   The transmission may or may not start at the boundary of the subframe, and it may or may not end at the boundary of the subframe
        *   傳輸可以不必在子幀的邊界開始或結束，這使得 LTE 信號更接近 Wi-Fi 的突發模式
*   Based on the evaluation results provided by Qualcomm, when an operator switches from WiFi to LAA, the throughput for this operator increases by 100%, and even the throughput for the WiFi operators increases by approximately 10%
    *   **根據 Qualcomm 的評估結果：**
    *   當運營商從 Wi-Fi 切換到 LAA 時，其吞吐量可以提高 100%。
    *   甚至 Wi-Fi 運營商的吞吐量也能提高約 10%。
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/56c88de6-26f4-42f5-a75c-cc362dec2718/image.png)

> Source: [https://www.sharetechnote.com/html/Handbook\_LTE\_LAA.html](https://www.sharetechnote.com/html/Handbook_LTE_LAA.html)

*   Discontinuous transmission （**不連續傳輸**）
    *   For LAA operation in some geographical regions (e.g. Japan), discontinuous transmission is part of the specification
        *   在某些地區（例如日本），不連續傳輸是 LAA 規範的一部分，旨在進一步降低 LAA 對其他系統的干擾
    *   An eNB can transmit again on the LAA SCell for a maximum duration of 4 ms immediately after sensing the channel to be idle for a sensing interval of 34 µs
        *   **運作方式：**
            *   LAA 基站（eNB）在感知頻道空閒後，可以立即在 LAA SCell 上進行傳輸，但傳輸時間不得超過4 毫秒。
            *   每次傳輸之間至少要進行 34 微秒的頻道感知。
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/36c22f6d-1c21-4fbc-88fc-7b37fea94fcd/image.png)
*   Frame Structure (**幀結構**)
    *   LTE technology works in a synchronous manner, in which data transmissions are aligned among cells, while LBT procedure of the LAA may be completed at any time instant
    *   Therefore, the channel access time of an LAA cell is generally not aligned with the LTE subframe boundary, which appears every 1 ms
        *   LTE 技術採用同步傳輸方式，所有基站的傳輸是對齊的。
        *   LAA 的 LBT 機制則可能在任意時間完成，導致 LAA 基站的傳輸時間可能無法與 LTE 的子幀邊界（每 1 毫秒出現一次）對齊
    *   Since the transmission opportunity can be taken by any other contender, while the LAA eNB is waiting for the coming subframe boundary, a reservation signal is necessary to fill the gap (由於傳輸機會可以被任何其他競爭者佔用，因此當 LAA eNB 等待即將到來的子幀邊界時，需要保留訊號來填充間隙)
    *   However, reservation signals contain no information bits, and thus waste time resources and incur additional signal overhead (然而，預留訊號不包含資訊位元，因此浪費時間資源並產生額外的訊號開銷)
    *   To efficiently utilize radio resources and alleviate the reservation signal overhead, LAA adopts the concept of a partial subframe. including an initial partial subframe and an ending partial subframe (為了有效利用無線資源並減輕預留訊號開銷，LAA採用部分子幀的概念。 包括初始部分子幀和結束部分子幀)
    *   The initial partial subframe with length of 1/2 the normal subframe can start transmission in the middle of an LTE subframe (長度為正常子訊框1/2的初始部分子訊框可以在LTE子訊框的中間開始傳輸)
    *   The ending partial subframe can be transmitted to make the most use of the MCOT, whose length can be chosen among {3, 6, 9, 10, 11, 12} orthogonal frequency-division multiple access (OFDMA) symbols. It is used when there is not enough time to transmit a full subframe comprising 14 OFDMA symbols (可以發送結束部分子訊框以充分利用MCOT，其長度可以在{3,6,9,10,11,12}個正交頻分多址(OFDMA)符號中選擇。 當沒有足夠的時間來傳送包含 14 個 OFDMA 符號的完整子訊框時使用)
        *   **解決方案：**
        *   **部分子幀（Partial Subframe）：** LAA 引入部分子幀的概念，包括初始部分子幀(initial partial)和結束部分子幀(ending partial subframe)，以更有效地利用頻道資源。
            *   初始部分子幀的長度為正常子幀的一半，可以在 LTE 子幀的中間開始傳輸。
            *   結束部分子幀的長度可以選擇 3、6、9、10、11 或 12 個 OFDMA 符號，以充分利用 MCOT。當沒有足夠時間傳輸完整的子幀（14 個 OFDMA 符號）時，會使用結束部分子幀。
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/e124261e-4264-4186-beb6-93db16739d05/image.png)
*   2 transmission modes defined in Rel. 13
    *   For transmissions on the physical downlink shared channel (PDSCH)
        *   The procedure is shown on the righthand side
    *   Transmitting a discovery reference signal (DRS) without the PDSCH
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/e25be893-1b91-4b8b-804a-5b975d3ff0e9/image.png)
*   Details of channel sensing for transmitting PDSCH
    *   The eNB starts sensing the channel for a period called defer duration time (Td ), and then selects a random number (N) that is uniformly distributed between 0 and CW
    *   The eNB senses the channel for an additional period of (N+1) slot durations (each slot is 9 µs)
    *   If the channel is found to be idle during Td and (N+1) slot duration, the eNB can start transmitting \[duration is within 2 ms and 10 ms\]
    *   If the channel is found busy during any time slot, the eNB continues sensing the channel for an additional defer duration time Td
    *   Td consists of a duration Tf that equals to 16 µs, followed immediately by some (ranges between 1 and 7) additional slot durations
    1. **傳輸物理下行共享信道（PDSCH）：**
        *   基站（eNB）首先進行頻道感知，包括：
            *   延遲時間（Td）：固定時間，由 16 微秒（Tf）加上 1 至 7 個額外的時隙（slot）組成。
            *   退避期（backoff）：隨機選取一個 0 至 CW 之間的整數 N，並額外感知 N + 1 個時隙（每個時隙 9 微秒）。
        *   若頻道在整個感知期間都空閒，eNB 即可開始傳輸 PDSCH，傳輸時間為 2 至 10 毫秒。
        *   若頻道在任何時隙被偵測為繁忙，eNB 則需要重新進行頻道感知。
*   Details of channel sensing for transmitting DRS
    *   The eNB senses the channel for a period of 25 µs
    *   If the channel is found to be idle for the entire period, the eNB can transmit a discovery signal for a max period of 1 ms
    *   Information carried is primary synchronization signal (PSS), secondary synchronization signal (SSS), and cell-specific reference signal (CRS)
    1. **傳輸發現參考信號（DRS）：**
        *   eNB 進行 25 微秒的頻道感知。
        *   若頻道空閒，eNB 即可傳輸 DRS，最長傳輸時間為 1 毫秒。
        *   DRS 攜帶的主要信息包括：
            *   主同步信號（PSS）
            *   次同步信號（SSS）
            *   小區特定參考信號（CRS）

LAA 的兩種傳輸模式都採用 LBT 機制，以確保在未授權頻段中與其他系統共存。

PDSCH 傳輸模式用於傳輸數據，而 DRS 傳輸模式用於小區發現和同步



# LBT Variation

*   According to 3GPP TR 36.889, two different channel access schemes are considered for LAA, i.e., LBT with random backoff in a fixed CW (named fixed CW, FCW), and LBT with random backoff in an exponentially increasing CW (named variable CW, VCW)
*   **LAA 中的 LBT 變化**
    *   根據 3GPP TR 36.889，LAA 考慮了兩種不同的頻道接入方案：
*   LBT with FCW
    *   A LAA-eNB senses the unlicensed band for a predefined period, termed channel clear access (CCA) whenever it has packets to transmit
    *   If the channel is free over CCA, the LAA-eNB sets an integer bacloff timer randomly and uniformly within a fixed CW \[0, WL ), where WL is the initial CW size
    *   The backoff timer counts down one per time slot. It freezes if the channel is busy, and does not resume until the channel is sensed free for CCA again
    *   Once the backoff timer turns to zero, a (re)transmission is trigger
    *   If the (re)transmission is collided (i.e., no ACK is returned), the LAAeNB resets the backoff timer within \[0, WL ) to retransmit the packet
    1. **固定競爭窗口（FCW）的 LBT：**
        *   LAA-eNB 在有數據要傳輸時，會先進行一段預定的頻道清空接入（CCA）感知。
        *   若頻道在 CCA 期間空閒，LAA-eNB 會在固定的競爭窗口 \[0, WL) 內隨機選取一個整數作為退避計時器的值，WL 是初始競爭窗口大小。
        *   退避計時器每個時隙倒數一次，如果頻道繁忙則凍結，直到頻道再次空閒才繼續。
        *   計時器歸零時，進行（重新）傳輸。
        *   如果（重新）傳輸發生碰撞（即沒有收到 ACK），LAA-eNB 會在 \[0, WL) 內重新設定退避計時器，以重傳數據包。

> \[3\] Qimei Cui, et al., “Effective Capacity of Licensed-Assisted Access in Unlicensed Spectrum for 5G: From Theory to Application,” IEEE JSAC, Vol. 35, No. 8, Aug. 2017, pp. 1754-1767.

*   LBT with VCW
    *   Exponential backoff is adopted on top of FCW, where CW doubles each time the (re)transmission of the LAA-eNB is collided
    *   KL is the max number of retransmission per packet, after which the CW is reset to WL
    *   The LAA-eNB resets the CW to WL after a collision-free (re)transmission
    *   Since the LAA-eNB can exploit OFDMA to multiplex signals for multiple LAA-UEs, it’s possible that only some of the LAA-UEs succeed and return ACKs after a collision-free (re)transmission. In such a case, the LAA-eNB still resets the CW to WL even only receives one ACK
    1. **變競爭窗口（VCW）的 LBT：**
        *   在 FCW 的基礎上採用指數退避（Exponential Backoff），即每次 LAA-eNB 的（重新）傳輸發生碰撞時，競爭窗口 CW 就會加倍。
        *   KL 是每個數據包的最大重傳次數，超過 KL 後 CW 會重置為 WL。
        *   在一次無碰撞的（重新）傳輸後，LAA-eNB 會將 CW 重置為 WL。
        *   由於 LAA-eNB 可以利用 OFDMA 為多個 LAA-UE 多路復用信號，因此在無碰撞的（重新）傳輸後，可能只有部分 LAA-UE 成功並返回 ACK。在這種情況下，即使只收到一個 ACK，LAA-eNB 仍然會將 CW 重置為 WL。
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/51722e0c-cd26-46f8-ac2d-069825016747/image.png)

FCW 和 VCW 是 LBT 的兩種變化形式，用於在未授權頻段中協調 LAA 與其他系統的頻道接入。VCW 通過指數退避機制，在發生碰撞時增加競爭窗口，可以有效降低碰撞概率，提升頻道利用率

# LTE-WLAN Aggregation (LWA)

*   LWA supports link aggregation at the packet data control protocol (PDCP) layer （LWA 支援分組資料控制協定 (PDCP) 層的連結聚合）
*   In DL transmission, PDCP packet data units (PDUs) of the same IP flow can be independently routed by the LTE eNB through the LTE and WiFi links 22 （在DL傳輸中，相同IP流的PDCP分組資料單元(PDU)可以由LTE eNB透過LTE和WiFi連結獨立路由22）
*   Xw interface between LTE and WLAN is used to route PDCP PDUs to WiFi APs （LTE 和 WLAN 之間的 Xw 介面用於將 PDCP PDU 路由到 WiFi AP）
*   Xw interface is terminated at the WLAN termination, a 3GPP logical node, which may be in control of one or more WiFi APs and provides seamless mobility among WiFi APs （Xw 介面終止於 WLAN 終端，它是一個 3GPP 邏輯節點，可控制一個或多個 WiFi AP，並提供 WiFi AP 之間的無縫移動性）
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/fb62f2e0-8a74-4117-bb83-7716b2b6e5e9/image.png)
    *   Header壓縮封包聚合
    *   RLC (Radio Link Control): maintain連線; 跟基地台做association
    *   PDCP往上才是IP
*   A new Ether-type is defined to identify the PDCP PDUs routed over WLAN, which allows the WiFi APs to differentiate LWA traffic from other WLAN traffic （定義了新的以太類型來識別透過 WLAN 路由的 PDCP PDU，這允許 WiFi AP 區分 LWA 流量和其他 WLAN 流量）
*   Software/firmware upgrades of legacy WiFi APs to recognize this new Ether-type are needed to enable LWA operation (需要對傳統 WiFi AP 進行軟體/韌體升級以識別這種新的乙太網路類型，以實現 LWA 操作)
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/42bcf2c7-4b76-4e36-a60a-d95b7e154194/image.png)
*   **LTE-WLAN 聚合（LWA）解釋**
*   **目的：**
    *   LWA 技術旨在將 LTE 和 WLAN（Wi-Fi）兩種無線網路聚合在一起，以提升用戶的整體數據吞吐量和網路體驗。
*   **運作方式:**
    1. **PDCP 層聚合:** LWA 在封包數據控制協議（PDCP）層進行聚合，允許同一 IP 流的 PDCP 封包數據單元（PDUs）在 LTE 和 WLAN 鏈路上獨立傳輸。
    2. **Xw 介面:** LTE 基站（eNB）和 WLAN 存取點（AP）之間使用 Xw 介面來傳遞 PDCP 封包。
    3. **WLAN 終端（WT）:** Xw 介面在 WLAN 終端（WT）處終止。WT 是一個 3GPP 邏輯節點，負責控制一個或多個 WLAN AP，並提供 AP 之間的無縫移動性。
    4. **新 Ether-type:** 定義了一種新的 Ether-type 來識別透過 WLAN 傳輸的 PDCP 封包，允許 WLAN AP 區分 LWA 流量和其他 WLAN 流量。
    5. **軟體升級:** 現有的 WLAN AP 需要進行軟體或韌體升級，以支援新的 Ether-type 並啟用 LWA 功能。

# LTE-WLAN radio level integration with IPsec tunnel (LWIP)

*   LWIP provides a more universal solution to access the unlicensed band, realized via legacy WiFi APs (no new Ether-type needed) (LWIP 提供了一種更通用的解決方案來存取免許可頻段，透過傳統 WiFi AP 實現（無需​​新的乙太網路類型）)
*   LWIP supports link switching of IP flows at the IP layer (LWIP支援IP層IP流的鏈路交換)
*   IP data is tunneled from the LTE eNB to UE transparently over legacy WiFi APs relaying via an LWIP-security gateway (SeGW) introduced between the LTE eNB and UE（IP 資料透過傳統 WiFi AP 透明地從 LTE eNB 傳輸到 UE，並透過 LTE eNB 和 UE 之間引入的 LWIP 安全閘道 (SeGW) 進行中繼）
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/326f8c00-ea90-4739-a2fa-c0dc6bf51316/image.png)
*   IP packets, transmitted between the LWIP-SeGW and the UE, are encapsulated with IPsec (LWIP-SeGW和UE之間傳輸的IP資料包採用IPsec封裝)
*   The path between LWIP-SeGW and UE is called an IPsec tunnel (LWIP-SeGW和UE之間的路徑稱為IPsec隧道)
*   IP packets of a data flow can be transmitted through either an LTE or a WiFi link (never over both) (資料流的 IP 資料包可以透過 LTE 或 WiFi 連結傳輸（不能同時透過兩者）)
    *   Reason: TCP cannot cope with the out-of-order delivery of packets transmitted over two radio interfaces (TCP 無法處理透過兩個無線電介面傳輸的資料包的無序傳送)
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/765e6899-08eb-4913-a557-7661268535fd/image.png)
    *   **LTE-WLAN 無線電層整合 IPsec 通道（LWIP）解釋**
    *   **目的：**
        *   LWIP 提供一種更通用的解決方案，通過現有的 WLAN AP 來接入未授權頻段，而不需要新的 Ether-type。
    *   **運作方式：**
        1. **IP 層鏈路切換：** LWIP 在 IP 層支持 IP 流的鏈路切換，允許 IP 流在 LTE 和 WLAN 鏈路之間切換。
        2. **IPsec 通道：** 引入了一個 LWIP 安全閘道（SeGW），位於 LTE eNB 和 UE 之間。IP 數據在 LTE eNB 和 UE 之間通過現有的 WLAN AP 進行透明傳輸，並在 LWIP-SeGW 和 UE 之間使用 IPsec 進行封裝。
        3. **鏈路選擇：** 同一 IP 流的 IP 封包只能通過 LTE 或 WLAN 鏈路中的一條進行傳輸，而不會同時在兩條鏈路上傳輸。這是因為 TCP 協議無法處理在兩個無線電介面上傳輸的封包的亂序交付問題。
    *   **優勢：**
        *   不需要對現有的 WLAN AP 進行升級。
        *   可以利用現有的 WLAN 基礎設施。
        *   提供 IP 層的靈活性。
        *   可保護用戶隱私和安全。

# WiFi 7 Multi-Link Operation

*   Modern off-the-shelf APs support dual- or tri-band operations. However, the WiFi MAC and PHY of various bands work almost independently, and provide multiple independent links to STAs (現代現成的 AP 支援雙頻或三頻操作。 但各個頻段的WiFi MAC和PHY幾乎是獨立運作，為STA提供多個獨立的連結)
*   Still one MAC address, while has multiple PHY interfaces (仍然是一個MAC位址，同時具有多個PHY介面)
*   Restricted mode v.s. dynamic link switch
    *   Restricted: data & ACK on one link; management on another link (一條鏈路上的資料和 ACK； 在另一個連結上進行管理)
    *   Dynamic link switch: multiple links can be used for transmission of the same flow; management information and negotiation sent over another link (可使用多條連結傳輸相同流量； 透過另一個連結發送的管理訊息和協商)
        *   Load balancing can be enabled (可以啟用負載平衡)
*   Multi-link channel access is an issue (多鏈路通道存取是個問題)
*   Asynchronous v.s. synchronous multi-link operations
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/bed1dd79-0a2c-499a-b6f6-f227abfcdf6f/image.png)



*   Duplicate v.s. joint mode
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/df0ac8e1-c78b-4941-ad1a-557210a5deea/image.png)

**WiFi 7 多鏈路操作（Multi-Link Operation）解釋**

**目的：**

WiFi 7 的多鏈路操作旨在提升無線網路的吞吐量、可靠性和延遲，以滿足日益增長的數據需求。它允許在多個頻段上同時傳輸數據，以充分利用可用的頻譜資源。

**運作方式:**

1. **MAC 地址與 PHY 介面：** WiFi 7 AP 保留一個 MAC 地址，但具有多個 PHY 介面，可以同時在多個頻段上運行。
    *   **受限模式與動態鏈路切換：**受限模式：數據和 ACK 在一個鏈路上傳輸，管理信息在另一個鏈路上傳輸。
    *   動態鏈路切換：允許同一個數據流在多個鏈路上傳輸，管理信息和協商在另一個鏈路上進行。
2. **負載平衡：** 可以根據各個頻段的擁塞情況，動態分配流量，以達到負載平衡。
3. **多鏈路信道接入：** 多個鏈路如何協調信道接入，以避免碰撞和干擾，是需要解決的關鍵問題。

**模式分類：**

*       *   **異步與同步：**
        *   異步：各個鏈路獨立傳輸數據，不需要精確同步。
        *   同步：各個鏈路協同傳輸數據，需要精確同步。
*       *   **重複與聯合：**
        *   重複模式：在多個鏈路上傳輸相同的數據，以提高可靠性。
        *   聯合模式：將數據分割成多個部分，在多個鏈路上同時傳輸，以提升吞吐量。

**優勢：**

*   提升吞吐量：充分利用多個頻段的頻寬。
*   降低延遲：多個鏈路同時傳輸，減少排隊等待時間。
*   提高可靠性：重複傳輸或聯合傳輸可以降低誤碼率。
*   增強靈活性：根據環境和需求動態調整鏈路配置。



# Supplementary-LTE TDD Frame Structure

![](https://t3764800.p.clickup-attachments.com/t3764800/63c84df4-466e-40d0-9982-55523ea34ec6/image.png)
