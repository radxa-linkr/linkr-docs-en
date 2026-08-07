---
id: link-skills
title: Linkr Skills Usage Guide
sidebar_position: 8
---

# Linkr Skills Usage Guide

`linkr-skills` is a standardized skill package for AI Agents (OpenClaw). It calls the standard HTTP interfaces (screen capture, keyboard, mouse, text input) provided by Radxa Linkr to achieve remote automated operations on the controlled machine.

It is suitable for scenarios such as remote server management, automated testing, and unattended operations.

Project source: [linkr-skills](https://github.com/radxa-linkr/linkr-skills)

:::tip

- This skill is based on the Linkr standard HTTP interfaces. For detailed interface protocols and event parameters, please refer to the [Developer Documentation](./develop-guide)
- Related documents: [Access Token](./access-token), [Linkr Web Usage Guide](./usage)

:::

## Features

| Feature | Description |
| :--- | :--- |
| Screen Capture | Get real-time screen image of the controlled machine for AI model analysis and decision-making |
| Mouse Control | Supports both absolute coordinates `[0.00, 1.00]` and relative coordinates (pixels) modes |
| Keyboard Simulation | Complete key press / release control, supports key combinations |
| Text Input | Supports automatic segmentation, pausing 1000ms after every 30 characters to ensure complete input |
| Delay Control | Ensure operation sequences execute in the expected order |

## System Architecture

```text
┌─────────────┐      HTTP API      ┌─────────────┐      KVM Signal      ┌─────────────┐
│   OpenClaw  │ ◄────────────────► │    Linkr    │ ◄──────────────────► │   Target    │
│    (PC)     │                    │             │                      │   Machine   │
└─────────────┘                    └─────────────┘                      └─────────────┘

    HTTP interface (provided by Linkr):
    ├── Screenshot endpoint: /api/public/snapshot
    └── Control endpoint:   /api/public/control
```

## Prerequisites

### 1. Get API Token

Calling the Linkr public API requires an access token (API Key). Please refer to [Access Token](./access-token) to create it in the Linkr web "System Settings → Access Token".

### 2. Configure Environment Variables

Before using this skill, you must set the following environment variables:

- `Linkr_IP`: Linkr device IP (e.g., `192.168.2.224`)
- `Linkr_TOKEN`: API Token

#### Bash

```bash
export Linkr_IP="192.168.x.x"
export Linkr_TOKEN="your_api_token"
```

#### PowerShell

```powershell
[System.Environment]::SetEnvironmentVariable("Linkr_IP", "192.168.x.x", "User")
[System.Environment]::SetEnvironmentVariable("Linkr_TOKEN", "your_api_token", "User")
```

:::warning

- `Linkr_IP` and `Linkr_TOKEN` in the documentation are just variable name descriptions and will not be automatically replaced with real values
- Real values must come from environment variables readable by the OpenClaw runtime
- After modifying environment variables, you need to restart OpenClaw or reopen the terminal before executing

:::

## Install to OpenClaw

```bash
# Copy to OpenClaw skills directory
cp -r linkr-skills ~/.openclaw/skills/

# Verify installation
openclaw skills list
```

### Dependencies

- `curl`: for HTTP requests
- `python3` + `requests`: for Python client (optional)

## API Interfaces

`linkr-skills` calls the following two interfaces. For request methods, parameters, and response descriptions, please refer to [Developer Documentation - AI Agent Interface](./develop-guide).

| Interface | Method | Purpose |
| :--- | :--- | :--- |
| `/api/public/snapshot` | GET | Get real-time screen capture (JPEG) of the controlled machine |
| `/api/public/control` | POST | Send event sequences such as keyboard/mouse, text, and delay |

```bash
# Screenshot
curl -X GET "http://${Linkr_IP}:80/api/public/snapshot" -H "Authorization: token ${Linkr_TOKEN}" -o screen.jpeg

# Control
curl -X POST "http://${Linkr_IP}:80/api/public/control" \
  -H "Content-Type: application/json" \
  -H "Authorization: token ${Linkr_TOKEN}" \
  -d '{"events": [["text", "hello"], ["delay", 300]]}'
```

## Event Type Quick Reference

Each event is an array whose first element indicates the event type. For detailed parameter explanations and examples of each event, please refer to [Developer Documentation - Control Interface Parameter Details](./develop-guide).

| Event | Format | Description |
| :--- | :--- | :--- |
| Keyboard | `["keyboard", "KeyA", true]` | Press / release key |
| Mouse Absolute | `["mouse_abs", 0, 0.5, 0.5, 0, 0]` | Move to absolute screen coordinates (0.00-1.00) |
| Mouse Relative | `["mouse_rel", 0, 100, 100, 0, 0]` | Move relative to current position by specified pixels |
| Text | `["text", "hello"]` | Input text at current cursor position |
| Delay | `["delay", 1000]` | Pause for specified milliseconds |

:::warning

- A pause event **must** be added after a text input event to ensure complete input of long text
- For text length of about 30 characters, it is recommended to pause for **1000ms**
- Long text must be input in segments, pausing once after every 30 characters

:::

## Complete Example: Using in OpenClaw

Directly input natural language instructions in the OpenClaw conversation, and the AI Agent will automatically load the `linkr-skills` skill, translate the instructions into event sequences, and send them to the controlled machine.

**User Input**:

```text
Open Chrome browser and visit https://radxa.com
```

**Agent Execution Flow**:

1. Load the `linkr-skills` skill and read the environment variables `Linkr_IP` and `Linkr_TOKEN`
2. Call the screenshot interface to confirm the current screen state of the controlled machine
3. Generate event sequences and send them via the control interface

**Event sequences sent**:

```json
{
  "events": [
    ["keyboard", "MetaLeft", true],
    ["keyboard", "KeyR", true],
    ["delay", 50],
    ["keyboard", "KeyR", false],
    ["keyboard", "MetaLeft", false],
    ["delay", 500],
    ["text", "chrome"],
    ["delay", 300],
    ["keyboard", "Enter", true],
    ["keyboard", "Enter", false],
    ["delay", 3000],
    ["mouse_abs", 0, 0.5, 0.08, 0, 0],
    ["delay", 200],
    ["text", "https://radxa.com"],
    ["delay", 1000],
    ["keyboard", "Enter", true],
    ["keyboard", "Enter", false]
  ]
}
```

**Step Breakdown**:

1. Press `Win+R` to open the Run dialog
2. Enter `chrome` and press Enter to launch the browser
3. Wait 3 seconds for the browser to finish launching
4. Move the mouse to the address bar (top center position)
5. Enter `https://radxa.com`
6. Pause 1000ms to ensure complete text input
7. Press Enter to navigate to the page

## Helper Scripts

`linkr-skills` provides both Bash and Python helper scripts for quick calling.

### Bash Quick Call

```bash
# Send control command
./scripts/send_control.sh '{"events":[["text","hello"],["delay",300]]}'

# Get screenshot
curl -X GET "http://${Linkr_IP}:80/api/public/snapshot" -H "Authorization: token ${Linkr_TOKEN}" -o screen.jpeg
```

### Python Client (Optional)

```python
from scripts.linkr_client import LinkrClient

client = LinkrClient()

# Get screenshot
client.screenshot("desktop.jpeg")

# Input text (auto-segment: pause 1000ms after every 30 characters)
client.text("This is a long text that will be automatically split into chunks...")

# Key combination Win+R
client.key_combo("MetaLeft", "KeyR")

# Click screen center
client.click(0.5, 0.5)
```

`linkr_client.py` also supports direct command-line invocation:

```bash
# Input text
python linkr_client.py text "Hello World"

# Run command via Win+R
python linkr_client.py run notepad

# Click specified position (absolute coordinates 0-1)
python linkr_client.py click 0.5 0.5

# Send key combination
python linkr_client.py combo MetaLeft KeyR
```

## Best Practices

### 1. Coordinate Positioning

- Prefer `mouse_abs` (absolute coordinates), range `[0.00, 1.00]` adapts to different resolutions
- Take a screenshot before critical operations to confirm the current screen state
- Use AI visual analysis for UI element positioning

### 2. Timing Control (Important)

| Scenario | Recommended Delay | Description |
| :--- | :--- | :--- |
| After short text input (less than 10 characters) | 300ms | Simple text |
| After medium text input (10-30 characters) | 500-800ms | e.g., URL |
| **After long text input (about 30 characters)** | **1000ms** | Required, ensure complete input |
| After launching application | 2000-5000ms | Depends on app launch time |
| After page load | 1000-3000ms | Depends on network condition |
| Between consecutive keystrokes | 50-100ms | Prevent key loss |

### 3. Long Text Input Strategy

Text exceeding 30 characters must be input in segments:

```json
{
  "events": [
    ["text", "This is a long text that needs"],
    ["delay", 1000],
    ["text", " to be split into multiple parts"],
    ["delay", 1000],
    ["text", " to ensure complete input."],
    ["delay", 1000]
  ]
}
```

When using the Python client, `client.text()` automatically segments, no manual handling needed.

### 4. Keystroke Operation Rules

- Press and release must appear in pairs: `[key, true]` and `[key, false]`
- Modifier keys (Ctrl/Alt/Shift/Win) pressed first, then the main key
- Release order is reversed: release the main key first, then the modifier keys

## Troubleshooting

| Phenomenon | Possible Cause | Solution |
| :--- | :--- | :--- |
| Screenshot failed | Network issue / Linkr not running | Check `Linkr_IP` connectivity |
| Control no response | Incorrect event format | Check JSON array length and types |
| Inaccurate coordinates | Resolution change | Use `mouse_abs` absolute coordinates `[0.00, 1.00]` |
| Garbled text | Wrong input method state | Switch to English input method first |
| Incomplete text input | Insufficient delay | Add 1000ms pause after every 30 characters |
| Operation order messed up | Insufficient delay | Increase `delay` duration |
| Long text truncated | Buffer overflow | Segment input every 30 characters |
