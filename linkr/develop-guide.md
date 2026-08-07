---
sidebar_position: 99
---

# Developer Documentation

## AI Agent Interface

Remotely automate operations on the controlled machine by calling the HTTP interfaces provided by Radxa Linkr (including screen capture, keyboard, and mouse control).

**For API Token acquisition, refer to the chapter on how to generate an API Token in the Usage Guide.**

### Snapshot Interface

- **URL**: `http://{linkr_ip}/api/public/snapshot`

- **Method**: GET

- **Purpose**: Get the current controlled machine screen status for AI model analysis and decision-making

- **Returns**: JPEG format screen capture

- **Request Example**:

```Plain Text
curl -X GET http://192.168.2.224:80/api/public/snapshot -H "Authorization: token {{your API Token}}" -o screen.jpeg
```

### Control Interface

- **URL**: `http://{linkr_ip}/api/public/control`

- **Method**: POST

- **Purpose**: Send event sequences such as keyboard/mouse, text, delay, etc., to remotely control the controlled machine

- **Request Example**:

```Plain Text
curl -X POST http://192.168.2.224:80/api/public/control \
  -H "Content-Type: application/json" \
  -H "Authorization: token {{your API Token}}" \
  -d '{
    "events": [
      // Control interface event list, each event is an array, the first element indicates the event type
      ["text", "Helloworld"],
      ["delay", 300],
      ["mouse_abs", 0, 0.1, 0.1, 0, 0],
      ["keyboard", "MetaLeft", true],
      ["keyboard", "MetaLeft", false],
      ["mouse_abs", 0, 0.5, 0.5, 0, 0],
      ["mouse_rel", 0, 100, 100, 0, 0]
    ]
  }'
```

- **Response**:

```Plain Text
{
  "code": 0,                       // 0 means success, non-zero means failure
  "data": null,
  "message": "Request succeeded!"  // Returns error message
}
```

## Control Interface Parameter Details

### Keyboard Event

```Plain Text
["keyboard", keyCode, isPressed]
```

**Parameter Description**:

- Index 0: Fixed string `"keyboard"`, indicating pressing or releasing a key on the keyboard.

