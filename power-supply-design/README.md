# 电源模块设计（Power Supply Design）

基于 Altium Designer 24 的多路输出电源模块 PCB 设计项目。

## 📐 项目概述

本项目设计一个多路电源转换模块，支持三种输入方式和三路稳压输出：

| 输入 | 类型 |
|------|------|
| P1 | DC 圆口插座（3.5×1.3mm） |
| P2 | USB Type-C |

### 电源架构

```
VBAT+ ──→ [TPS5430 Buck] ──→ VCC5V (5V/3A)
                                  │
                                  └──→ [SPX29302 LDO] ──→ 3.3V/3A
                                                              │
                                                              └──→ [MT3608 Boost] ──→ +5V
```

### 主要芯片

| 芯片 | 型号 | 功能 | 封装 |
|------|------|------|------|
| U1 | TPS5430 | Buck 降压转换器，5V/3A 输出，500kHz | SOIC-8 EP (PowerPAD) |
| U2 | SPX29302 | LDO 线性稳压器，3.3V/3A | TO-263-5 |
| U3 | MT3608 | Boost 升压转换器，3.3V→5V | SOT-23-6 |
| D5 | SS54 | 肖特基二极管，5A | SMB |

### 关键网络
- `VCC5V` — TPS5430 Buck 输出
- `3.3V` — SPX29302 LDO 输出
- `+5V` — MT3608 Boost 输出
- `TYPE-C_5V` — USB-C 输入
- `GND` — 公共地

## 📁 文件结构

```
├── Power supply design.PrjPcb    # Altium 项目文件
├── Power supply design.PrjPcbStructure
├── dainyuan.SchDoc               # 原理图设计
├── dianyuan.PcbDoc               # PCB 设计
├── Schlib1.SchLib                # 原理图元件库
├── Power supply design.OutJob    # 输出作业配置
├── Power supply design.pdf       # 项目输出 PDF
├── buck电路元件选型计算.xlsx      # Buck 电路元件参数计算
├── 电源模块负载测试.xlsx          # 负载测试数据
├── Project Outputs for Power supply design/  # Gerber + DRC 报告
├── References/                   # 芯片数据手册与参考笔记
│   ├── tps5430.pdf               # TPS5430 数据手册（原版）
│   ├── tps5430-中文.pdf          # TPS5430 数据手册（中文翻译）
│   ├── SPX29300.PDF              # SPX29302 数据手册
│   ├── 二极管分类与应用参考.md
│   └── 电源拓扑分类与应用参考.md
└── .gitignore
```

## 🛠️ 设计要点

### 过孔规则
- 默认过孔：内径 0.3mm / 外径 0.6mm（12/24mil）
- 焊环宽度：0.15mm（6mil）
- 阻焊：常规盖油，散热焊盘开窗
- 过孔间距：≥0.25mm（10mil）
- 过孔到铜皮：≥0.15mm（6mil），电源网络建议 0.2mm

### 散热设计
- TPS5430 PowerPAD 底部：9 个过孔（3×3 阵列）
- SPX29302 散热铜皮：12-16 个过孔（开窗）
- 功率焊盘与 GND 铜皮采用直接连接

## 📝 开发环境

- **EDA 工具**: Altium Designer 24
- **PCB 打样**: 适用于嘉立创等常规工艺（0.3/0.6mm 过孔为标准工艺，无额外费用）

## 📄 许可

本项目为开源硬件设计，仅供学习与参考。
