# CANmeleon VN16xx 兼容固件 — CANoe、CANalyzer 与 CANape

[English](README.md) · [简体中文](README.zh-CN.md)

CANmeleon VN16xx 固件让支持的 USB-CAN/CAN FD 硬件在 Windows 上通过 Vector 驱动接入 CANoe、CANalyzer、CANape 或 XL Driver Library（vxlapi）。VN1610、VN1640A 运行模式按固件版本、硬件和授权选择。

**[支持硬件](#支持硬件)** · [下载与安装](#下载与安装) · [VN16xx 使用指南](https://canmeleon.com/zh/firmware/vn1610/) · [CANmeleon 固件总览](https://github.com/CANmeleon/canmeleon-usb-can-firmware)

## 什么时候选择 VN16xx 固件

- 将适用的 CANmeleon 硬件接入 Windows 上的 CANoe、CANalyzer 或 CANape。
- 使用 Vector XL Driver Library（vxlapi）开发自有 CAN 工具。
- 按物理通道、固件版本与授权选择 VN1610 或 VN1640A 模式，再在 Vector 硬件配置工具中映射通道。

## 支持硬件

下列支持平台属于鲲弘 KHCM 芯片或衍生硬件的商业适配案例，请选择与完整型号匹配的固件包。设备型号表示实际硬件，VN1610/VN1640A 表示其固件运行模式。

| 硬件 | 物理通道 | 硬件资料 |
| --- | --- | --- |
| KH-UCANFD-LITE-X2U | 2 | [LITE 规格与接线](https://docs.kunhong-elec.com/zh/products/can-communication/KH-UCANFD-LITE-X2.html) |
| KH-UCANFD-PRO-X2U | 2 | [PRO 规格与接线](https://docs.kunhong-elec.com/zh/products/can-communication/KH-UCANFD-PRO-X2.html) |
| KH-UCANFD-PRO-X4U | 4 | [PRO 规格与接线](https://docs.kunhong-elec.com/zh/products/can-communication/KH-UCANFD-PRO-X2.html) |
| KHCM102 | 2 | [控制器芯片资料](https://docs.kunhong-elec.com/zh/products/can-communication/CANmeleon-controller-ic.html) |

通过[设备管理器](https://github.com/CANmeleon/canmeleon-device-manager)核对完整型号和可用 VN16xx 固件包。运行模式及可用 CAN/LIN 通道取决于硬件、固件版本和授权。完整型号列表见[设备目录](https://canmeleon.com/zh/firmware/devices/)。

## 运行模式与软件接入

| 模式 | 使用方式 |
| --- | --- |
| VN1610 | 使用 Vector 驱动，将物理通道分配到目标软件。 |
| VN1640A | 8.12.0 起提供四通道 CAN FD 或双 CAN FD 加双 LIN 模式，需要对应硬件和授权支持。 |

| 软件或 API | 接入路径 |
| --- | --- |
| CANoe | Vector 驱动与物理通道映射，使用对应 CANoe 软件授权。 |
| CANalyzer | Vector 驱动与物理通道映射，使用对应 CANalyzer 软件授权。 |
| CANape | Vector 驱动与物理通道映射，使用对应 CANape 软件授权。 |
| Vector XL Driver Library / vxlapi | 通过 Vector 驱动和物理通道开发应用。 |

软件配置见[固件指南](https://canmeleon.com/zh/firmware/vn1610/)。可选通道配置取决于运行模式和驱动。

<!-- firmware-parameters:start -->
## 固件特性与性能参数

支持 VN1610 / VN1640 模式；通道数按硬件与授权选择。

### 通信能力

| 参数 | 能力 / 数值 | 备注 |
| --- | --- | --- |
| CAN 通道 | VN1610：2 路；VN1640：4 路 CAN / CAN FD | 每通道支持发送和接收；本表为 CAN 通道模式。 |
| 报文格式 | 11 / 29 位 ID；Classic CAN 0–8 B，CAN FD 最高 64 B | 支持 Classic RTR；CAN FD 支持 BRS 开启 / 关闭。 |
| Classic CAN 速率 | 5 kbit/s–1 Mbit/s | 通过上位机设置总线速率。 |
| CAN FD 数据速率 | 最高 10 Mbit/s | 仲裁段与数据段独立配置；需配套相应速率的收发器和总线布线。 |
| 自定义位时序 | 支持速率、采样点和 SJW 配置 | 在上位机中设置，固件自动适配。 |
| 错误与节点状态 | 支持错误事件、发送 / 接收错误计数及 Bus-Off 状态上报 | 支持无 ACK、速率不匹配等故障的状态诊断。 |
| Bus-Off 恢复 | 支持上位机复位恢复 | 复位或重新激活通道后恢复通信。 |
| ISO-TP / UDS 接入 | 支持单会话诊断通信 | 配合上位机诊断软件使用。 |
| 终端电阻控制 | 支持软件控制终端电阻 | 通过设备管理器设置；需配套软控终端硬件。 |
| 总线负载率 | 支持显示总线负载率 | 与 Vector 原装显示值的典型差异不超过 1 个百分点。 |
| 监听模式 | 支持 | 监听时不发送报文，也不向总线提供 ACK。 |

### 时间戳

| 参数 | 能力 / 数值 | 备注 |
| --- | --- | --- |
| 接收硬件时间戳 | 支持 | 记录报文接收时间，可用于报文时间间隔分析。 |
| 发送完成硬件时间戳 | 支持 | 记录报文实际发送完成时间。 |
| 同设备内时间戳精度 | 1 µs | 用于同一设备内各 CAN 通道的报文时间比较。 |
| 多设备软件同步精度 | &lt; 10 µs | Vector 官方 VN1610 标称软件同步精度为典型 50 µs。 |
| CAPL 时间戳读取 | 支持 time_ns（纳秒单位） | 读取报文时间并计算时间间隔。 |
| 时间戳分辨率（XL API） | 约 8 µs | 使用配套 Vector 驱动读取报文时间戳。 |

### 典型通信性能

| 参数 | 能力 / 数值 | 备注 |
| --- | --- | --- |
| 8 字节报文单向传输帧率 | 约 23,000 帧/秒（短时） | CAN FD 标准帧，启用 BRS；1 Mbit/s 仲裁 / 8 Mbit/s 数据；单条总线、单向。 |
| 64 字节报文接收帧率 | 约 10,100 帧/秒 | CAN FD 标准帧，启用 BRS；仲裁速率 1 Mbit/s，数据速率 8 Mbit/s。单条总线、单向。 |
| 64 字节报文有效数据吞吐 | 约 5.18 Mbit/s | 与上一行相同的速率配置，单条总线、单向；仅计算接收报文的数据字段。 |

### 软件配套

| 参数 | 能力 / 数值 | 备注 |
| --- | --- | --- |
| 主机平台与开发接口 | 支持 Windows / Vector XL API | 使用 Vector 驱动，支持上位机接入和应用开发。 |
| CANoe / CAPL | 支持 CAN 收发、发送完成回显和状态读取 | — |
| 配套应用软件 | 支持 CANoe / CANalyzer / CANape | 安装 Vector 驱动。 |

### 与原装的差异及不支持的功能

| 参数 | 能力 / 数值 | 备注 |
| --- | --- | --- |
| CAN FD 数据速率 | 最高 10 Mbit/s | Vector 官方 VN1610 最高 8 Mbit/s。高速通信需配套相应速率的收发器和总线布线。 |
| 发送自应答（TX Self-ACK） | 不支持 | 发送需要其他节点提供 ACK；没有 ACK 时会重试，后续发送可能等待。 |
| 受限输出模式（Restricted） | 不支持 | 选择 Restricted 后仍按普通模式运行。 |
| 收发器工作模式设置 | 仅支持正常模式（Normal） | 设置其他收发器模式时，设备仍保持正常收发状态。 |
| 主动错误帧发送 / 故障注入 | 不支持 | Vector 官方 VN1610 支持主动错误帧发送；本固件支持错误检测、错误计数和 Bus-Off 状态上报。 |
| Classic CAN 三次采样 | 不支持；使用单次采样 | 工程中选择单次采样。 |

<!-- firmware-parameters:end -->

## 下载与安装

1. 安装 [Windows x64 设备管理器](https://canmeleon.com/zh/device-manager/#downloads)，连接设备并核对型号和固件适用性。
2. 在固件目录选择适用版本。离线安装可下载 [G2 8.15.2 固件 ZIP](https://gitee.com/sysmax/kpcfg4-canmeleon/releases/download/8.15.2/KH-UCANFD-G2.zip)，使用导入固件 ZIP 功能；该包要求管理器 **0.8.1 或更新版本**，见[版本说明](https://gitee.com/sysmax/kpcfg4-canmeleon/releases/tag/8.15.2)。
3. 选择 **VN16xx** 固件，检查空间和待执行变更，确认安装。保持设备连接至写入完成。
4. 重新连接并切换到该固件，等待 USB 重新识别。
5. 从 [Vector Driver Setup](https://www.vector.com/latest-driver-setup-windows) 获取驱动，按 [VN16xx 驱动指南](https://canmeleon.com/zh/guides/vector/driver/install/)安装。
6. 打开 Vector Hardware Manager 或 Vector Hardware Config，核对物理通道并映射到 CANoe、CANalyzer、CANape 或 XL Driver Library 应用。

固件包由 [CANmeleon 固件总览与发布仓库](https://github.com/CANmeleon/canmeleon-usb-can-firmware)统一组织。详细操作见[固件管理](https://canmeleon.com/zh/device-manager/firmware-management/)与[更新恢复](https://canmeleon.com/zh/device-manager/updates-and-recovery/)。

## 常见问题

**这是 Vector 原厂 VN1610 或 VN1640A 的升级固件吗？** 本固件安装于上方列出的 CANmeleon 平台。Vector 原厂设备请通过 Vector 支持与下载渠道获取更新。

**双通道设备能变成四通道吗？** 切换固件不会增加物理通道。四通道运行需要相应硬件和授权支持。

**应使用哪个驱动？** 使用当前 VN16xx 模式对应的 Vector 驱动。切换后在 Windows 设备管理器中核对识别情况，并在 Vector 硬件配置工具中检查通道映射。

**固件源码在哪里？** 本仓库提供兼容说明、安装指南和二进制包下载入口，许可信息以对应组件或发布包为准。

## 帮助与相关固件

- [VN16xx 问题反馈](https://github.com/CANmeleon/canmeleon-usb-can-firmware/issues)：附完整硬件型号、固件版本、运行模式、Vector 驱动版本、软件版本和复现步骤。
- [管理器故障排查](https://canmeleon.com/zh/device-manager/faq/)：设备识别、安装或恢复问题。
- [固件总览](https://github.com/CANmeleon/canmeleon-usb-can-firmware)：PCAN、GS USB、Kvaser、ES582 等其他软件路径。

固件相关的问题和新需求可在 [GitHub 固件主仓库提 Issue](https://github.com/CANmeleon/canmeleon-usb-can-firmware/issues)。

## 生态参与与商业技术服务

CANmeleon 面向硬件厂商、芯片厂商和开发者。软件/固件集成、芯片平台 CANmeleon 固件移植与维护，以及定制固件开发，可联系 [len2slaw@foxmail.com](mailto:len2slaw@foxmail.com)，并说明板卡/MCU、目标 API、所需功能和计划时间。

[开源硬件与免费适配计划](https://github.com/CANmeleon/.github/blob/main/profile/README.zh-CN.md#开源建设与免费固件适配) · [申请开源板卡适配](https://github.com/CANmeleon/canmeleon-usb-can-firmware/issues/new?template=open_hardware_adaptation.md)
