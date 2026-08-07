---
sidebar_position: 5
---

# Access Token

Radxa Linkr provides an **Access Token** feature for programmatically accessing some of the Linkr's capabilities via API without a web login session. It is suitable for scenarios such as automation scripts, monitoring integration, and third-party tool calls.

The access token is equivalent to an API key, which can be used to call the device's public API interfaces after creation.

## Feature Overview

| Capability | Description |
| ------------ | ------------------------------------------------------ |
| Web Interface Management | Create, view name, and delete access tokens in System Settings |
| Password Verification | Entering the Linkr login password is required to generate a new token, preventing unauthorized creation |
| One-time Display | The token plaintext is only shown once upon successful creation and cannot be viewed again after closing the dialog |
| Persistent Storage | The token is stored in the device's local configuration and remains valid after restart until manually deleted |

## Applicable Scenarios

- **Remote Screenshot**: Periodically capture the Linkr's current screen snapshot for monitoring or inspection
- **Remote Control**: Send control commands via API (keyboard, mouse, etc.)
- **Automation Integration**: Integrate the Linkr into CI/CD, O&M platforms, or custom scripts

:::caution Security Note
The access token has API access permissions comparable to its creator. Please keep it safe and never commit it to a public code repository or share it with untrusted parties. If a token is leaked, delete it immediately in the management interface and regenerate it.
:::

## Operation Steps

### 1. Enter System Settings

1. Open the Linkr management web interface and log in.
2. Click **System Settings** (gear icon) in the left sidebar.
3. Find the **Access Token** collapsible panel.

### 2. Generate a New Token

1. Click the **+ Generate** button to bring up the "Access Token" dialog.
2. Fill in the **Key Name** (required):
   - Only English letters `a-z`, digits `0-9`, and hyphen `-` are allowed
   - Must start with a letter or digit, cannot start or end with `-`
   - Maximum 20 characters
   - Examples: `monitor-script`, `ci-deploy-01`
3. Fill in the **User Password** (required): Enter the login password of the current Linkr management account for identity verification.
4. Click the green **Generate** button.

### 3. Save the Token

After successful generation, the dialog displays the complete access token string (prefixed with `radxa_linkr_`).

1. Click the **Copy** icon on the right side of the token to save it to a secure location (password manager, secrets management system, etc.).
2. After confirming it is safely saved, close the dialog.

:::warning Important
The token plaintext **is only displayed once at creation**. After closing the dialog, neither the interface nor the API can retrieve the complete token content again. If the token is lost, you can only delete the old entry and regenerate it.
:::

### 4. Manage Existing Tokens

In the **Access Token** panel, created tokens are displayed as a list of **Key Names**:

- The list **does not display** the token plaintext, only the name for easy identification of purpose.
- Click the **Delete** icon on the right side of the entry, and confirm to revoke the token, which takes effect immediately.

## Using Access Token to Call API

### Authentication Method

Carry the access token in the HTTP request header:

```text
Authorization: token <your access token>
```

Example:

```bash
curl -H "Authorization: token radxa_linkr_xxxxxxxx" \
  https://<kvm-ip>/api/public/snapshot \
  --output snapshot.jpg
```

Replace `<kvm-ip>` with the actual IP address or domain name of the Linkr (local LAN IP, Tailscale IP, etc. are all acceptable).

### Available Public APIs

The public interfaces that currently support authentication via access token are as follows:

| Interface | Method | Description |
| ---------------------- | ---- | ---------------------------------------- |
| `/api/public/snapshot` | GET | Get a JPEG screenshot of the current screen |
| `/api/public/control` | POST | Send remote control commands (request body is control protocol data) |

#### Get Screenshot Example

```bash
curl -H "Authorization: token radxa_linkr_xxxxxxxx" \
  "https://192.168.1.100/api/public/snapshot" \
  -o snapshot.jpg
```

On success, image/jpeg format image data is returned.

#### Send Control Command Example

```bash
curl -X POST \
  -H "Authorization: token radxa_linkr_xxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '<control data>' \
  "https://192.168.1.100/api/public/control"
```

The format of the control data depends on the Linkr control protocol. For specific fields, please refer to the API documentation or integration SDK.

### Authentication Failure

If `403 No Permission` is returned, please check:

- Whether the `Authorization` header format is `token <token>` (note there is a space between `token` and the token)
- Whether the token is complete and not truncated
- Whether the token has been deleted
- Whether the Linkr device IP or network is reachable

## Token Format Description

- **Prefix**: `radxa_linkr_`
- **Body**: Base64 URL-encoded random string (about 86 characters)
- **Example**: `radxa_linkr_-yDJ3JYDST0BygX5ltq1aFfOom0imn6hnfLTrl4-fDgHTkO8Uk0vdkf_Gxuia_T-fn07GJmZ_MDvhRLnLQ73WA`

Each token's name must be unique on the device and cannot be created with the same name repeatedly.

## Security Recommendations

1. **Least Privilege Principle**: Create tokens with different names for different purposes for easy individual revocation.
2. **Regular Rotation**: It is recommended to delete old tokens and regenerate them regularly, especially after personnel changes or script migrations.
3. **Secure Storage**: Use environment variables or a secrets management tool to store tokens, do not hardcode them in source code.
4. **HTTPS Access**: In production environments, it is recommended to access the Linkr API via HTTPS to avoid token interception during transmission.
5. **Revoke Promptly**: If leakage or no longer in use is discovered, immediately delete the corresponding token in System Settings.

## FAQ

### "Name Format Error" Prompt

The key name does not meet the rules. Please confirm:

- Only contains `a-z`, `0-9`, and `-`
- Starts with a letter or digit
- Does not end with `-`

### Wrong Password Prompt

The user password entered when generating the token is inconsistent with the Linkr login password. Please use the correct password of the current management account.

### Name Already Taken Prompt

Two tokens with the same name cannot be created on the same device. Please change the key name, or delete the old token with the same name first.

### Copy Failed

If the browser does not support the Clipboard API (e.g., non-HTTPS and non-localhost environment), please manually select the token text to copy.

### Script Still Reports 403 After Deleting Token

The deletion takes effect immediately. Please update the script or environment with a new token, or regenerate and configure it.
