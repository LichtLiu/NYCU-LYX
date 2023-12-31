---
title: "Wireless-Multimedia-Network"
permalink: /Wireless-Multimedia-Network/1-Introduction-&-Review-of-the-cellular-networks/
layout: default
---
# Lecture 1 - Introduction & Review of the cellular networks

![](https://t3764800.p.clickup-attachments.com/t3764800/4d8ce3b1-3a4a-4f24-8c7c-67944295b48f/Screen%20Shot%202023-09-14%20at%206.56.53%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/d26ed73c-6688-430c-b0cc-d22a07d02b8d/Screen%20Shot%202023-09-14%20at%206.57.02%20PM.png)

*   /LTE-A 的峰值下行速率為 1Gbps,上行速率為 500Mbps。
*   5G 的設計峰值數據速率根據 IMT-2020 要求可達到 20Gbps。
*   IMT-2020 是國際電信聯盟在 2015 年提出的移動通信標準。我們需要新技術來支持未來的移動流量增長。按照預測,到 2022 年移動流量將達到每月 1 EB。

這張圖顯示了全球移動數據流量的增長趨勢。從 2016 年到 2021 年，全球移動數據流量從 11EB 增長到 49EB，增長了 7 倍。這一增長是由於以下因素造成的：

*   移動設備的普及：隨著智能手機和平板電腦的普及，越來越多的人使用移動設備來訪問互聯網。
*   移動數據應用的增長：移動數據應用的增長，如視頻流媒體、社交媒體和遊戲，也導致了移動數據流量的增加。

圖表中顯示了移動數據流量的複合年增長率 (CAGR) 為 47%。這意味著移動數據流量在未來幾年仍將繼續增長。

圖表的右下角有一個觀察：我們需要新的技術來支持即將到來的移動流量。這一觀察是基於移動數據流量增長速度的預期。隨著移動數據流量的增加，現有的移動網絡可能無法滿足需求。因此，需要新的技術來提高移動網絡的容量和性能。

以下是一些可能用於支持即將到來的移動流量的新技術：

*   5G：5G 是一種新的移動通信標準，可提供比 4G LTE 更高的速度和容量。
*   光纖到用戶：光纖到用戶 (FTTP) 是一種將光纖連接直接到用戶的技術。FTTP 可提供比傳統的銅線接入更高的速度和可靠性。
*   雲計算：雲計算可用於將移動數據流量從移動網絡轉移到雲端。這可以幫助釋放移動網絡的容量。

這些技術仍在開發中，但它們有可能在未來幾年內實現。



![](https://t3764800.p.clickup-attachments.com/t3764800/3a069338-8947-4653-84da-0cea06fe2e04/Screen%20Shot%202023-09-14%20at%206.57.11%20PM.png)

*   WiFi正變得越來越重要,主要是因為成本問題和覆蓋問題。
*   WiFi無需許可證頻段,部署網絡的成本較低。同時WiFi也可以彌補行動網絡在某些區域的覆蓋不足。
*   為了支援日益增長的流量需求,未來的移動網絡將朝著異構網絡(Heterogeneous network)方向發展。
*   異構網絡指同時使用多種無線接入技術的網絡,如4G、5G、WiFi等。每種技術都有自己的優勢,組合使用可以發揮不同技術的優勢。
*   CISCO、Ericsson等公司預測到2020年會有超過200億個終端設備連接到網絡,為這些設備提供連接是一大挑戰。
*   視頻、社交、音頻等應用的流量增長最快,這需要新技術來支持。



offload traffic 通常是指將流量從移動網絡轉移到其他網絡，如 Wi-Fi 或固定寬頻網絡。

offload traffic 有以下幾個目的：

*   釋放移動網絡的容量：隨著移動數據流量的增長，移動網絡的容量可能會不足以滿足需求。offload traffic 可以幫助釋放移動網絡的容量，從而提高移動網絡的性能。
*   提高移動網絡的性能：offload traffic 可以將流量從移動網絡轉移到其他網絡，這些網絡可能具有更高的速度和容量。這可以提高移動網絡的性能，從而為用戶提供更好的體驗。
*   降低移動網絡的成本：offload traffic 可以將流量從移動網絡轉移到其他網絡，這些網絡可能具有更低的成本。這可以降低移動網絡的成本，從而提高移動網絡的盈利能力。

offload traffic 的技術有很多種，包括：

*   **Wi-Fi offloading**：將流量從移動網絡轉移到 Wi-Fi 網絡。
*   **fixed broadband offloading**：將流量從移動網絡轉移到固定寬頻網絡。
*   **edge computing**：將流量從移動網絡轉移到邊緣計算節點。
*   **cloud computing**：將流量從移動網絡轉移到雲端。





Heterogeneous network (HetNet) 是指由不同類型的網絡組成的移動網絡。HetNet 通常由蜂窩網絡、Wi-Fi 網絡、固定寬頻網絡等組成。

Offload traffic 是將流量從一個位置轉移到另一個位置。在 HetNet 中，offload traffic 可以將流量從蜂窩網絡轉移到其他網絡，如 Wi-Fi 網絡或固定寬頻網絡。

HetNet 與 offload traffic 有以下幾個關係：

*   **HetNet 為 offload traffic 提供了基礎**：HetNet 由不同類型的網絡組成，這為 offload traffic 提供了基礎。移動網絡可以將流量轉移到其他網絡，從而釋放移動網絡的容量和提高移動網絡的性能。
*   **Offload traffic 可以提高 HetNet 的性能**：Offload traffic 可以將流量從移動網絡轉移到其他網絡，這些網絡可能具有更高的速度和容量。這可以提高 HetNet 的性能，從而為用戶提供更好的體驗。

以下是一些 HetNet 中 offload traffic 的示例：

*   **Wi-Fi offloading**：在室內，移動設備可以使用 Wi-Fi 網絡來訪問互聯網。這可以將流量從蜂窩網絡轉移到 Wi-Fi 網絡，從而釋放蜂窩網絡的容量。
*   **fixed broadband offloading**：在室外，移動設備可以使用固定寬頻網絡來訪問互聯網。這可以將流量從蜂窩網絡轉移到固定寬頻網絡，從而提高蜂窩網絡的性能。
*   **edge computing offloading**：在邊緣計算節點上，移動設備可以處理一些計算密集型應用。這可以將流量從移動網絡轉移到邊緣計算節點，從而降低蜂窩網絡的負載。
*   **cloud computing offloading**：在雲端，移動設備可以處理一些數據密集型應用。這可以將流量從移動網絡轉移到雲端，從而提高蜂窩網絡的性能。

總體而言，HetNet 與 offload traffic 是相輔相成的。HetNet 為 offload traffic 提供了基礎，而 offload traffic 可以提高 HetNet 的性能。







請讓我知道如果需要補充或擴展說明。

![](https://t3764800.p.clickup-attachments.com/t3764800/760ee0a7-7ad3-4bb8-9e8d-5ccd55cc06f9/Screen%20Shot%202023-09-14%20at%206.57.20%20PM.png)

*   CISCO、Ericsson等公司預測到2020年會有超過200億個終端設備連接到網絡,為這些設備提供連接是一大挑戰。



M2M 指機器對機器通信(Machine to Machine Communications)。它的關鍵特征是:

*   M2M 指無人參與的設備或傳感器之間的自動通信。
*   通過嵌入式傳感器和通信模塊,M2M 設備可以互相連接,無需人為干預。
*   應用示例包括遠程資產和裝置監控,自動報表和數據捕獲,無人機及機器人的遠程操作等。
*   M2M 技術應用於工業、交通、健康护理、公用事業等多個領域。
*   M2M 通信可以是有線的,也可以是無線的,如蜂窩Cellular網絡、衛星網絡、WiFi等。
*   隨著物聯網的發展,预计到2020年會有上百億的 M2M 連接。
*   M2M 是支援大規模物聯網連接的重要技術,是 5G 網絡的一大應用場景。

M2M 是一種自主設備間的智能互聯技術,被廣泛應用於各行各業,是物聯網的基礎。



![](https://t3764800.p.clickup-attachments.com/t3764800/0c6f53b9-0444-4bd1-beff-d6c2cd545361/Screen%20Shot%202023-09-14%20at%206.57.48%20PM.png)

social media網路成長的使用率變高（不一定跟娛樂有關，有可能是交通上攝影上，智慧醫療 等等），audio減少



![](https://t3764800.p.clickup-attachments.com/t3764800/7a15bb77-e66c-436d-8391-c92306a293d3/Screen%20Shot%202023-09-14%20at%207.00.47%20PM.png)

*   基地台細胞變小，離基地台越近訊號越好
*   Multi-Ran 各種服務 (heterogeneous network)
*   wifi不需要跟國家申請頻寬，想多大就多大
*   3GPP訂定LTE-U: LTE-LAA



**1\. RAT Revolution**

RAT Revolution 是指無線接入技術的革命性變革。隨著新一代無線接入技術的不斷發展，如 5G、Wi-Fi 6 和 6E，用戶將能夠享受到更快、更可靠、更具擴展性的無線連接。

**2\. Cell Shrinking**

Cell Shrinking 是指蜂窩網絡小區的縮小。隨著移動數據流量需求的不斷增長，移動運營商需要在城市和人口密集的地區部署更多小區，以提高容量和性能。

**3\. Composite wireless infrastructure**

Composite wireless infrastructure 是指由多種不同類型的無線網絡組成的無線網絡。這些網絡可以包括蜂窩網絡、Wi-Fi 網絡和固定寬頻網絡。複合無線基礎設施旨在為用戶提供無縫和可靠的無線連接，無論他們的位置或使用的設備類型。

**4\. Heterogeneous Network**

Heterogeneous Network 是指由不同類型和頻率的無線網絡組成的網絡。這些網絡可以包括蜂窩網絡、Wi-Fi 網絡和固定寬頻網絡。Heterogeneous Network 旨在為用戶提供最佳的無線體驗，無論他們的位置或使用的設備類型。

**5\. Flexible Spectrum Management**

Flexible Spectrum Management 是指無線頻譜的靈活管理。隨著無線數據流量需求的不斷增長，移動運營商需要能夠靈活地利用無線頻譜，以滿足不斷變化的需求。

**6\. Exploiting Cloud Concept**

Exploiting Cloud Concept 是指利用雲計算的概念。雲計算可以用來部署和管理無線網絡基礎設施，從而提高效率和降低成本。

**7\. Introduction of Intelligence**

Introduction of Intelligence 是指人工智能技術在無線網絡中的應用。人工智能可以用來提高無線網絡的性能和可靠性，以及提供更加個性化的用戶體驗。

以下是對上述概念的具體應用：

*   **RAT Revolution**：5G 網絡的部署將為用戶帶來更快、更可靠、更具擴展性的無線連接。
*   **Cell Shrinking**：小區的縮小將有助於提高蜂窩網絡的容量和性能。
*   **Composite wireless infrastructure**：複合無線基礎設施將為用戶提供無縫和可靠的無線連接。
*   **Heterogeneous Network**：Heterogeneous Network 將為用戶提供最佳的無線體驗。
*   **Flexible Spectrum Management**：靈活的頻譜管理將有助於滿足不斷變化的無線數據流量需求。
*   **Exploiting Cloud Concept**：雲計算將有助於提高無線網絡的效率和降低成本。
*   **Introduction of Intelligence**：人工智能將有助於提高無線網絡的性能和可靠性，以及提供更加個性化的用戶體驗。

這些概念將共同推動用戶連網的發展，為用戶提供更加優質的無線體驗。





這張圖顯示了一個小蜂窩網絡Cellular network (SCN-small cell network) 的示例，其中包括一個小蜂窩基站 (SBS) 和一個雲端控制器。SBS 是 SCN 的邊緣節點，負責與移動設備進行通信。雲端控制器是 SCN 的中央節點，負責管理 SBS 和其他 SCN 資源。

圖中的文字說明了 SCN 的一些關鍵特點：

*   \*\*小尺寸：\*\*SCN 的大小通常小於傳統的Cellular網絡。這使得它們更容易部署在室內和人口密集的地區。
*   \*\*高密度：\*\*SCN 可以部署得更密集，從而提高容量和性能。
*   \*\*邊緣計算：\*\*SCN 可以利用邊緣計算來將一些計算密集型任務從雲端移到 SBS。這可以提高性能和降低延遲。
*   \*\*靈活性：\*\*SCN 可以根據需求進行靈活部署。這使得它們適合多種應用，如室內覆蓋、熱點擴展和工業物聯網。

圖中還顯示了 SCN 的一些可能的應用：

*   \*\*室內覆蓋：\*\*SCN 可以用來改善室內覆蓋，尤其是在建築物和其他室內環境中。
*   \*\*熱點擴展：\*\*SCN 可以用來擴展現有的蜂窩網絡熱點，從而提高容量和性能。
*   \*\*工業物聯網：\*\*SCN 可以用來支持工業物聯網應用，如機器對機器 (M2M) 通信和遠程監控。

總體而言，SCN 是一種新的移動網絡架構，具有小尺寸、高密度、邊緣計算和靈活性等優點。它們可以用於多種應用，如室內覆蓋、熱點擴展和工業物聯網。



![](https://t3764800.p.clickup-attachments.com/t3764800/775fafb5-023a-4f41-b678-35bd62a71a66/Screen%20Shot%202023-09-14%20at%207.10.17%20PM.png)



中間的wifi受到3GPP訂定LTE-U: LTE-LAA 規範

![](https://t3764800.p.clickup-attachments.com/t3764800/9f02c94d-bef4-4f19-8a15-ea7a152ae12b/Screen%20Shot%202023-09-14%20at%207.08.41%20PM.png)

工研院設計全光交換器，與日本COSMOS簽合約測試

*   edge computing 比如路燈可以給經過的汽車回傳資料
*   SDN & NFV 只要更新硬體，就能直接將新的功能或演算法deploy到硬體上
*   Network slicing 切頻寬 end-to-end
*   Internet QoS (Quality of Service) => 一般人看不懂所以變成利用QoE 評分 Quality of experience (_QoE_) is a measure of the delight or annoyance of a customer's experiences with a service
*   Massive MIMO 多天線 _Massive MIMO_波束成形是實現5G信號的先進技術，能夠極大擴展網絡容量。透過此項技術可大幅提高每個用戶的峰值數據速率和吞吐量，達到10Gbps的連接速度。channel state information （通道資訊）傳送，如果是正交，就是不同的資料



*   **Cloud/edge computing**：雲端計算和邊緣計算是兩種不同的計算架構。雲端計算將計算能力集中在雲端，而邊緣計算將計算能力部署到靠近用戶的邊緣。
*   **SDN & NFV**：SDN（軟體定義網路）和NFV（網路功能虛擬化）是兩種網路技術，可以用來提高網路的靈活性和效率。SDN 將網路控制層從網路硬體中分離出來，而 NFV 將網路功能虛擬化到軟體中。
*   **Network slicing**：網路切片是一種將網路資源劃分為邏輯子網的技術。網路切片可以用來為不同類型的用戶或應用提供定制的服務。
*   **Service-oriented cloud**：服務導向雲是一種將雲端服務作為服務提供的架構。服務導向雲可以用來簡化雲端部署和管理。
*   **Internet QoS**：Internet QoS（互聯網質量服務）是指對互聯網流量進行優先級排序的技術。Internet QoS 可以用來確保關鍵應用獲得足夠的帶寬和資源。
*   **Resource management**：資源管理是指對網路資源進行分配和使用的技術。資源管理可以用來提高網路的效率和性能。
*   **Massive MIMO**：Massive MIMO（大規模天線陣列）是一種使用大量天線來提高無線通信性能的技術。Massive MIMO 可以用來提高無線網絡的容量和可靠性。
*   **COMP (Coordinated Multi-Point Transmission)**：COMP（協調多點傳輸）是一種利用多個天線同時發送數據的技術。COMP 可以用來提高無線網絡的容量和性能。
*   **Beamforming technology**：Beamforming 是一種將無線信號集中到特定方向的技術。Beamforming 可以用來提高無線網絡的容量和可靠性。



[clouds.blogspot.com/2018/02/lte-beamforming-precoding-1.html](http://clouds.blogspot.com/2018/02/lte-beamforming-precoding-1.html)

![](https://t3764800.p.clickup-attachments.com/t3764800/7f89dc88-49cf-436d-864b-52ce7d41f935/Screen%20Shot%202023-09-14%20at%207.37.56%20PM.png)



*   頻率越高，服務的越多





![](https://t3764800.p.clickup-attachments.com/t3764800/ddf755f4-fa79-4996-a302-39b2c450ea96/Screen%20Shot%202023-09-14%20at%208.03.55%20PM.png)

*   GSM是2G行動通信的主要標準,提供了數字語音服務。
*   圖中顯示了GSM的基本網路架構,包含了移動台(MS)、基地台(BTS)、基地台控制器(BSC)和網路交換系統(NSS)。
*   移動台指的是用戶的手機設備。基地台負責與移動台的無線通信。
*   基地台控制器控制多個基地台,管理無線資源及手機切換。
*   網路交換系統則包含了移動服務交換中心(MSC)、家鄉註冊器(HLR)、訪客註冊器(VLR)等,提供調用控制和用戶數據的管理。
*   MSC提供調用建立、維護和切換功能。HLR存儲用戶資料。VLR在用戶漫遊時暫存數據。
*   這個架構實現了GSM的全數字語音服務和基本數據服務。



*   AUC(Authentication Center): AUC負責GSM系統的身份鑒別和加密功能。它保存著每個用戶的鑒別和加密密鑰信息,並進行密鑰管理。
*   EIR(Equipment Identity Register): EIR是存儲移動設備身份信息的數據庫。它保存合法移動設備的識別碼,並管理設備黑名單以防止被盜設備接入。EIR 傳遞手機ID 電信業者會紀錄
*   GMSC (Gateway MSC): GMSC作為閘道交換中心,負責GSM網與固網PSTN之間的互連。它支持用戶在GSM網和固網之間漫遊。
*   PSTN (Public Switched Telephone Network): PSTN指公共交換電話網,也就是傳統的固定電話網。GSM網通過GMSC與PSTN互連,以實現與固網用戶的調用。
*   HLR是註冊在當初辦的電信 像戶籍地，假設到國外且電信台有漫遊就會知道你人在哪裡，並且將訊號傳回原電信





BSC控制訊號傳遞的地方

| 2G | MS | BS |
| ---| ---| --- |
| 3G | UE | NodeB |
| 4G | UE | eNB(eNodeB) |
| 5G | UE | gNB |

Core network

BSS沒有資料庫

電腦到AP

![](https://t3764800.p.clickup-attachments.com/t3764800/9287aa5b-ae64-4ea8-829e-c76b3daa2a0b/Screen%20Shot%202023-09-14%20at%208.07.33%20PM.png)

核網有資料庫- 進行身份認證一定會進到核網，到資料庫做深份驗證後資料才會回來

AP到有線

![](https://t3764800.p.clickup-attachments.com/t3764800/42736182-f9ae-4022-953f-5975793b6340/Screen%20Shot%202023-09-14%20at%208.08.03%20PM.png)

MSC交換器 notebook

![](https://t3764800.p.clickup-attachments.com/t3764800/813fac6a-2aff-4cc1-958a-f621b337a642/Screen%20Shot%202023-09-14%20at%208.18.50%20PM.png)

*   SGSN(Serving GPRS Support Node)是GPRS網絡的一個關鍵核心網元件。它負責封包數據在GSM和外部數據網之間的傳輸。
*   GGSN(Gateway GPRS Support Node)作為閘道,負責提供存取外部數據網的連接點。
*   PCU(Packet Control Unit)控制BSC與SGSN之間的PACKET交換。
*   BSC(Base Station Controller)基站控制器，控制和管理其所管轄的多個基地台。它負責無線資源管理、頻率重用、切換以及與MSC間的接口。可分配CS域和PS域,CS域負責語音、PS域負責數據。
*   GTP(GPRS Tunneling Protocol)用於SGSN和GGSN之間建立隧道。
*   HLR提供用戶註冊和數據庫存儲功能。
*   EIR(Equipment Identity Register)用於設備身份鑒別，EIR設備身份寄存器,是一個數據庫,存儲所有合法移動設備的身份識別信息。它可防止被盜設備接入網絡。
*   SMS-IWMSC是短信中心,負責傳遞文字短信。
*   MMS-IWMSC是彩信中心,負責傳遞圖片、視頻等彩信。



![](https://t3764800.p.clickup-attachments.com/t3764800/6ef513a1-305c-47ce-bb47-8fc64018c886/Screen%20Shot%202023-09-14%20at%208.19.07%20PM.png)

移動交換中心(MSC)-

*   交換功能
*   網絡接口
*   共同信道訊號傳輸
*   閘道功能
*   HLR和VLR的維護

基地台控制器(BSC)-

*   管理的基地台之間進行切換
*   信號功率級別管理
*   基地台之間的頻率管理

驗證中心(AUC)-

*   處理驗證和加密
*   處理欺詐和假冒

設備身份寄存器(EIR)-

*   包含有關移動設備身份的資料庫



![](https://t3764800.p.clickup-attachments.com/t3764800/0c781eb2-467c-478d-ab5e-d83586f8d309/Screen%20Shot%202023-09-14%20at%208.19.26%20PM.png)

2G 跟 3G 核網一樣 但基地台不一樣，所以使用者要換手機

上面講電話

下面用網路

Air 是 UMTS 網路的無線接入網路 (RAN) 的一部分。它位於 UMTS 網路的邊緣，負責連接移動用戶和基站。



**_BSC 連到 MSC 和 SGSN 是為了提供以下功能：_**

*   \*\*呼叫控制：\*\*BSC 將呼叫路由到 MSC，MSC 負責管理呼叫的建立、維持和終止。
*   \*\*移動性管理：\*\*BSC 將移動用戶的註冊信息傳遞給 MSC，MSC 負責管理移動用戶的註冊和身份驗證。
*   \*\*數據服務：\*\*BSC 將數據包傳遞給 SGSN，SGSN 負責管理數據包的路由。

具體來說，BSC 通過 A 接口連接到 MSC，通過 Gb 接口連接到 SGSN。

A 接口是一種電路域接口，用於傳輸呼叫控制信令。BSC 使用 A 接口將呼叫路由到 MSC，MSC 負責管理呼叫的建立、維持和終止。

Gb 接口是一種分組域接口，用於傳輸數據包。BSC 使用 Gb 接口將數據包傳遞給 SGSN，SGSN 負責管理數據包的路由。

因此，BSC 連到 MSC 和 SGSN 是為了提供 UMTS 網路的核心功能。





**_RNC 連到 MSC 和 SGSN 是為了提供以下功能：_**

*   \*\*呼叫控制：\*\*RNC 將呼叫路由到 MSC，MSC 負責管理呼叫的建立、維持和終止。
*   \*\*移動性管理：\*\*RNC 將移動用戶的註冊信息傳遞給 MSC，MSC 負責管理移動用戶的註冊和身份驗證。
*   \*\*數據服務：\*\*RNC 將數據包傳遞給 SGSN，SGSN 負責管理數據包的路由。

具體來說，RNC 通過 Iu-CS 接口連接到 MSC，通過 Iu-PS 接口連接到 SGSN。

Iu-CS 接口是一種電路域接口，用於傳輸呼叫控制信令。RNC 使用 Iu-CS 接口將呼叫路由到 MSC，MSC 負責管理呼叫的建立、維持和終止。

Iu-PS 接口是一種分組域接口，用於傳輸數據包。RNC 使用 Iu-PS 接口將數據包傳遞給 SGSN，SGSN 負責管理數據包的路由。

因此，RNC 連到 MSC 和 SGSN 是為了提供 UMTS 網路的核心功能。

此外，RNC 還與其他 RNC 連接，以便管理無線接入網路的資源。RNC 通過 Iub 接口連接到其他 RNC。

Iub 接口是一種無線接入網路接口，用於傳輸無線接入控制信令和用戶數據。RNC 使用 Iub 接口與其他 RNC 交換移動用戶的註冊信息、呼叫控制信令和數據包。

因此，RNC 連接到 MSC、SGSN 和其他 RNC 是為了提供 UMTS 網路的完整功能。



> GMSC (Gateway MSC): GMSC作為閘道交換中心,負責GSM網與固網PSTN之間的互連。它支持用戶在GSM網和固網之間漫遊。



> GGSN(Gateway GPRS Support Node)作為閘道,負責提供存取外部數據網的連接點。



Camel application part 及 Mobile application part ([https://doc.clickup.com/d/h/3jwj0-4202/e104d24a59e91ab](https://doc.clickup.com/d/h/3jwj0-4202/e104d24a59e91ab))





UMTS 是一種移動電信網路，使用蜂窩網路與其他網路進行通訊。蜂窩網路由無線網路連接到蜂窩網路。無線網路由有線網路連接到蜂窩網路。有線網路連接到其他網路，例如固定電話網路和網際網路。

圖片中顯示了 UMTS 網路的各個組件。這些組件包括：

*   行動用戶：移動用戶是使用 UMTS 網路進行通訊的設備。
*   基站：基站是蜂窩網路的基礎設施。它們負責發射和接收無線信號。
*   無線接入網路：無線接入網路是連接移動用戶和基站的網路。它使用無線電波進行通訊。
*   回程網路：回程網路是連接無線接入網路和其他網路的網路。它使用有線電路進行通訊。
*   核心網路：核心網路是 UMTS 網路的控制中心。它負責管理移動用戶的註冊、路由和呼叫控制。核網位於 Backbone 上，但它本身並不是 Backbone。

圖片中顯示了 UMTS 網路的組件如何連接在一起。移動用戶通過無線接入網路連接到基站。基站通過回程網路連接到核心網路。核心網路通過有線網路連接到其他網路。

UMTS 網路是一種複雜的系統，它使移動用戶能夠與其他網路進行通訊。它是當今移動通信的基礎。

以下是圖片中顯示的各個組件的詳細說明：

*   **移動用戶 (MS)**：移動用戶是使用 UMTS 網路進行通訊的設備。它可以是手機、平板電腦或其他行動裝置。
*   **基站 (BS)**：基站是蜂窩網路的基礎設施。它們負責發射和接收無線信號。基站通常位於高處，例如屋頂或電線桿上，以便可以覆蓋更大的區域。
*   **無線接入網路 (RAN)**：無線接入網路是連接移動用戶和基站的網路。它使用無線電波進行通訊。RAN 由基站和無線接入控制器 (RNC) 組成。RNC 負責管理基站和移動用戶之間的通信。
*   **回程網路 (Backbone)**：回程網路是連接無線接入網路和其他網路的網路。它使用有線電路進行通訊。回程網路通常由光纖或銅纜組成。
*   **核心網路 (CN)**：核心網路是 UMTS 網路的控制中心。它負責管理移動用戶的註冊、路由和呼叫控制。CN 由許多不同組件組成，包括：
    *   移動用戶設備 (UE) 控制器：UE 控制器負責管理移動用戶的註冊和身份驗證。
    *   路由控制器：路由控制器負責將呼叫路由到正確的基站。
    *   呼叫控制器：呼叫控制器負責管理呼叫的建立、維持和終止。
    *   其他組件：核心網路還包含許多其他組件，這些組件負責支持 UMTS 網路的各種功能。





![](https://t3764800.p.clickup-attachments.com/t3764800/34bd66ff-b798-4871-97b8-9d028077e387/Screen%20Shot%202023-09-14%20at%208.21.20%20PM.png)



![](https://t3764800.p.clickup-attachments.com/t3764800/05835931-2d24-4a87-9922-4f7e78305035/Screen%20Shot%202023-09-14%20at%208.22.10%20PM.png)

circuit suite以秒計費 （先保留）

通訊變少所以變packet core

Vo-LTE LTE就是packet core 把聲音包成封包（circuit core ➝ packet core）



2G ➝ GSM

3G ➝ UMTS

4G ➝ LTE



各代移動通信網絡架構之間的主要差異：

*   **信號類型：** 1G 和 2G 網絡使用模擬信號，而 3G 網絡、4G 網絡和 5G 網絡使用數位信號。
*   **數據速率：** 1G 網絡的數據速率很低，而 2G 網絡的數據速率有所提高，3G 網絡、4G 網絡和 5G 網絡的數據速率更高。
*   **應用程序支持：** 1G 網絡只能支持語音通信，而 2G 網絡可以支持語音和數據通信，3G 網絡可以支持更豐富的應用程序，例如網上衝浪、電子郵件和視頻流媒體，4G 網絡可以支持更多用戶，5G 網絡可以支持更高的數據速率和更低的延遲。
*   **核心網絡架構：** 在 1G 和 2G 網絡中，核心網絡由固定線路組成，與無線接入網絡分離。在 3G 網絡中，核心網絡開始採用 IP 技術，與無線接入網絡整合。在 4G 網絡中，核心網絡繼續採用 IP 技術，並進一步整合無線接入網絡。在 5G 網絡中，核心網絡採用 SDN 技術，以實現更靈活和可擴展的網絡。





\===================NOT YET======================

![](https://t3764800.p.clickup-attachments.com/t3764800/d0be9c76-f125-4b57-aeb6-aa413abd23c1/Screen%20Shot%202023-09-14%20at%208.27.19%20PM.png)

ePDG ([https://doc.clickup.com/d/h/3jwj0-4222/2b6d783513985da](https://doc.clickup.com/d/h/3jwj0-4222/2b6d783513985da)) 是演進的分組數據網關 (Evolved Packet Data Gateway) 的縮寫。ePDG 是 4G 網路中的一個重要組件，它負責為非 3GPP 接入網 (Non-3GPP Access Network) 中的用戶設備提供安全的連接到 3GPP 核心網 (3GPP Core Network)



3GPP ([https://doc.clickup.com/d/h/3jwj0-4242/43d1308892c4d64](https://doc.clickup.com/d/h/3jwj0-4242/43d1308892c4d64)) 是第三代合作夥伴計劃 (3rd Generation Partnership Project) 的縮寫。3GPP 是一個由移動通信產業公司組成的國際標準組織，負責制定 2G、3G、4G 和 5G 移動通信標準。



GERAN ([https://doc.clickup.com/d/h/3jwj0-4262/2387049bb91a6c5](https://doc.clickup.com/d/h/3jwj0-4262/2387049bb91a6c5)) 是 GSM EDGE Radio Access Network 的縮寫。GERAN 是 GSM 系統的無線接入網 (RAN)，它由基站、天線和其他無線設備組成。基站負責與移動設備進行通信，天線負責發射和接收無線信號。



HSS ([https://doc.clickup.com/d/h/3jwj0-4282/9da24689528e9b9](https://doc.clickup.com/d/h/3jwj0-4282/9da24689528e9b9)) HSS 是 Home Subscriber Server 的縮寫，是移動通信網路的一個重要組件，它負責存儲和管理用戶的數據和信息。HSS 是 GSM、UMTS、LTE 和 5G 等移動通信系統的核心組件。

PCRF ([https://doc.clickup.com/d/h/3jwj0-4302/ebd7a5ae9c5cabb](https://doc.clickup.com/d/h/3jwj0-4302/ebd7a5ae9c5cabb)) 是 Policy and Charging Rules Function 的縮寫，是移動通信網路的一個重要組件，它負責策略控制和計費控制。PCRF 是 3GPP 定義的，是 LTE 和 5G 網路的核心組件。



MSC➝Serving GW

VLR、HLR➝HSS

MME 總管找HSS驗證使用者後 叫 eNB件tunnel

PCRF累加使用量![](https://t3764800.p.clickup-attachments.com/t3764800/1ec425ec-0d00-4d5e-91b7-049ba7884a37/Screen%20Shot%202023-09-14%20at%208.32.45%20PM.png)



RAN = UE + E-UTRAN Node B (eNB)



E-UTRAN Node B (eNB) ([https://doc.clickup.com/d/h/3jwj0-4322/e1a8148f0c42bca](https://doc.clickup.com/d/h/3jwj0-4322/e1a8148f0c42bca))是 4G LTE 網路的無線接入網 (RAN) 組件，也被稱為 LTE 基站。eNB 負責與移動設備進行通信，並提供 LTE 網路的所有服務，包括語音通話、短信和數據傳輸。



LTE EPC（演進分封核心網）是由 MME（移動性管理實體）、SGW（服務網關）、PGW（PDN 網關）和 HSS（歸屬訂戶服務器）組成，LTE EPC 是 4G LTE 網路的核心網，負責用戶的接入、移動性管理、數據傳輸和計費等功能。



*   **MME**：MME 負責用戶的接入和移動性管理。當用戶接入 LTE 網路時，MME 會進行認證和授權，並分配給用戶一個 IP 地址。當用戶在 LTE 網路中移動時，MME 會跟蹤用戶的位置，並確保其連接不中斷。
*   **SGW**：SGW 負責用戶的數據傳輸。SGW 負責將用戶的數據包從 LTE 網路路由到外部 IP 網絡，反之亦然。SGW 還可以根據用戶的 QoS 要求分配不同的服務質量。
*   **PGW**：PGW 負責將 LTE 網路連接到外部 IP 網絡。PGW 負責將用戶的數據包從 LTE 網路路由到外部 IP 網絡，反之亦然。PGW 還可以根據用戶的服務訂閱提供不同的服務。
*   **HSS**：HSS 負責存儲和管理用戶的數據和信息，包括用戶的 IMSI、Ki 號碼、認證信息、移動性信息和服務信息等。HSS 還負責處理用戶的認證、位置查詢和服務管理等請求。





![](https://t3764800.p.clickup-attachments.com/t3764800/edb06cf8-7301-448e-9fad-2104e66e205a/Screenshot_20231019_232653_Chrome.jpg)