- Index 1: Field type: String. Indicates the keyboard key identifier, using the Web standard [`KeyboardEvent.code`](https://developer.mozilla.org/en-US/docs/Web/API/UI_Events/Keyboard_event_code_values) value.

- Index 2: Field type: Boolean. Indicates the key state, `true` means pressed, `false` means released.

**Common Key Identifiers**:

- `"MetaLeft"` - Left Meta key (Windows key / Command key)

- `"KeyA"` - A key

- `"KeyB"` - B key

- `"KeyC"` - C key

- `"KeyV"` - V key

- `"Enter"` - Enter key

- `"Escape"` - ESC key

- `"Tab"` - Tab key

- `"Space"` - Space key

- `"ControlLeft"` - Left Ctrl key

- `"AltLeft"` - Left Alt key

- `"ShiftLeft"` - Left Shift key

**Example**:

```Plain Text
["keyboard", "MetaLeft", true],   // Press Windows key
["keyboard", "MetaLeft", false]  // Release Windows key
["keyboard", "KeyR", true],       // Press R key
["keyboard", "KeyR", false],     // Release R key

```

### Absolute Coordinate Mouse Event (mouse_abs)

```Plain Text
["mouse_abs",0,0.1,0.1,0,0],
```

**Parameter Description**:

- Index 0: Fixed string `"mouse_abs"`, indicating the mouse moves in absolute coordinates, with the origin at the top-left corner of the screen, and the horizontal and vertical coordinate ranges [0.00, 1.00].

- Index 1: Field type: Number. Indicates the mouse button. 0: no mouse button pressed or release all mouse buttons. Bit 0 indicates left button, bit 1 indicates right button, bit 2 indicates middle wheel button. When pressing multiple buttons simultaneously, add their corresponding values. For example, pressing left button (1) and right button (2) simultaneously results in 3 (i.e., 1 + 2).

- Index 2: Field type: Number. Indicates the mouse absolute coordinate X (0.00-1.00, origin at top-left corner)

- Index 3: Field type: Number. Indicates the mouse absolute coordinate Y (0.00-1.00, origin at top-left corner)

- Index 4: Field type: Number. Indicates the mouse vertical wheel value. Range [-20, 20]. For example, a positive value (e.g., n) means scrolling the mouse vertically down by n pixels, a negative value (e.g., -n) means scrolling the mouse vertically up by n pixels.

- Index 5: Field type: Number. Indicates the mouse horizontal wheel value. Range [-20, 20]. For example, a positive value (e.g., n) means scrolling the mouse horizontally right by n pixels, a negative value (e.g., -n) means scrolling the mouse horizontally left by n pixels.

**Example**:

```Plain Text
["mouse_abs",0,0.5,0.5,0,0],      // Move mouse to screen center
["mouse_abs",1,0.5,0.5,0,0],      // Move mouse to screen center and click left button
["mouse_abs",0,0.5,0.5,0,0],      // Move mouse to screen center and release the mouse button from the previous operation
["mouse_abs",0,0.5,0.5,20,10],    // Move mouse to screen center, and scroll mouse vertically down 20 pixels and horizontally right 10 pixels.
```

### Relative Coordinate Mouse Event (mouse_rel)

```Plain Text
["mouse_rel",0,100,100,0,0],
```

**Parameter Description**:

- Index 0: Fixed string `"mouse_rel"`, indicating the mouse moves in relative coordinates, with the origin at the top-left corner of the screen, and the movement unit is pixels.

- Index 1: Field type: Number. Indicates the mouse button. 0: no mouse button pressed or release all mouse buttons. Bit 0 indicates left button, bit 1 indicates right button, bit 2 indicates middle wheel button. When pressing multiple buttons simultaneously, add their corresponding values. For example, pressing left button (1) and right button (2) simultaneously results in 3 (i.e., 1 + 2).

- Index 2: Field type: Number. Indicates the relative horizontal movement pixel value of the mouse. A positive value (e.g., n) means moving right by n pixels, a negative value (e.g., -n) means moving left by n pixels.

- Index 3: Field type: Number. Indicates the relative vertical movement pixel value of the mouse. A positive value (e.g., n) means moving down by n pixels, a negative value (e.g., -n) means moving up by n pixels.

- Index 4: Field type: Number. Indicates the mouse vertical wheel value. Range [-20, 20]. For example, a positive value (e.g., n) means scrolling the mouse vertically down by n pixels, a negative value (e.g., -n) means scrolling the mouse vertically up by n pixels.

- Index 5: Field type: Number. Indicates the mouse horizontal wheel value. Range [-20, 20]. For example, a positive value (e.g., n) means scrolling the mouse horizontally right by n pixels, a negative value (e.g., -n) means scrolling the mouse horizontally left by n pixels.

**Example**:

```Plain Text
["mouse_rel",0,10,10,0,0],        // From the current mouse position, translate right and down by 10 pixels each.
["mouse_abs",1,0,0,0,0],          // Click left button at the current mouse position
["mouse_abs",0,0,0,0,0],          // Release the mouse button from the previous operation at the current mouse position
["mouse_abs",0,10,10,20,10],      // From the current mouse position, translate right and down by 10 pixels each, and scroll mouse vertically down 20 pixels and horizontally right 10 pixels.
```

### Text Event (text)

```Plain Text
["text", "text_to_type"]
```

**Parameter Description**:

- Index 0: Fixed string `"text"`, indicating inputting a text string.

- Index 1: Field type: String. Indicates the text string to input, maximum 1024 characters.

Only the following ASCII characters are supported:

- Control characters: **9 (Tab), 10 (Enter)**

- Printable characters: **32 ~ 126**

**Example**:

```Plain Text
["text", "https://www.baidu.com"] // Input https://www.baidu.com at the current cursor position
```

### Delay Event (delay)

```Plain Text
["delay", milliseconds]
```

**Parameter Description**:

- Index 0: Fixed string `"delay"`, indicating pause, ensuring the Linkr completes the previous operation. For example: used to ensure complete input of long text.

- Index 1: Field type: Number. Indicates the pause duration, unit: milliseconds.

**Note**:
A pause event usually needs to be added after a text input event to ensure the Linkr has enough time to process the complete long text input. If the Linkr needs a longer operation, multiple pause events need to be sent. Generally, when the input text length is 30, a 1000 millisecond pause is required.

**Example**:

```Plain Text
["text", "https://www.baidu.com"] // Input https://www.baidu.com at the current cursor position
["delay", 1000]                   // Pause 1000 milliseconds to ensure the above long text output is complete
```
