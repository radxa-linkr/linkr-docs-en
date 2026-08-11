---
sidebar_position: 3
doc_kind: page
title: "Custom EDID"
description: "Configure a custom EDID for Radxa Linkr and understand the format requirements, hardware limits, and recovery procedure."
locale: en
product: linkr
task_type: config
last_verified: 2026-08-11
source_of_truth: local
---

# Custom EDID

EDID (Extended Display Identification Data) is a VESA-standard data format that describes a display's manufacturer, supported resolutions, refresh rates, and other capabilities. A target device reads the EDID provided by Linkr over HDMI and uses it to select suitable video output parameters.

Linkr's preset EDIDs work for most use cases. Configure a custom EDID only when the target device does not offer the resolution or refresh rate you need, or when its output is incompatible with the presets.

:::warning

An invalid EDID or one that exceeds Linkr's capture capabilities can cause a blank screen, unstable video, or missing display modes. Before changing it, note the current preset so that you can restore it.

:::

## Limitations

When selecting or generating an EDID, observe these limits:

- Video capture supports up to **2K at 30 FPS**. The maximum, preferred, and refresh-rate modes declared by the EDID must not exceed this limit.
- Interlaced scan modes are not supported. Use progressive scan modes only.
- Linkr supports at most **two EDID blocks**: 128 bytes (one block) or 256 bytes (two blocks).
- Linkr does not capture audio over HDMI, so audio support declared by the EDID does not affect audio capture. To capture audio from the target device, use **Virtual Sound Card** under [Virtual Devices](../web#virtual-devices).

## Prepare the EDID data

You can use a known-good monitor EDID or find one that meets the limits above in the [linuxhw/EDID](https://github.com/linuxhw/EDID) database.

Using the linuxhw/EDID database as an example:

1. Open the `Digital` directory and find a suitable display by manufacturer, model, and resolution.
2. Click the display's **ID** to open its EDID details.

![Select a display ID in the linuxhw/EDID database](/img/linkr/custom-edid-database.webp)

3. Find `edid-decode (hex)` and copy the hexadecimal bytes below it. Copy only the EDID data, without the heading, line numbers, separator, or decoded output.

![Copy the EDID data below edid-decode (hex)](/img/linkr/custom-edid-hex.webp)

:::tip

`Block 0` on the details page is the first 128-byte block. If the page also contains `Block 1`, the EDID is 256 bytes. Do not use an EDID that contains `Block 2` or any additional blocks.

:::

## Configure Linkr

1. Open the Linkr management web interface and sign in.
2. Open **Display Settings** from the toolbar.
3. Open **Resolution / Frame Rate** (EDID), then select **Custom**.
4. Paste the hexadecimal EDID data into the input field.
5. Click **Save** and wait for the target device to detect the updated display information.

The HDMI video may briefly disconnect after you save the setting. Some operating systems do not reread the EDID immediately; if necessary, reconnect the target device's HDMI cable or restart the target device.

## Validate the configuration

After video returns, check the target device's display settings:

- Confirm that the resolution and refresh rate declared by the EDID are available.
- Confirm that the Linkr web video is stable and has the correct aspect ratio.
- Reconnect HDMI or restart the target device and confirm that the setting remains effective.

## Restore a preset EDID

If the screen remains blank or the video is incorrect after saving:

1. Return to **Display Settings** in the Linkr web interface.
2. Open the **Resolution / Frame Rate** (EDID) list and select any resolution and refresh-rate preset provided by Linkr.

Selecting a preset restores the preset EDID. You do not need to clear the custom EDID input field.

## Troubleshooting

### No video after saving

- Confirm that the EDID contains only one or two blocks.
- Confirm that its preferred mode does not exceed 2K at 30 FPS and is not interlaced.
- Make sure you copied only complete hexadecimal bytes, without line numbers or decoded text.
- Select a resolution and refresh-rate preset provided by Linkr from the **Resolution / Frame Rate** (EDID) list.

### The target resolution is unavailable

- Confirm that the EDID includes the target mode in its detailed or standard timings.
- Reconnect HDMI to force the target device to read the EDID again.
- If the operating system caches display information, restart the target device and check again.

### Can I use an EDID that declares audio support?

Yes, but Linkr does not capture audio over HDMI. Declaring audio support in the EDID does not add audio to the remote video stream. To capture audio from the target device, use **Virtual Sound Card** under [Virtual Devices](../web#virtual-devices) to send audio to the browser for playback.
