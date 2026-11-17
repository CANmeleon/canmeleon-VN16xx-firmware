# CANmeleon VN16xx-Compatible Firmware — CANoe, CANalyzer and CANape

[English](README.md) · [简体中文](README.zh-CN.md)

CANmeleon VN16xx firmware connects supported USB-CAN/CAN FD hardware to the Vector driver and CANoe, CANalyzer, CANape or XL Driver Library (vxlapi) workflows on Windows. Select VN1610 or VN1640A operation according to the firmware version, hardware and available license.

**[Supported hardware](#supported-hardware)** · [Download and install](#download-and-install) · [VN16xx guide](https://canmeleon.com/en/firmware/vn1610/) · [All CANmeleon firmware](https://github.com/CANmeleon/canmeleon-usb-can-firmware)

## When to choose VN16xx firmware

- Connect hardware with a matching CANmeleon firmware port to CANoe, CANalyzer or CANape on Windows.
- Develop a custom CAN tool using Vector XL Driver Library (vxlapi).
- Choose VN1610 or VN1640A mode using the physical channel count, firmware version and license; then map channels in the Vector hardware configuration tool.

## Supported hardware

The supported platforms below are commercial adaptation examples using Kunhong KHCM chips or derived hardware. Install the package matching your exact model. The model is the physical hardware you own; VN1610/VN1640A identifies its firmware operating mode.

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

<!-- firmware-parameters:start -->
## Features and performance

VN1610 / VN1640 modes supported; select the channel count according to hardware and licensing.

### Communication capabilities

| Parameter | Capability / value | Notes |
| --- | --- | --- |
| CAN channels | VN1610: 2 channels; VN1640: 4 CAN / CAN FD channels | Each channel supports transmission and reception; this table covers CAN-channel modes. |
| Frame formats | 11 / 29-bit IDs; Classic CAN 0–8 B, CAN FD up to 64 B | Classic RTR supported; CAN FD supports BRS enabled or disabled. |
| Classic CAN bit rate | 5 kbit/s–1 Mbit/s | Configure the bus bit rate in the host software. |
| CAN FD data-phase bit rate | Up to 10 Mbit/s | Configure arbitration and data phases independently; use transceivers and bus wiring suitable for the selected rates. |
| Custom bit timing | Configurable bit rate, sample point and SJW | Configure these in the host software; the firmware adapts automatically. |
| Errors and node status | Error events, transmit / receive error counters and Bus-Off status reporting supported | Diagnose conditions such as missing ACKs and mismatched bit rates. |
| Bus-Off recovery | Recovery through a host-initiated reset supported | Communication resumes after resetting or reactivating the channel. |
| ISO-TP / UDS integration | Single-session diagnostic communication supported | Use with host diagnostic software. |
| Termination control | Software-controlled termination supported | Configure in Device Manager; requires hardware with software-controlled termination. |
| Bus load | Bus-load display supported | The typical difference from the value displayed with Vector hardware is no more than 1 percentage point. |
| Listen-only mode | Supported | Does not transmit frames or acknowledge frames on the bus in listen-only mode. |

### Timestamps

| Parameter | Capability / value | Notes |
| --- | --- | --- |
| Hardware receive timestamps | Supported | Records frame reception times for analyzing intervals between frames. |
| Hardware transmit-completion timestamps | Supported | Records actual frame transmission completion times. |
| Timestamp accuracy within one device | 1 µs | For comparing frame times across CAN channels within the same device. |
| Multi-device software synchronization accuracy | &lt; 10 µs | Vector specifies a typical software synchronization accuracy of 50 µs for its VN1610. |
| Reading timestamps in CAPL | time_ns supported (nanosecond units) | Read frame timestamps and calculate time intervals. |
| Timestamp resolution (XL API) | approximately 8 µs | Read frame timestamps through the corresponding Vector driver. |

### Typical communication performance

| Parameter | Capability / value | Notes |
| --- | --- | --- |
| 8-byte frame rate, one direction | approximately 23,000 frames/s (short-duration) | Standard-ID CAN FD frames with BRS; 1 Mbit/s arbitration / 8 Mbit/s data; one bus, one direction. |
| 64-byte frame receive rate | approximately 10,100 frames/s | Standard-ID CAN FD frames with BRS; 1 Mbit/s arbitration / 8 Mbit/s data; one bus, one direction. |
| 64-byte frame payload throughput | approximately 5.18 Mbit/s | Same bit-rate configuration as the preceding row; one bus, one direction; counts only the data fields of received frames. |

### Software and APIs

| Parameter | Capability / value | Notes |
| --- | --- | --- |
| Host platform and development API | Windows / Vector XL API supported | Uses the Vector driver for host-software integration and application development. |
| CANoe / CAPL | CAN transmission, reception, transmit-completion echo and status queries supported | — |
| Application software | CANoe / CANalyzer / CANape supported | Install the Vector driver. |

### Differences from Vector hardware and unsupported features

| Parameter | Capability / value | Notes |
| --- | --- | --- |
| CAN FD data-phase bit rate | Up to 10 Mbit/s | Vector specifies up to 8 Mbit/s for its VN1610. Higher-speed communication requires suitable transceivers and bus wiring. |
| TX Self-ACK | Not supported | Transmission requires another node to acknowledge frames; without ACKs, transmission is retried and subsequent frames may wait. |
| Restricted output mode | Not supported | Selecting Restricted still operates in normal mode. |
| Transceiver operating modes | Normal mode only | Selecting another transceiver mode leaves the device in normal transmit/receive operation. |
| Active error-frame transmission / fault injection | Not supported | Vector's VN1610 supports active error-frame transmission; this firmware supports error detection, error counters and Bus-Off status reporting. |
| Classic CAN triple sampling | Not supported; uses single sampling | Select single sampling in your project. |

<!-- firmware-parameters:end -->

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

- [Report a VN16xx issue](https://github.com/CANmeleon/canmeleon-usb-can-firmware/issues): include the full hardware model, firmware version, active mode, Vector driver version, software version and steps to reproduce.
- [Device Manager troubleshooting](https://canmeleon.com/en/device-manager/faq/) for detection, installation or recovery issues.
- [Firmware catalog](https://github.com/CANmeleon/canmeleon-usb-can-firmware) for PCAN, GS USB, Kvaser, ES582 and other software workflows.

Firmware problems and new feature requests can be submitted as [Issues in the main firmware repository](https://github.com/CANmeleon/canmeleon-usb-can-firmware/issues).

## Ecosystem participation and commercial services

CANmeleon works with hardware makers, chip vendors and developers. For software/firmware integration, CANmeleon firmware porting and maintenance on your chip platform, or custom firmware development, contact [len2slaw@foxmail.com](mailto:len2slaw@foxmail.com). Include your board/MCU, target API, required features and schedule.

[Open-source hardware projects](https://github.com/CANmeleon/canmeleon-hardware) · [Request an open-source board adaptation](https://github.com/CANmeleon/canmeleon-usb-can-firmware/issues/new?template=open_hardware_adaptation.md)
