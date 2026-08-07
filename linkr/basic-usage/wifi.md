---
sidebar_position: 8
---

# Wi-Fi Connection

This mainly introduces how to control the controlled device by connecting Radxa Linkr and the host (control device) to the same Wi-Fi network.

:::tip Prerequisites
The Wi-Fi connection needs to be configured in the [linkr.now](https://linkr.now/) management interface, so the first configuration must use the USB-C direct connection and USB-C to RJ45 methods to connect successfully before configuring the Wi-Fi connection.

- [USB-C Direct](./usb-c.md)

- [USB-C to RJ45](./rj45.md)

:::

## Hardware Connection

Connect the controlled device using the HDMI input port and USB-C device port of Radxa Linkr. After connecting to Wi-Fi in the [linkr.now](https://linkr.now/) management interface, the host (control device) and Radxa Linkr are on the same Wi-Fi network.

:::tip

The schematic is the Wi-Fi connection wiring diagram. If Wi-Fi is not connected, please configure the Wi-Fi connection via the wired connection (USB-C direct or USB-C to RJ45) first, then proceed with the hardware connection shown below.

:::

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/wifi.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

① Radxa Linkr

② Controlled device

③ Host (control device)

④ Router / Switch

- Indicator Description

After completing the hardware connection above, the system status indicator will change from blue blinking (system booting) to solid blue (system running normally). The video status indicator lights up when an HDMI video signal from the controlled device is detected.

## Control the Controlled Device

### Configure Wi-Fi Connection

Based on the wired connection (USB-C direct or USB-C to RJ45) method, configure the Wi-Fi connection in the Linkr management interface.

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-wifi-connect.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

### Control the Controlled Device via Wi-Fi

Disconnect the wired connection to verify the Wi-Fi control.

Open the [linkr.now](https://linkr.now/) page using Chrome, Edge, or Firefox to access the Radxa Linkr management interface.

Note: The UI may differ after future linkr.now updates. Follow the actual on-screen prompts.

### Allow Access Permissions

When accessing the [linkr.now](https://linkr.now/) page for the first time, the browser may prompt you to allow access. Please follow the prompts so that Radxa Linkr can be discovered normally.

:::tip

If access permission has already been granted, it will not be requested again. Proceed to the next step directly.

:::

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

Click the device card with the corresponding name to enter the control page.

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-device.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

### Log in to Linkr Device

Log in to the Linkr device using the set username and password.

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-login.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

### Linkr Management Interface

After successful login, the controlled device's system interface is displayed, with the Linkr device's function options on the side.

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-succ.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>
