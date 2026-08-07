---
sidebar_position: 1
---

# USB-C Direct

This mainly introduces how to control the controlled device using the USB-C direct connection method of Radxa Linkr.

## Hardware Connection

Connect the controlled device using the HDMI input port and USB-C device port of Radxa Linkr, and at the same time connect the USB-C network port of Linkr to the host (control device) using a USB-C cable.

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/usb-c-direct.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

① Radxa Linkr

② Controlled device

③ Host (control device)

- Indicator Description

After completing the hardware connection above, the system status indicator will change from blue blinking (system booting) to solid blue (system running normally). The video status indicator lights up when an HDMI video signal from the controlled device is detected.

## Control the Controlled Device

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

<Tabs>
<TabItem value="first-config" label="First Configuration" default>

For first-time configuration, the device name displays partial serial number information. Click the corresponding device option to configure.

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-select-device.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

- Set user information

Set the access username, password, and device name for the Linkr device, then click `Next` to proceed.

:::tip Device Name
For users with multiple Linkr devices, you can set different device names to distinguish them easily.
:::

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-device-info.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

</TabItem>
<TabItem value="config" label="Configured">

For Linkr devices that have completed the first configuration, the configured device name will be displayed in the device list.

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-device.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

</TabItem>
</Tabs>

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
