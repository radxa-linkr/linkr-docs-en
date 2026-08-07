---
sidebar_position: 7
---

# Hardware Connection

Radxa Linkr supports USB-C direct connection to PC, USB-C to RJ45 to router/switch, Wi-Fi hotspot, and Wi-Fi client connection. Users can choose the appropriate connection method based on the actual usage scenario.

The purpose of the above methods is to put Radxa Linkr and the host (control device) in the same local network, so as to control the controlled device within the same LAN.

:::tip Remote Access

If you need to access the controlled device across different LANs, please use Tailscale for remote access. For details, see the [Tailscale Remote Access](../advanced-usage/tailscale.md) page.

:::

## 4 Connection Methods

The Wi-Fi client and Wi-Fi hotspot methods need to be configured in the Radxa Linkr management interface, so the first configuration must use the USB-C direct connection and USB-C to RJ45 methods, and then configure the Wi-Fi client or Wi-Fi hotspot in the [linkr.now](https://linkr.now/) management interface.

<Tabs>
<TabItem value="usb-c-direct" label="USB-C Direct" default>

Connect the controlled device using the HDMI input port and USB-C device port of Radxa Linkr, and at the same time connect the USB-C network port of Linkr to the host (control device) using a USB-C cable.

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/usb-c-direct.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

① Radxa Linkr

② Controlled device

③ Host (control device)

</TabItem>
<TabItem value="usb-c-rj45" label="USB-C to RJ45">

Connect the controlled device using the HDMI input port and USB-C device port of Radxa Linkr, and at the same time connect the USB-C network port of Linkr to the router/switch using a USB-C to RJ45 cable.

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/usb-c-rj45.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

① Radxa Linkr

② Controlled device

③ Host (control device)

④ Router / Switch

</TabItem>
<TabItem value="wifi-hot" label="Wi-Fi Hotspot">

Connect the controlled device using the HDMI input port and USB-C device port of Radxa Linkr. After configuring the Wi-Fi hotspot in the [linkr.now](https://linkr.now/) management interface, the host (control device) connects to the Radxa Linkr Wi-Fi hotspot.

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/wifi-hot.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

① Radxa Linkr

② Controlled device

③ Host (control device)

</TabItem>
<TabItem value="wifi" label="Wi-Fi">

Connect the controlled device using the HDMI input port and USB-C device port of Radxa Linkr. After connecting to Wi-Fi in the [linkr.now](https://linkr.now/) management interface, the host (control device) and Radxa Linkr are on the same Wi-Fi network.

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/wifi.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

① Radxa Linkr

② Controlled device

③ Host (control device)

④ Router / Switch

</TabItem>
</Tabs>

## Indicator Description

After completing the hardware connection above, the system status indicator will change from blue blinking (system booting) to solid blue (system running normally). The video status indicator lights up when an HDMI video signal from the controlled device is detected.

:::tip Detailed Steps

For detailed operations of various hardware connection methods, please refer to the following tutorials:

- [USB-C Direct](../basic-usage/usb-c.md)

- [USB-C to RJ45](../basic-usage/rj45.md)

- [Wi-Fi Connection](../basic-usage/wifi.md)

- [Wi-Fi Hotspot](../basic-usage/wifi-hot.md)

:::
