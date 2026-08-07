---
sidebar_position: 5
---

# Interface Description

This introduces the interfaces and indicators of Radxa Linkr to help users connect and use the device correctly.

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-interface.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

| # | Description | # | Description |
| :--: | :--------------------- | :--: | :--------------------------------------------------------------- |
|  1   | User Button |  2   | USB-C Device Port |
|  3   | HDMI Input Port |  4   | Video Status Indicator |
|  5   | System Status Indicator |  6   | USB-C Network Port |

## User Button

- **Short press once**: The device highlights on [linkr.now](https://linkr.now), which can be used to quickly locate the device.

- **Long press ≥ 10 seconds**: Reset the device (restore all configurations to factory defaults).

:::warning Reset Note
Long-pressing the user button resets the system and clears all local configurations (including network, account, Tailscale binding, etc.). Please make sure to back up necessary information before operating.
:::

## USB-C Device Port

Used to connect to the controlled device's USB port to transmit keyboard and mouse data, or to connect to a PC for firmware flashing.

- Data Transmission

Used to transmit keyboard and mouse data to the controlled device for remote control. At the same time, the controlled device can power the Linkr through this port.

- Firmware Flashing

When the device malfunctions, you can connect the Linkr to a PC via the USB-C device port and use a flashing tool to burn the firmware.

## HDMI Input Port

Used to connect to the controlled device's HDMI output port to capture video signals; supports up to 2K@30Hz video input.

## Video Status Indicator

The onboard video status LED shows the video (HDMI) signal status of the controlled device, helping users determine whether the video link is normal.

| LED Status | Description |
| -------- | ------------------ |
| Off | No video signal |
| On | Video signal present |
| Blinking | Video link abnormal or error |

:::tip Video Status Indicator

The HDMI indicator can be controlled on the [linkr.now](https://linkr.now) page to turn it on or off.

:::

## System Status Indicator

The onboard system status LED shows the device's running status, helping users determine whether the device is working normally.

| LED Status | Description |
| -------- | -------------------------- |
| Blue blinking | System booting |
| Solid blue | System running normally |
| Solid green | In use (active connection) |
| White blinking | Upgrading firmware |
| Solid white | Resetting system |

:::tip System Status Indicator

The system status indicator can be controlled on the [linkr.now](https://linkr.now) page to adjust its brightness.

:::

## USB-C Network Port

Used for wired connection to the management PC or router, supporting USB-C direct connection and USB-C to RJ45 adapter, providing a 10/100 Mbps Ethernet connection.
