---
sidebar_position: 1
doc_kind: page
title: "Linkrd Clipboard Sync"
description: "Install the Linkrd plugin and remote program, grant browser permissions, and synchronize text clipboards in both directions."
locale: en
product: linkr
task_type: install
last_verified: 2026-10-21
source_of_truth: local
---

# Linkrd Clipboard Sync

Linkrd synchronizes plain-text clipboards in both directions between the controlling computer and the remote computer, so you can copy on one computer and paste directly on the other.

Install the **Linkrd plugin** on Linkr and the **Linkrd program** on the remote computer. Currently, only plain text is supported; images and files are not synchronized.

## Prerequisites

- Linkr firmware that supports Linkrd, and a compatible `.apk` plugin package.
- A data-capable USB cable connecting Linkr's **USB-C device port** to the remote computer. See [Hardware Interfaces](../getting-started/hardware-interface.md).
- A remote computer running Windows x64, or Linux x64 / ARM64 with an X11 or Wayland desktop session.
- A browser on the controlling computer that supports clipboard reading and writing, connected to Linkr over **HTTPS**, with clipboard access allowed for the site.

:::tip

The controlling computer opens Linkr's web interface. The remote computer connects to Linkr through HDMI and USB. Install the Linkrd program on the remote computer.

The browser must trust Linkr's HTTPS certificate. A custom certificate must cover the hostname or IP address used to access Linkr. For a certificate issued by a local CA, trust that CA's root certificate on the controlling computer. Bypassing a certificate warning does not establish browser trust.

:::

## 1. Install the plugin on Linkr

1. Log in to Linkr's web interface and open **Plugin Center**.
2. Under **Install Plugin Package**, upload the Linkrd `.apk` file.
3. After uploading, check that the package name is **Linkrd**, then click **Install**.
4. Enable Linkrd under **Installed Plugins**.

The plugin provides `Linkrd.img`, which contains the installers for the remote computer. Installing the plugin alone does not install the remote program; continue with the next section.

## 2. Install the program on the remote computer

### Open the installation disk

1. In Linkr's web interface, go to **Keyboard & Mouse → Quick Paste → Clipboard sync** and turn on **Clipboard sync**. This enables USB ACM serial communication.
2. Open **Virtual Devices → Virtual Disk**, find `Linkrd.img`, and mount it.
3. On the remote computer, open the drive labeled **LINKRD** and select the folder for its operating system and processor.

| Remote computer | Folder | Installer |
| --- | --- | --- |
| Windows x64 | `windows-x64` | `install.cmd` |
| Linux x64 | `linux-x64` | `install.sh` |
| Linux ARM64 | `linux-arm64` | `install.sh` |

The installation disk currently does not include a macOS version of Linkrd.

### Windows

1. Copy the entire `windows-x64` folder to a local disk on the remote computer.
2. Double-click `install.cmd` and follow the prompts. Administrator privileges are not required.

Installation starts the program immediately in the background and enables automatic startup at the current user's next login. The default installation path is `%LOCALAPPDATA%\Programs\linkrd\linkrd.exe`.

### Linux

Open a terminal in the remote computer's logged-in desktop session and enter the `linux-x64` or `linux-arm64` folder on the installation disk. Copy the entire folder to a local temporary directory under your home directory, then grant execution permission to the copied installer and program before installing:

```bash
linkrd_install_dir=$(mktemp -d -p "$HOME")
cp -R . "$linkrd_install_dir/"
cd "$linkrd_install_dir"
chmod u+x install.sh linkrd
./install.sh
```

Set execution permissions in the local copy. Do not run `chmod` directly on the **LINKRD** virtual disk.

Run the script as your normal desktop user. **Do not run the installer as root or through `sudo`.** The script checks serial port access. If your user needs membership in `dialout` or `uucp`, it prompts for your `sudo` password and refreshes group permissions for the installer.

If prompted, log out of the desktop, log back in, and run the script again. Ask an administrator for help if `sudo` access is unavailable, the device belongs to an unexpected group, or access is still denied.

Installation starts the program immediately in the background and enables automatic startup at the current user's next login. The default installation path is `~/.local/bin/linkrd`.

:::tip

The installation scripts and the README on the disk are in English. Both Windows and Linux scripts call the program's built-in `install --autostart` command.

After installation, you can unmount `Linkrd.img` in Linkr's virtual disk settings. Synchronization uses the installed program and does not require the installation disk to remain mounted.

:::

## 3. Enable two-way sync

1. Return to **Keyboard & Mouse → Quick Paste → Clipboard sync**.
2. Confirm that **Clipboard sync** is enabled and the status changes to **Remote computer connected**.
3. Enable **Automatic two-way sync**. Allow clipboard access if the browser requests it.
4. Keep the Linkr page visible and focused, then copy new text to synchronize it.

