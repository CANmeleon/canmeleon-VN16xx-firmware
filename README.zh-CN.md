# CANmeleon VN16xx 兼容固件 — CANoe、CANalyzer 与 CANape

[English](README.md) · [简体中文](README.zh-CN.md)

CANmeleon VN16xx 固件让支持的 CANmeleon USB-CAN/CAN FD 硬件在 Windows 上通过 Vector 驱动接入 CANoe、CANalyzer、CANape 或 XL Driver Library（vxlapi）。VN1610、VN1640A 运行模式按固件版本、硬件和授权选择。

**[支持硬件](#支持硬件)** · [下载与安装](#下载与安装) · [VN16xx 使用指南](https://canmeleon.com/zh/firmware/vn1610/) · [CANmeleon 固件总览](https://github.com/CANmeleon/canmeleon-usb-can-firmware)

## 支持硬件

本固件安装于下列 CANmeleon 平台。设备型号表示实际硬件，VN1610/VN1640A 表示其固件运行模式。

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

- [VN16xx 问题反馈](https://github.com/CANmeleon/canmeleon-VN16xx-firmware/issues)：附完整硬件型号、固件版本、运行模式、Vector 驱动版本、软件版本和复现步骤。
- [管理器故障排查](https://canmeleon.com/zh/device-manager/faq/)：设备识别、安装或恢复问题。
- [固件总览](https://github.com/CANmeleon/canmeleon-usb-can-firmware)：PCAN、GS USB、Kvaser、ES582 等其他软件路径。
