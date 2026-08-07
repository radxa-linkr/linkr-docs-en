---
sidebar_position: 15
---

# Tailscale Remote Access

Radxa Linkr has a built-in Tailscale client. After joining the device to the Tailnet, you can access the Linkr management interface remotely through an encrypted network without a public IP or port forwarding.

Tailscale is based on the WireGuard protocol, and communication between devices is encrypted.

:::tip

Using Tailscale remotely does not affect the Linkr's local network access methods. The device can still be accessed via USB-C direct connection to PC, USB-C to RJ45 to router/switch, Wi-Fi hotspot, and Wi-Fi client connection.

:::

## Prerequisites

- Register a [tailscale.com](https://tailscale.com/) account

- The Linkr can access the internet

- The host (control device) can access the internet and has Tailscale installed

## Configure Tailscale

Go to the Linkr management page: Advanced Settings -> Enable Tailscale -> Bind Tailscale account.

- Enable / Bind Tailscale

Clicking the bind option will automatically redirect to the Tailscale login / authorization page. Follow the prompts to connect the device to the Tailnet.

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-tailscale.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-tailscale-connect.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-bind-succ.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

After successful binding, the [linkr.now](https://linkr.now/) management page will display the bound account and version information.

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-tailscale-succ.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

## View Tailscale IP

After successful binding, you can view the Tailscale IP assigned to the device (usually in the `100.x.x.x` range) in the [Tailscale Admin Console](https://login.tailscale.com/admin/machines).

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-tailscale-ip.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

## Remote Control of Linkr

Install and log in to Tailscale on the host (control device), make sure it joins the same account or Tailscale private network (Tailnet) as the Linkr device, then access the Linkr via the following address:

```text
https://<Device Tailscale IP>
```

If MagicDNS is enabled on the Tailnet, you can also access it via MagicDNS / Full domain:

```text
https://<device hostname>.<Tailnet DNS name>.ts.net
```

<div style={{textAlign: 'center'}}>
   <img src="/en/img/linkr/linkr-tailscale-remote-succ.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

:::tip Note
Tailscale only provides a secure network connection. When accessing the Linkr management interface, you still need to log in with the Linkr's own username and password.
:::

## References

- [Tailscale Official Documentation](https://tailscale.com/kb/)
- [Tailscale Admin Console](https://login.tailscale.com/admin/machines)
- [WireGuard Protocol](https://www.wireguard.com/)
