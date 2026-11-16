---
sidebar_position: 6.5
doc_kind: page
title: "Plugins"
description: "Download Radxa Linkr plugins and use Plugin Center to install, enable, disable, and uninstall them."
locale: en
product: linkr
source_of_truth: local
---

# Plugins

Extend Radxa Linkr with plugins.

**Currently, only officially released plugins are supported. Custom plugins are not supported at this time.** Download packages from the official plugin downloads page linked below.

Plugins are installed on the Linkr device and managed through **Plugin Center** in the web interface. Some plugins also require additional configuration or a program on the remote computer. See the individual plugin guide for its requirements.

## Prerequisites

- Linkr firmware that supports **Plugin Center**.
- A controlling computer that can access Linkr's web interface and is logged in.
- Enough free storage on Linkr.

## Download Plugins

1. On the controlling computer, open the [official plugin downloads page](https://github.com/radxa-linkr/plugins/releases/latest).
2. Expand **Assets** and download the `.apk` file for the plugin you need. For example, Linkrd package filenames begin with `Linkrd-`.
3. Save the file on the controlling computer for upload in the next step. You do not need to extract or run it on the computer.

Download the plugin `.apk` asset provided by the release; **Source code** archives cannot be installed through Plugin Center. These `.apk` files are Linkr plugin packages. Ordinary Android application packages cannot be used instead.

## Install a Plugin

1. Log in to Linkr's web interface and open **Plugin Center** in the sidebar.
2. Select **Install Plugin Package**, then click the upload area to choose the downloaded `.apk` file, or drag the file into that area. Each file must be within the **100 MB** limit shown in the interface.
3. Wait for the upload to finish, then check the displayed package name, version, architecture, installed size, and description.
4. Click **Install** and wait for installation to succeed. Uploading only transfers the file to Linkr; installation still requires confirmation.
5. After installation, the page switches to **Installed Plugins**. Confirm that the plugin and its version appear in the list, then complete any required configuration and enable it.

If you uploaded the wrong package or do not want to install it, click **Discard** to delete the pending package. This does not uninstall an installed plugin.

## Enable or Disable a Plugin

Find the plugin under **Installed Plugins** and use its switch to control whether it is enabled:

- **On**: Starts the plugin service and enables automatic startup on boot.
- **Off**: Stops the plugin service and disables automatic startup on boot. The plugin remains installed.

Some plugins have a dedicated configuration panel and require configuration before they can be enabled. For example, EasyTier requires a network configuration. Follow the interface prompts and the individual plugin guide.

## Uninstall a Plugin

1. Open **Plugin Center → Installed Plugins**.
2. Find the plugin you want to remove and click **Uninstall**.
3. Check the plugin name in the **Uninstall Plugin** confirmation dialog, then click **Uninstall** again.
4. Wait for the success message and confirm that the plugin no longer appears in the list.

Uninstalling automatically stops the plugin service and disables its automatic startup; you do not need to turn off the switch first. Uninstalling does not necessarily remove all plugin configuration. For example, use **Leave network** in EasyTier before uninstalling if you also want to delete its network configuration.

If you are accessing Linkr remotely through the network plugin you plan to uninstall, switch to another working connection first to avoid losing access.

## Troubleshooting

### Plugin Center is missing

Check whether the current firmware supports Plugin Center. If needed, follow [Firmware Update](../getting-started/firmware-update.md) to upgrade.

### An uploaded plugin does not appear under Installed Plugins

Check whether the **Install Plugin Package** page is still waiting for confirmation. After uploading, click **Install**. The package only appears in the installed list after installation succeeds.

### The package is invalid, unsupported, or fails to install

Confirm that the file is a complete `.apk` plugin package from the official downloads page and is compatible with the current firmware. Follow the error message in the interface. If needed, download and upload the file again, and check the free storage on Linkr.

## Plugin Guides

<DocCardList />
