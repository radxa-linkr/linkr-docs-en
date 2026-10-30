---
sidebar_position: 6
doc_kind: page
---

# Capture Linkr Video with OBS

Load the Linkr device's management page in an OBS Studio **Browser** source to capture the controlled device's remote screen and add it to an OBS scene.

## Prerequisites

- The controlled device is connected to Linkr over HDMI, and video displays correctly in the management interface.
- The computer running OBS can reach Linkr over the network.
- [OBS Studio](https://obsproject.com/) is installed and offers a **Browser** source.

## Get the Device Address

1. Open [linkr.now](https://linkr.now/) in a regular browser, find the Linkr device whose video you want to capture, and open its management page.
2. Copy the management page URL from the address bar, keeping its actual protocol, IP address or hostname, and port. For example, an HTTP address might be `http://192.168.1.100/`; replace this with your device's address.

Use the device's own management address as the OBS Browser source URL. `https://linkr.now/` is the discovery portal, not the device's video page.

## Add a Browser Source

1. Open OBS and create or select a scene.
2. In the **Sources** panel, click **+ → Browser** and create a source, for example named `Linkr`.
3. Clear **Local file** and set **URL** to the device management address from the previous step.
4. Set **Width** and **Height**, for example to `1920 × 1080`. These values set the webpage viewport size; they do not change the controlled device's HDMI output resolution.
5. To specify the rendering frame rate, enable **Use custom frame rate** and set FPS to match the video, for example `30`. A higher value does not increase the frame rate of the Linkr video itself.
6. Click **OK** to save.

## Log In and Arrange the Video

1. Right-click the new Browser source and select **Interact**.
2. Enter the Linkr username and password in the interaction window and follow the login prompts. If two-factor authentication is enabled, enter the verification code as well.
3. Confirm that both the interaction window and the OBS preview show live video from the controlled device, then close the interaction window.
4. To keep only the video area, right-click the source and select **Transform → Edit Transform**. Adjust the top, bottom, left, and right crop values to remove the sidebar and bottom toolbar.
5. Position and resize the source on the canvas while preserving the video's aspect ratio.

:::tip Login and connection

The OBS Browser source uses a separate browser session, so complete login through **Interact**. In the current firmware, a new login replaces the previous session. Avoid logging in to the same Linkr from another browser during capture, as this may interrupt the OBS connection.

To keep the connection when switching scenes, leave **Shutdown source when not visible** and **Refresh browser source when scene becomes active** disabled in the source properties.

:::

## Verify the Captured Video

1. Switch windows or move the mouse on the controlled device and confirm that the OBS preview updates accordingly.
2. Check that the video area is complete, its aspect ratio is correct, and there is no black screen or unintended cropping.
3. Confirm that the video continues to update in the OBS preview after closing the **Interact** window. Capture setup is now complete.

## Troubleshooting

- **Browser is missing from the source list**: Install an official OBS package that includes the Browser source component. Some third-party Linux packages may omit it.
- **Only the login page appears**: Right-click the source and select **Interact** to log in within OBS.
- **An HTTPS page does not load**: Check that the device certificate is valid and trusted by the environment running OBS. Accepting a certificate prompt in a regular browser does not mean OBS also trusts it.
- **The page connects but the video is black**: Confirm that the controlled device is outputting HDMI video, then try switching Linkr's **Video Mode** to **MJPEG** through the interaction window. If video still does not appear, check the network connection, click **Refresh cache of current page** in the source properties, and reconnect.
- **Video is cropped or has black borders after a resolution change**: Adjust the Browser source size, crop values, and OBS canvas again while preserving the video's aspect ratio.

For OBS settings, see the official [Browser Source documentation](https://obsproject.com/kb/browser-source) and [Quick Start Guide](https://obsproject.com/kb/quick-start-guide).
