+   - The KeyDown and KeyPress events are not same as they are fired at different points in the keyboard event stream and contain different information in the EventArgs object.
+   - The KeyEventArgs event data associated with the KeyDown and KeyUp events provides low-level information about the keystroke.
+   - This information is used to determine, if an upper - or lowercase character was pressed. It also tells if any modifier keys (Alt, Ctrl, or Shift) were pressed along with it in combination.

# 2. KeyEventArgs properties (KeyDown and KeyUp)

| Property | Data type | Description |
|---|---|---|
| Alt | Boolean | Read-only value indicating if the Alt key was pressed. `true` if pressed, `false` otherwise. |
| Control | Boolean | Read-only value indicating if the Ctrl key was pressed. `true` if pressed, `false` otherwise. |
| Shift | Boolean | Read-only value indicating if the Shift key was pressed. `true` if pressed, `false` otherwise. |
| Modifiers | Keys | Read-only flags indicating the combination of modifier keys (Alt, Ctrl, Shift) pressed. Modifier keys can be combined using the bitwise OR operator. |
| Handled | Boolean | Value indicating if the event was handled. `false` until set otherwise. |
| KeyCode | Keys | Read-only value containing the key code for the key pressed. Typical values include the A key, Alt, and BACK (backspace). |
| KeyData | Keys | Read-only value containing the key code for the key pressed, combined with modifier flags to indicate combination of modifier keys (Alt, Ctrl, Shift). |
| KeyValue | integer | Key code property expressed as a read-only integer. |

# 3. Unicode and ASCII Characters

+   - Each character in the American Standards Committee for Information Interchange (ASCII) character set is represented by a single byte (8 bits) of data, representing 256 characters. The first 128 characters (represented by 7 bits) are standardized and usually referred to as low-order ASCII characters. The upper 128 characters are not standardized, although many well established character sets use all 256 characters.