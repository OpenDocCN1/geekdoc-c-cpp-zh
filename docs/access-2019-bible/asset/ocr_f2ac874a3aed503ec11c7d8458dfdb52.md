# TABLE 26.2 Essential Form Events

| Event | When the Event Is Triggered |
|---|---|
| Open | When a form is opened, but the first record is not yet displayed |
| Load | When a form is loaded into memory |
| Resize | When the size of a form changes |
| Unload | When a form is closed and the records unload, but before the form is removed from the screen |
| Close | When a form is closed and removed from the screen |
| Activate | When an open form receives the focus, becoming the active window |
| Deactivate | When a different window becomes the active window, but before the current window loses focus |
| GotFocus | When a form with no active or enabled controls receives the focus |
| LostFocus | When a form loses the focus |
| Timer | When a specified time interval passes; the interval (in milliseconds) is specified by the Timer Interval property |
| BeforeScreenTip | When a ScreenTip is activated |

# Form mouse and keyboard events

Access forms also respond to a number of mouse and keyboard events, as shown in Table 26.3.

# TABLE 26.3 Form Mouse and Keyboard Events

| Event | When the Event Is Triggered |
|---|---|
| Click | When the user presses and releases (clicks) the left mouse button |
| DblClick | When the user presses and releases (clicks) the left mouse button twice on a form |
| MouseDown | When the user presses the mouse button while the pointer is on a form |
| MouseMove | When the user moves the mouse pointer over an area of a form |
| MouseUp | When the user releases a pressed mouse button while the pointer is on a form |
| MouseWheel | When the user spins the mouse wheel |
| KeyDown | When the user presses any key on the keyboard when a form has focus or when the user uses a SendKeys macro action |
| KeyUp | When the user releases a pressed key or immediately after the user uses a SendKeys macro action |
| KeyPress | When the user presses and releases a key on a form that has the focus or when the user uses a SendKeys macro |