The three switches have different purposes:

| Switch | Purpose |
| --- | --- |
| Linkrd plugin | Controls whether `Linkrd.img` appears in the virtual disk list. Also available in Plugin Center. |
| Clipboard sync | Enables USB ACM and clipboard communication with the remote computer. |
| Automatic two-way sync | Automatically synchronizes text changes between the two computers. Requires browser clipboard permission. |

Automatic sync handles new changes after it is enabled. After reconnecting, it does not automatically resend old text from before the disconnection. Sync pauses when you switch tabs, minimize the browser, or the page loses focus. After returning to the page, copy the desired text again if needed to ensure it is synchronized.

## 4. Verify synchronization

### Controlling computer to remote computer

1. Copy some new text on the controlling computer, such as `Hello Linkrd`.
2. Return to the Linkr page and give it focus.
3. Paste into a text editor on the remote computer and check that the text matches.

### Remote computer to controlling computer

1. Copy different new text on the remote computer.
2. Keep the Linkr page visible and focused. Check that the text appears under **Remote clipboard**.
3. Paste into a text editor on the controlling computer and check that the text matches.

## Manual sync

With a connection established, you can synchronize text manually without enabling automatic sync:

- **Send to the remote computer:** Type or paste text under **Send text**, click **Sync to remote**, then paste on the remote computer. You can also click **Paste local text** to read the controlling computer's clipboard.
- **Copy to the controlling computer:** View text under **Remote clipboard**, click **Copy to local**, then paste on the controlling computer.

If browser clipboard access is unavailable, copy and paste manually in the text fields. Shorten the text if it exceeds the byte limit shown in the interface. **Sending empty text clears the remote text clipboard.**

The existing **Keyboard input** mode remains available independently.

## Manage the remote program

The installer configures PATH for the current user. Follow its output and open a new terminal before running these commands:

| Command | Purpose |
| --- | --- |
| `linkrd status` | Show whether the current user's process is running and its PID. |
| `linkrd --list-ports` | List detected serial ports. |
| `linkrd stop` | Stop Linkrd for the current user. |
| `linkrd start` | Start in the background using saved arguments. |
| `linkrd autostart status` | Show login autostart registration status. |
| `linkrd autostart disable` | Disable startup at the next login without stopping the current process. |
| `linkrd autostart enable` | Enable startup at the next login. |

`linkrd status` checks the process only, not USB or clipboard connectivity. Check for **Remote computer connected** in Linkr to confirm the clipboard connection.

To uninstall, run these commands on the remote computer, then remove the plugin from Linkr's Plugin Center if no longer needed:

```bash
linkrd stop
linkrd uninstall
```

Uninstalling removes the program and login autostart entry but retains logs.

## Troubleshooting

### Linkrd.img is missing

Confirm that **Linkrd** is installed and enabled in Plugin Center, then refresh the virtual disk list. Enabling **Clipboard sync** alone does not make the installation image appear.

### The status stays at "Enabled, waiting for the remote computer"

- Check that Linkr's USB-C device port connects to the remote computer with a data-capable cable.
- Confirm the remote program is installed. Run `linkrd status` to check the process, or `linkrd start` if it is stopped.
- Run `linkrd --list-ports` and check that the serial device is detected.
- On Linux, run the program in the logged-in X11 / Wayland desktop session and confirm that your user has read/write access to the serial device.

### Linux reports Permission denied

If changing execution permissions or running the program fails on the **LINKRD** virtual disk, follow the Linux installation steps above. Copy the entire folder for your architecture to a local temporary directory, run `chmod u+x install.sh linkrd` in the copied folder, then run `./install.sh`.

If access to the serial port is denied, check the actual device name and the current session's groups on the remote computer, for example:

```bash
ls -l /dev/ttyACM0
id -nG
```

Run the installer again and follow its authorization or desktop logout/login instructions. If group membership is correct but access is still denied, ask an administrator to check device permissions or ACLs.

### Remote text appears, but local text does not sync

Confirm that **Automatic two-way sync** is enabled, then check:

- The connection uses HTTPS, the browser trusts the certificate, and the certificate covers the hostname or IP address in use.
- Clipboard access is allowed in the browser's site settings. Check these settings even if no permission prompt appeared.
- The Linkr tab is visible and focused.
- You copied new text after enabling automatic sync, rather than relying on existing clipboard contents.

If automatic sync still fails, test manual sending with **Send text → Sync to remote**.

### A manual send times out or the connection drops

Refresh the connection status and check the current clipboard contents on both computers. A timeout does not prove that the text was not written. Check the contents before deciding whether to send again.
