<div align="center">

# OpenWorker Deck

**给你的 AI 同事一个身体 · Give your AI coworker a body**

四大支柱：**智能链接**（MHS 原生，直连设备）· **边缘计算** · **检测** · **存储**，外加预测维护 —— 以及一块 TRAE 式的桌面 Agent 面板。它同时是一台**工业网关 + 无线网关**：Modbus（RTU/TCP）· CAN/J1939 · OBD-II · BLE · LoRa，直连现场设备，无需集成商。

An open-source hardware companion for [OpenWorker](https://github.com/andrewyng/openworker) — TRAE-style agent visibility on a desk device, built on four pillars: **smart link** (MHS-native) · **edge computing** · **detection** · **storage** — with predictive maintenance on top. It talks to equipment **directly**: an industrial + wireless gateway speaking Modbus (RTU/TCP), CAN/J1939, OBD-II, BLE and LoRa.

[![Kickstarter](https://img.shields.io/badge/Status-Kickstarter_Coming_Soon-orange)](https://hdhaidong.github.io/openworker-deck/)
[![MHS](https://img.shields.io/badge/Model_Hardware_Standard-compatible-blue)](https://modelhardwarestandard.com/)
[![OpenWorker](https://img.shields.io/badge/OpenWorker-companion_agent-8A2BE2)](https://github.com/andrewyng/openworker)
[![License](https://img.shields.io/badge/Firmware-MIT-green)]()

</div>

---

## English

### The problem

[OpenWorker](https://github.com/andrewyng/openworker) gave AI coworkers a place to live — your desktop, your data, your permissions. But your coworker has no way to **show you** what it's doing when you're looking elsewhere, and no way to **touch** the physical world it keeps notes about.

Meanwhile, the machines you rely on — the tractor, the HVAC, the clinic sterilizer, the compressor in your workshop — fail on their own schedule, and nobody notices until they break.

### The solution

**OpenWorker Deck** is one device that solves both:

| Pillar | What it does |
|---|---|
| **Agent console (TRAE-style)** | A 4″ screen that mirrors your coworker's live todo list and progress panel. When the agent needs permission — OpenWorker's `interactive` mode — it rings the desk: a physical card with **Approve / Deny** buttons. A status ring shows idle / thinking / needs-you. |
| **Smart link (MHS-native)** | Connects to equipment **directly** — Modbus RTU master (RS-485 multi-drop), Modbus TCP, CAN 2.0B/J1939, OBD-II, BLE 5.2 and LoRa — then registers itself and every bridged device on your network following the [Model Hardware Standard](https://modelhardwarestandard.com/) pattern: standard read/write interface, natural-language safety labels auto-generated. Any MHS-compatible agent (OpenWorker, Claude) discovers it instantly. |
| **Detection** | Four sensing modalities: vibration (3-axis accelerometer), thermal (IR thermopile), current signature (CT clamp), and acoustic (MEMS mic). Plus CAN 2.0B / RS-485 Modbus / OBD-II / BLE bridging into existing fault codes. |
| **Edge computing** | On-device NPU (0.5 TOPS) runs anomaly detection locally. Works offline. Nothing leaves your network unless you say so. |
| **Storage** | Rolling telemetry history on microSD (up to 512 GB) + 8 GB eMMC. The Deck runs the night shift — it keeps sensing while your computer is off, and the agent ingests the buffer when you're back. |
| **Predictive maintenance** | Remaining-useful-life estimates from telemetry patterns: bearing wear, belt stretch, filter clog, refrigerant-loss curves — alerts days or weeks before the failure, not after. |

### The night-shift loop

```
your computer on:   OpenWorker ↔ Deck ↔ equipment   (live: agent reads, you approve)
your computer off: Deck → senses → stores          (night shift: buffered telemetry)
you return:        Deck → buffered history → OpenWorker   ("while you were away...")
```

Pairs with the open-source [Hardware Repair Companion](https://github.com/andrewyng/openworker/pull/593) coworker: the Deck senses, the agent diagnoses — telemetry as evidence, manuals and parts pulled from public sources, maintenance logged per device.

### Direct device link — industrial gateway + wireless gateway in one

Legacy fieldbus on one side, MHS on the other. Every protocol below maps onto the same standard read/write interface with safety labels, so the agent never learns a vendor SDK.

| Link | How it connects | Typical equipment |
|---|---|---|
| **Modbus RTU** | RS-485 master, multi-drop bus (up to 32 devices, unit IDs 1–247) — reads holding/input registers and coils directly | VFDs, PLCs, energy meters, irrigation valves, center pivots |
| **Modbus TCP** | Ethernet / Wi-Fi client — same registers, no adapter hardware | Building management, power monitors, industrial PCs |
| **CAN 2.0B / J1939** | Direct bus tap at 250/500 kbit/s, PGN decoding | Tractors, harvesters, engines, implements |
| **OBD-II** | Via adapter cable — standard OBD PIDs | Generators, vehicles, compact tractors |
| **BLE 5.2** | Central role — GATT sensor profiles and vendor services | Cordless-tool batteries, BLE sensors and gauges |
| **LoRa 868/915 MHz** | Sub-GHz wireless gateway — field sensors at hundreds of meters to km range | Remote barns, pivots, tanks, greenhouses |
| **1-Wire** | Direct chain — digital temperature probes | Cold chains, boiler rooms |

No protocol island survives contact: the agent sees one MHS device tree, and the Deck translates underneath it. Devices with no digital interface at all fall back to the four contactless sensing modalities.

### Industrial design

Two editions, one design language — matte graphite enclosures, functional color accents, fanless passive cooling:

| Edition | Form factor | Role |
|---|---|---|
| **Desktop** | CNC anodized aluminum, 4″ console, USB-C powered, status ring | Sits next to you: todo/progress panel, physical Approve/Deny permission cards |
| **Industrial** | 35 mm DIN-rail, terminal blocks (RS-485/CAN), RJ45 (Modbus TCP), LoRa antenna, heatsink fins | Goes in the cabinet: wide-temperature, IP65 variant for the field |

Concept renders (EVT-phase): [`img/deck-desktop.jpg`](img/deck-desktop.jpg) · [`img/deck-industrial.jpg`](img/deck-industrial.jpg) — final tooling may adjust.

### Nine equipment domains

The Deck works across the same nine domains the Hardware Repair Companion covers — with the compliance posture to match:

| Domain | Deck's role |
|---|---|
| Household | Full monitoring: HVAC, washer, water heater |
| Garden / Yard | Seasonal equipment, irrigation controllers |
| Outdoor | Generators (with CO-alarm integration), power stations |
| Agriculture | Tractors via OBD-II/CAN, hour-meter telemetry, pivots via Modbus |
| Laboratory | Equipment-room sensing; MHS-native domain — no instrument contamination |
| Medical | Environment + equipment-room monitoring only — never patient-connected circuits |
| Private clinic | Uptime triage feeds: sterilizer cycle counts, compressor duty cycles |
| Dental | Chair hydraulics, compressor and suction duty monitoring |
| Fire safety | Detector health, extinguisher pressure trends, emergency-light battery logging — records that survive an audit, never a replacement for certified inspection |

### Specs

| | |
|---|---|
| SoC | Dual-core Cortex-A7 @ 1.2 GHz + 0.5 TOPS NPU |
| Memory / storage | 256 MB RAM · 8 GB eMMC · microSD up to 512 GB |
| Display | 4″ LCD — todo/progress panel, permission cards |
| Controls | Approve / Deny buttons · rotary encoder · status ring |
| Sensors | 3-axis accelerometer · IR thermopile · CT clamp (0–100 A) · MEMS mic |
| Ports | CAN 2.0B / J1939 · RS-485 (Modbus RTU multi-drop) · 10/100M Ethernet (Modbus TCP) · 1-Wire · OBD-II via adapter |
| Radios | BLE 5.2 · Wi-Fi 4 · LoRa 868/915 MHz (optional module) |
| Power | USB-C PD · optional passive PoE |
| Enclosure | Desktop edition + IP65 field edition (−20 to 60 °C) + DIN-rail industrial edition |
| Firmware | Open source, MIT — MHS-compatible registration |

### Crowdfunding tiers (planned)

Platform: **Kickstarter** (all-or-nothing). Campaign goal: **$60,000**. Launch pending platform review.

| Tier | Price | Includes |
|---|---|---|
| Early Bird | $89 (limited 500) | 1× Deck, sensor set, desk stand |
| Standard | $109 | 1× Deck, sensor set |
| Duo | $199 | 2× Decks — desk + workshop |
| Fleet | $499 | 6× Decks, field edition, fleet dashboard |
| Clinic / Lab Pack | $899 | 10× Decks, compliance-report templates, priority support |

### Competitive landscape

Two benchmarks frame the price:

- **[Moxa](https://www.moxa.com.cn/)** (Taiwan) — the incumbent industrial-protocol gateway vendor. A Modbus TCP/RTU gateway ([MGate MB3170-G2](https://shopmoxa.neteon.net/mgate-mb3170/)) lists around **$426**; CAN/J1939 gateways ([MGate 5121](https://marugged.com/mgate-5121-series/)) around **$1,117**; IIoT edge gateways with cloud integration run **$780–1,600**. Strengths: −40 to 75 °C wide temp, IEC 62443, 70-country channel. Not offered: AI-agent integration, MHS, OBD-II/BLE/LoRa as first-class links, sensing or predictive maintenance, a desk console.
- **[USR IOT](https://www.usr.cn/)** (Jinan) — the value champion of Chinese IIoT. Serial device servers from **¥59**, rail-mount Modbus gateways ([USR-DR302](https://www.usr.cn/)) around **¥134–160**, edge gateways ([USR-M300](https://shop.usr.cn/mobile/Goods/categoryList.html)) **¥1,099**, 5G industrial routers **¥1,298–1,799**. Strengths: price, SKU breadth, e-commerce availability, 有人云. Not offered: AI-agent or MHS integration, CAN/J1939/OBD-II focus, detection/predictive-maintenance/storage narrative, desk console.

The Deck is not a cheaper gateway — it is a different category: **the gateway your agent operates**. Same field protocols in one box, plus MHS-native registration, the approval console, four-modality sensing, edge anomaly detection, night-shift storage and predictive maintenance, at a crowdfunding price of **$89–109**.

### Timeline

Campaign (30 days) → tooling & EVT (10 weeks) → DVT (8 weeks) → PVT & certification (6 weeks) → production & fulfillment (8 weeks). Estimated delivery: ~8 months after campaign close.

### Risks, honestly

- **MHS is a research preview.** The Deck follows its published pattern (standard drivers, plain-language safety labels, read/write discipline) and will track the spec as it stabilizes — firmware updates are open source and shipped as they land.
- **Certification timing** (FCC/CE and regional equivalents) gates shipping dates; we buffer PVT accordingly.
- **Component supply** — the SoC and display have second-source plans.
- **Compliance boundaries are fixed, not stretch goals**: the Deck is a monitoring device. It is not a medical device, and it does not replace certified fire-safety inspection.

### The creator

Built by **[Hdhaidong](https://github.com/Hdhaidong)** — custom business-agent creator. Also the author of the [Amazon Product Scout](https://github.com/andrewyng/openworker/pull/592) and [Hardware Repair Companion](https://github.com/andrewyng/openworker/pull/593) coworkers for OpenWorker. This campaign is the hardware half of that work: *the agent that thinks, and the desk it sits at.*

---

## 中文

### 问题

[OpenWorker](https://github.com/andrewyng/openworker) 让 AI 同事住进了你的电脑 —— 你的数据、你的权限、你的桌面。但这个同事**看不见**你不在电脑前时的任务进度，也**摸不着**它一直在记录的那个物理世界。

同时，你依赖的机器 —— 拖拉机、暖通、诊所灭菌器、车间空压机 —— 按自己的节奏坏，坏了才有人知道。

### 方案

**OpenWorker Deck**，一台设备解决两件事：

| 支柱 | 它做什么 |
|---|---|
| **Agent 控制台（TRAE 式）** | 4″ 屏幕实时镜像同事的 todo 清单和进度面板。Agent 需要权限时（OpenWorker 的 `interactive` 模式），桌面响起提示：一张实体卡片 + **批准 / 拒绝** 物理按键。状态灯环显示 空闲 / 思考中 / 等你确认。 |
| **智能链接（MHS 原生）** | **直连设备**：Modbus RTU 主站（RS-485 多点）· Modbus TCP · CAN/J1939 · OBD-II · BLE 5.2 · LoRa，再按模型硬件标准（[MHS](https://modelhardwarestandard.com/)）注册自己和桥接的每台设备 —— 标准读写接口 + 自动生成的自然语言安全标签。任何 MHS 兼容 Agent（OpenWorker、Claude）即插即发现。 |
| **检测** | 四种感知模态：振动（三轴加速度计）、热成像（红外热电堆）、电流特征（钳形表）、声学（MEMS 麦克风）。外加 CAN / RS-485 Modbus / OBD-II / BLE 桥接现有故障码。 |
| **边缘计算** | 板载 NPU（0.5 TOPS）本地跑异常检测。离线可用。不经你允许，数据不出你的网络。 |
| **存储** | microSD（最高 512GB）+ 8GB eMMC 滚动遥测历史。电脑关机它值守夜班 —— 持续感知存储，你回来时 Agent 一键消化缓冲。 |
| **预测维护** | 从遥测模式估算剩余使用寿命：轴承磨损、皮带拉伸、滤芯堵塞、制冷剂流失曲线 —— 在故障前几天到几周预警，而不是事后。 |

### 夜班闭环

```
电脑开机：  OpenWorker ↔ Deck ↔ 设备    （实时：Agent 读取，你批准）
电脑关机：  Deck → 感知 → 存储          （夜班：缓冲遥测）
你回来时：  Deck → 缓冲历史 → OpenWorker （"你不在的这段时间…"）
```

与开源的 [Hardware Repair Companion](https://github.com/andrewyng/openworker/pull/593) 同事配对使用：Deck 负责感知，Agent 负责诊断 —— 遥测即证据，手册配件从公开来源检索，每台设备独立维护日志。

### 直连设备 —— 工业网关 + 无线网关一体

一侧接传统现场总线，一侧输出 MHS。Agent 永远不需要学厂商 SDK。

- **Modbus RTU** —— RS-485 主站多点直读寄存器与线圈（32 台 · 单元号 1–247）：变频器、PLC、电表、灌溉阀、枢轴灌溉
- **Modbus TCP** —— 以太网 / Wi-Fi 客户端，同一套寄存器，无需转接硬件：楼宇自控、电力监控
- **CAN 2.0B / J1939 · OBD-II** —— 总线直挂 + PGN/PID 解码：拖拉机、收割机、发电机、车辆
- **BLE 5.2** —— 无线传感中枢：电动工具电池、BLE 传感器仪表
- **LoRa 868/915 MHz** —— 远距离无线网关，数百米到公里级：远端大棚、粮仓、水塔、泵站
- **1-Wire** —— 数字温度探头链：冷库、锅炉房

协议孤岛到此为止：Agent 看到的是一棵 MHS 设备树，翻译由 Deck 在底层完成。完全没有数字接口的设备，退回四模态非接触感知。

### 工业设计

一个设计语言，两种形态 —— 哑光深灰机身、功能色点睛、无风扇被动散热：

- **桌面版**：CNC 铝合金阳极氧化外壳，4″ 控制台 + 状态灯环，USB-C 供电 —— 坐在你手边，值守 Agent 的任务面板与权限卡
- **工业版**：35 mm DIN 轨安装，RS-485/CAN 端子排 + RJ45 + LoRa 天线 + 散热鳍片，宽温进柜，另有 IP65 场版

概念渲染（EVT 阶段）：[`img/deck-desktop.jpg`](img/deck-desktop.jpg) · [`img/deck-industrial.jpg`](img/deck-industrial.jpg) —— 量产模具或有微调。

### 九大设备领域

Deck 覆盖与 Hardware Repair Companion 相同的九个领域，合规姿态一致：医用领域只做环境与设备间监测（绝不接患者回路）；消防安全只做记录与预警（绝不替代法定年检）。

### 众筹档位（规划中）

平台：**Kickstarter**（全有或全无）。众筹目标：**$60,000**。上线以平台审核为准。

早鸟 $89（限量 500）· 标准 $109 · 双机 $199 · 车队 $499（6 台 + 场版）· 诊所/实验室包 $899（10 台 + 合规报告模板 + 优先支持）

### 竞品对标

两个标杆框定了这个价位：

- **[台湾摩莎 Moxa](https://www.moxa.com.cn/)** —— 工业协议网关的老牌厂商：Modbus TCP/RTU 网关（MGate MB3170-G2）约 **$426**，CAN/J1939 网关（MGate 5121）约 **$1,117**，带云对接的 IIoT 边缘网关 **$780–1,600**。强项：宽温 −40~75 °C、IEC 62443 认证、70 国渠道。没有的：AI Agent 集成、MHS、OBD-II/BLE/LoRa 一等公民支持、传感检测/预测维护、桌面控制台。
- **[济南有人 USR IOT](https://www.usr.cn/)** —— 国产 IIoT 性价比之王：串口服务器 **¥59** 起，导轨 Modbus 网关（USR-DR302）约 **¥134–160**，边缘计算网关（USR-M300）**¥1,099**，5G 工业路由 **¥1,298–1,799**。强项：价格、SKU 广度、电商渠道、有人云。没有的：AI Agent / MHS 集成、CAN/J1939/OBD-II 主打、检测/预测维护/存储叙事、桌面控制台。

Deck 不是更便宜的网关，是不同品类：**Agent 能亲手操作的网关** —— 同一套现场协议装进一个盒子，加上 MHS 原生注册、批准控制台、四模态检测、边缘异常检测、夜班存储与预测维护，众筹价 **$89–109**。

### 风险，说实话

MHS 仍是研究预览版（固件开源，随标准演进持续更新）；认证周期可能影响发货；元器件供应有二供方案；合规边界是固定的 —— Deck 是监测设备，不是医疗器械，也不替代消防法定检测。

### 创作者

**[Hdhaidong](https://github.com/Hdhaidong)** —— 定制业务 Agent 创作者，OpenWorker 平台 [Amazon Product Scout](https://github.com/andrewyng/openworker/pull/592) 与 [Hardware Repair Companion](https://github.com/andrewyng/openworker/pull/593) 两个同事的作者。这场众筹是那项工作的硬件一半：**会思考的 Agent，和它坐镇的桌面。**

---

<div align="center">

*Open firmware (MIT) · Local-first · Made for [OpenWorker](https://github.com/andrewyng/openworker) and the [Model Hardware Standard](https://modelhardwarestandard.com/)*

</div>
