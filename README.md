# CANmeleon VN16xx-Compatible Firmware — CANoe, CANalyzer and CANape

[English](README.md) · [简体中文](README.zh-CN.md)

CANmeleon VN16xx firmware connects supported CANmeleon USB-CAN/CAN FD hardware to the Vector driver and CANoe, CANalyzer, CANape or XL Driver Library (vxlapi) workflows on Windows. Select VN1610 or VN1640A operation according to the firmware version, hardware and available license.

**[Supported hardware](#supported-hardware)** · [Download and install](#download-and-install) · [VN16xx guide](https://canmeleon.com/en/firmware/vn1610/) · [All CANmeleon firmware](https://github.com/CANmeleon/canmeleon-usb-can-firmware)

## Supported hardware

Install this CANmeleon firmware on the supported platforms below. The model is the physical hardware you own; VN1610/VN1640A identifies its firmware operating mode.

| Hardware | Physical channels | Hardware documentation |
| --- | --- | --- |
| KH-UCANFD-LITE-X2U | 2 | [LITE specifications and wiring](https://docs.kunhong-elec.com/en/products/can-communication/KH-UCANFD-LITE-X2.html) |
| KH-UCANFD-PRO-X2U | 2 | [PRO specifications and wiring](https://docs.kunhong-elec.com/en/products/can-communication/KH-UCANFD-PRO-X2.html) |
| KH-UCANFD-PRO-X4U | 4 | [PRO specifications and wiring](https://docs.kunhong-elec.com/en/products/can-communication/KH-UCANFD-PRO-X2.html) |
| KHCM102 | 2 | [Controller IC documentation](https://docs.kunhong-elec.com/en/products/can-communication/CANmeleon-controller-ic.html) |

Confirm the complete model and available VN16xx package in [Device Manager](https://github.com/CANmeleon/canmeleon-device-manager). Mode availability and usable CAN/LIN channels depend on hardware, firmware version and licensing. See the [device catalog](https://canmeleon.com/en/firmware/devices/) for the maintained model list.

## Modes and software compatibility

| Mode | Operation |
| --- | --- |
| VN1610 | Use the Vector driver and assign physical channels to the target software. |
| VN1640A | Firmware release 8.12.0 introduced four CAN FD channels or two CAN FD plus two LIN channels, subject to suitable hardware and licensing. |

| Software or API | Connection path |
| --- | --- |
| CANoe | Vector driver and mapped physical channels; use the relevant CANoe software license. |
| CANalyzer | Vector driver and mapped physical channels; use the relevant CANalyzer software license. |
| CANape | Vector driver and mapped physical channels; use the relevant CANape software license. |
| Vector XL Driver Library / vxlapi | Develop applications using the Vector driver and physical channels. |

Follow the [firmware guide](https://canmeleon.com/en/firmware/vn1610/) for software-specific setup. The selected mode and driver determine which channel options are available.

## Download and install

1. Install [CANmeleon Device Manager for Windows x64](https://canmeleon.com/en/device-manager/#downloads), connect your device, and check its model and firmware applicability.
2. Select an applicable release in **Firmware Catalog**. For offline installation, download the [G2 8.15.2 firmware ZIP](https://gitee.com/sysmax/kpcfg4-canmeleon/releases/download/8.15.2/KH-UCANFD-G2.zip) and use **Import firmware ZIP**. This package requires manager **0.8.1 or later**; [read its release notes](https://gitee.com/sysmax/kpcfg4-canmeleon/releases/tag/8.15.2).
3. Select **VN16xx** firmware, review storage and pending changes, and confirm installation. Keep the device connected until writing completes.
4. Reconnect and select **Switch to this firmware**. Wait for the USB device to re-enumerate.
5. Install the driver from [Vector Driver Setup](https://www.vector.com/latest-driver-setup-windows), following the [VN16xx driver guide](https://canmeleon.com/en/guides/vector/driver/install/).
6. Open Vector Hardware Manager or Vector Hardware Config. Verify physical channels and map them to CANoe, CANalyzer, CANape or your XL Driver Library application.

Firmware packages are centralized in the [CANmeleon firmware overview and release hub](https://github.com/CANmeleon/canmeleon-usb-can-firmware). See [firmware management](https://canmeleon.com/en/device-manager/firmware-management/) and [recovery](https://canmeleon.com/en/device-manager/updates-and-recovery/) for installation details.

## Frequently asked questions

**Is this a firmware update for my Vector-manufactured VN1610 or VN1640A?**

This package is installed on the CANmeleon platforms listed above. For Vector-manufactured hardware, obtain device updates through Vector's support and download channels.

**Can a two-channel adapter become a four-channel interface?**

Firmware selection does not add physical channels. Four-channel operation requires suitable hardware and licensing.

**Which driver should I use?**

Use the Vector driver for the active VN16xx mode. After switching firmware, check Windows Device Manager and channel mapping in the Vector hardware configuration tool.

**Where is the firmware source code?**

This repository provides compatibility and installation documentation with binary-package download links. Refer to the relevant component or release for licensing information.

## Help and related firmware

- [Report a VN16xx issue](https://github.com/CANmeleon/canmeleon-VN16xx-firmware/issues): include the full hardware model, firmware version, active mode, Vector driver version, software version and steps to reproduce.
- [Device Manager troubleshooting](https://canmeleon.com/en/device-manager/faq/) for detection, installation or recovery issues.
- [Firmware catalog](https://github.com/CANmeleon/canmeleon-usb-can-firmware) for PCAN, GS USB, Kvaser, ES582 and other software workflows.
