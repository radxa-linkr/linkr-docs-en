---
sidebar_position: 1
---

# Quick Start

This tutorial is designed to help you get started with Radxa Linkr quickly.

## Product Appearance

| # | View | # | View | # | View |
| :--: | :---------------: | :--: | :---------------: | :--: | :---------------: |
|  ①   | Linkr Front View |  ②   | Linkr Side View |  ③   | Linkr Back View |

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-view.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

## Product Interfaces

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-interface.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

| # | Description | # | Description |
| :--: | :--------------------- | :--: | :--------------------------------------------------------------- |
|  1   | User Button |  2   | USB-C Device Port |
|  3   | HDMI Input Port |  4   | Video Status Indicator |
|  5   | System Status Indicator |  6   | USB-C Network Port |

## Prerequisites

You need to prepare the following devices in advance:

- Radxa Linkr
- Host (control device)
- Controlled device (e.g., PC, SBC, industrial PC)
- USB-C cable
- USB-C cable or USB-C to RJ45 cable (for network connection)

:::tip Host (Control Device)
The host (control device) needs Chrome, Edge, or Firefox (latest version recommended), as you will later access the Radxa Linkr management interface in the browser.
:::

## Hardware Connection

Radxa Linkr supports USB-C direct connection to PC, USB-C to RJ45 to router/switch, Wi-Fi hotspot, and Wi-Fi client connection. The quick start mainly introduces the USB-C direct connection to PC and USB-C to RJ45 connection methods.

:::tip Other Connection Methods

For more connection methods, please refer to the [Hardware Connection](./connect-methods.md) page.

:::

<Tabs>
<TabItem value="usb-c-direct" label="USB-C Direct" default>

Connect the controlled device using the HDMI input port and USB-C device port of Radxa Linkr, and at the same time connect the USB-C network port of Linkr to the host (control device) using a USB-C cable.

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/usb-c-direct.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

1. Radxa Linkr
2. Controlled device
3. Host (control device)

</TabItem>
<TabItem value="usb-c-rj45" label="USB-C to RJ45">

Connect the controlled device using the HDMI input port and USB-C device port of Radxa Linkr, and at the same time connect the USB-C network port of Linkr to the router/switch using a USB-C to RJ45 cable.

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/usb-c-rj45.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

1. Radxa Linkr
2. Controlled device
3. Host (control device)
4. Router / Switch

</TabItem>
</Tabs>

After completing the hardware connection above, the system status indicator will change from blue blinking (system booting) to solid blue (system running normally). The video status indicator lights up when an HDMI video signal from the controlled device is detected.

## First Configuration

### Access [linkr.now](https://linkr.now/)

After completing the hardware connection, open the [linkr.now](https://linkr.now/) page using Chrome, Edge, or Firefox to access the Radxa Linkr management interface.

Note: The UI may differ after future linkr.now updates. Follow the actual on-screen prompts.

### Allow Access Permissions

When accessing the [linkr.now](https://linkr.now/) page for the first time, the browser may prompt you to allow access. Please follow the prompts so that Radxa Linkr can be discovered normally.

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-acess-allow.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

### Scan for Linkr Devices

Click the `Start Scanning` option to scan for Radxa Linkr devices on the local network.

:::tip Multiple Linkr Devices
If you have multiple Linkr devices, you can short-press the user button on the side of the Linkr, and the corresponding Linkr device will be highlighted on the device page for easy identification.
:::

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-scan.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

### Select Linkr Device

For first-time configuration, the device name displays partial serial number information. Click the corresponding device option to configure.

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-select-device.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

### Set User Information

Set the access username, password, and device name for the Linkr device, then click `Next` to proceed.

:::tip Device Name
For users with multiple Linkr devices, you can set different device names to distinguish them easily.
:::

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-device-info.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

### Log in to Linkr Device

After setting up, you can log in to the Linkr device using the username and password you just set.

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-login.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

### Linkr Management Interface

After successful login, the controlled device's system interface is displayed, with the Linkr device's function options on the side.

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-succ.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>
