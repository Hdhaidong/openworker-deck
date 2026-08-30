<div align="center">

# OpenWorker Deck

**给你的 AI 同事一个身体 · Give your AI coworker a body**

四大支柱：**智能链接**（MHS 原生）· **边缘计算** · **检测** · **存储**，外加预测维护 —— 以及一块 TRAE 式的桌面 Agent 面板。

An open-source hardware companion for [OpenWorker](https://github.com/andrewyng/openworker) — TRAE-style agent visibility on a desk device, built on four pillars: **smart link** (MHS-native) · **edge computing** · **detection** · **storage** — with predictive maintenance on top.

[![Crowdfunding](https://img.shields.io/badge/Status-Crowdfunding_Coming_Soon-orange)]()
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
| **Smart link (MHS-native)** | Registers itself and every bridged device on your network following the [Model Hardware Standard](https://modelhardwarestandard.com/) pattern — standard read/write interface, natural-language safety labels auto-generated. Any MHS-compatible agent (OpenWorker, Claude) discovers it instantly. |
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
| Ports | CAN 2.0B · RS-485 (Modbus RTU) · 1-Wire · OBD-II via adapter |
| Radios | BLE 5.2 · Wi-Fi 4 |
| Power | USB-C PD · optional passive PoE |
| Enclosure | Desktop edition + IP65 field edition (−20 to 60 °C) |
| Firmware | Open source, MIT — MHS-compatible registration |

### Crowdfunding tiers (planned)

| Tier | Price | Includes |
|---|---|---|
| Early Bird | $89 (limited 500) | 1× Deck, sensor set, desk stand |
| Standard | $109 | 1× Deck, sensor set |
| Duo | $199 | 2× Decks — desk + workshop |
| Fleet | $499 | 6× Decks, field edition, fleet dashboard |
| Clinic / Lab Pack | $899 | 10× Decks, compliance-report templates, priority support |

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
| **智能链接（MHS 原生）** | 按模型硬件标准（[MHS](https://modelhardwarestandard.com/)）的模式在网络上注册自己和桥接的每台设备 —— 标准读写接口 + 自动生成的自然语言安全标签。任何 MHS 兼容 Agent（OpenWorker、Claude）即插即发现。 |
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

### 九大设备领域

Deck 覆盖与 Hardware Repair Companion 相同的九个领域，合规姿态一致：医用领域只做环境与设备间监测（绝不接患者回路）；消防安全只做记录与预警（绝不替代法定年检）。

### 众筹档位（规划中）

早鸟 $89（限量 500）· 标准 $109 · 双机 $199 · 车队 $499（6 台 + 场版）· 诊所/实验室包 $899（10 台 + 合规报告模板 + 优先支持）

### 风险，说实话

MHS 仍是研究预览版（固件开源，随标准演进持续更新）；认证周期可能影响发货；元器件供应有二供方案；合规边界是固定的 —— Deck 是监测设备，不是医疗器械，也不替代消防法定检测。

### 创作者

**[Hdhaidong](https://github.com/Hdhaidong)** —— 定制业务 Agent 创作者，OpenWorker 平台 [Amazon Product Scout](https://github.com/andrewyng/openworker/pull/592) 与 [Hardware Repair Companion](https://github.com/andrewyng/openworker/pull/593) 两个同事的作者。这场众筹是那项工作的硬件一半：**会思考的 Agent，和它坐镇的桌面。**

---

<div align="center">

*Open firmware (MIT) · Local-first · Made for [OpenWorker](https://github.com/andrewyng/openworker) and the [Model Hardware Standard](https://modelhardwarestandard.com/)*

</div>
