---
sidebar_position: 2
---

# Wake on LAN Device Wakeup

Radxa Linkr supports the **Wake on LAN (WOL)** feature. When the remote computer is in a shutdown or sleep state, the Linkr can send a Magic Packet to its NIC to remotely wake up the target device, without having to press the power button on site.

The Linkr and the target computer are usually in the same LAN via Ethernet cable or switch; after sending the wake-up packet, the target machine receives the broadcast packet matching its MAC address and starts up.

## Feature Overview

| Capability | Description |
| --- | --- |
| Web Interface Operation | Enter the MAC address in the management interface and send the wake-up packet with one click |
| Standard WOL Protocol | Send a 102-byte standard Magic Packet, UDP broadcast to `255.255.255.255:9` |
| MAC Address Validation | Supports 6-byte MAC format separated by `:` or `-`, prompts error for invalid input |

## Preparations Before Use

Before waking up the target computer via the Linkr, please confirm that the target machine is correctly configured for WOL:

### 1. Enable Wake on LAN in BIOS/UEFI

Enter the target computer's BIOS/UEFI settings and find and enable the following options (names vary by motherboard manufacturer):

- **Wake on LAN**
- **Power On By PCI-E / PME**
- **Resume by LAN**

Some motherboards need to keep the NIC powered in the shutdown state (ErP / deep power saving related options need to be disabled).

### 2. Enable NIC Wakeup in the Operating System

**Windows:**

1. Open "Device Manager" → Network Adapters → target NIC properties.
2. In "Advanced", enable **Wake on Magic Packet** (or similar option).
3. In "Power Management", check **Allow this device to wake the computer**.

**Linux:**

Use `ethtool` to check and enable (taking `eth0` as an example):

```bash
sudo ethtool eth0 | grep Wake-on
sudo ethtool -s eth0 wol g
```

### 3. Network Connection Requirements

- After the target computer is shut down, the **wired NIC** must maintain physical connection to the network (connected to the network cable, switch, or the network segment where the Linkr is located).
- The Linkr and the target computer should be in the **same layer-2 broadcast domain** (same LAN or VLAN), and the wake-up packet is sent via UDP broadcast.
- Wireless NICs generally have poor support for WOL, so it is recommended to use the MAC address of the wired NIC port.

### 4. Get the Target MAC Address

When the target computer is powered on, view the NIC MAC address through system commands or the router management page, for example:

- Windows: `ipconfig /all`
- Linux: `ip link show`
- macOS: `ifconfig`

Write down the MAC address of the NIC used to connect to the LAN where the Linkr is located.

## Operation Steps

### 1. Enter Advanced Settings

1. Open the Linkr management web interface and log in.
2. Click **Advanced Settings** (gear icon) at the bottom of the left sidebar.
3. Find the **Device Wakeup** collapsible panel on the page and expand it.

### 2. Enter the MAC Address

Fill in the target computer's NIC MAC address in the **MAC Address** input box.

Supported format examples:

```
00-E0-0C-1F-30-F1
00:E0:0C:1F:30:F1
```

Each segment is a two-digit hexadecimal number, 6 segments in total, separated by `-` or `:` (case insensitive).

### 3. Send Wake-up Packet

1. Confirm the MAC address is filled in correctly.
2. Click the green **Wake** button on the right.
3. Wait for the operation to complete:
   - **Send Successful**: The interface prompts success, and the target computer should start within a few to tens of seconds (depending on hardware and power state).
   - **Send Failed**: Please check the network connection and target-side WOL configuration, then retry.

:::tip Note
"Send Successful" means the Linkr has successfully sent the Magic Packet, which does not guarantee that the target computer will definitely power on. If the target side is not correctly configured for WOL or is not in the same broadcast domain, the computer may still fail to wake up.
:::

## Working Principle

Wake on LAN uses the standard Magic Packet format:

1. The packet body consists of a 6-byte `0xFF` header + 16 repetitions of the target MAC address, totaling 102 bytes.
2. The Linkr broadcasts the packet via UDP to `255.255.255.255:9` (standard WOL port).
3. The target NIC, in a shutdown/sleep but powered state, listens for link-layer traffic and triggers the motherboard to power on upon recognizing its own MAC.

```
Linkr management interface → Enter MAC → Click "Wake"
       ↓
  Construct Magic Packet (102 bytes)
       ↓
  UDP broadcast → 255.255.255.255:9
       ↓
  Target NIC receives → Motherboard powers on
```

## FAQ

### "Invalid MAC Address" Prompt

- Check that it is exactly 6 segments, each 2 hexadecimal characters.
- Confirm using `-` or `:` as the separator, not spaces or other symbols.
- Example: `AA-BB-CC-DD-EE-FF` or `aa:bb:cc:dd:ee:ff`.

### "Send Successful" Displayed but Computer Does Not Power On

- Confirm Wake on LAN is enabled in BIOS, and NIC wakeup is enabled in the OS.
- Confirm using the **wired NIC** MAC, and the network cable is still connected to the same LAN after shutdown.
- Check whether the motherboard disables NIC power after shutdown (ErP, EuP, and other power-saving options).
- Some computers only support wake from **sleep/hibernation**, not from full shutdown (S5) state.
- If the Linkr and the target computer are not in the same network segment or VLAN, the broadcast packet may not reach the target NIC.

### Send Failed

- Confirm the Linkr device network is normal; being able to access the management interface means basic connectivity.
- Check whether the switch/router between the Linkr and the target device allows broadcast traffic to pass through.
- Retry later; if it continues to fail, you can restart the Linkr network service or check the firmware version.

### How to Confirm Which NIC's MAC Is Used

If the computer has multiple NICs (wired, wireless, virtual), please use the MAC of the **actual wired NIC connected to the LAN where the Linkr is located**. You can temporarily disable other NICs and then execute `ipconfig` / `ip link` to confirm.

## Difference from "Prevent Sleep" Feature

The Linkr also provides a **Prevent Sleep** feature: when connected to the remote computer, it periodically sends tiny mouse movements to prevent the system from entering sleep. This feature applies to scenarios where the computer is **already powered on and connected via the Linkr**.

**Wake on LAN (Device Wakeup)**, on the other hand, is used to remotely power on the computer via a network magic packet when the computer is **shut down or in deep sleep**. The two have different purposes; please choose according to the actual scenario.

## Related Links

- [Wake-on-LAN Wikipedia](https://en.wikipedia.org/wiki/Wake-on-LAN)
- [IEEE 802.3 Magic Packet Description](https://en.wikipedia.org/wiki/Wake-on-LAN#Magic_packet)
