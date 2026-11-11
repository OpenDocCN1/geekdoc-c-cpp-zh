The buttons at the bottom depend on the dialog type and the *option type*. When calling `showMessageDialog` and `showInputDialog`, you get only a standard set of buttons (OK and OK/Cancel, respectively). When calling `showConfirmDialog`, you can choose among four option types:

```
```
DEFAULT_OPTION
YES_NO_OPTION
YES_NO_CANCEL_OPTION
OK_CANCEL_OPTION
```
```

With the `showOptionDialog` you can specify an arbitrary set of options. You supply an array of objects for the options. Each array element is rendered as follows:

|  |  |
|---|---|
| `String` | Make a button with the string as label |
| `Icon` | Make a button with the icon as label |
| `Component` | Show the component |
| `Any other object` | Apply `toString` and make a button with the resulting string as label |

The return values of these functions are as follows:

|  |  |
|---|---|
| `showMessageDialog` | None |
| `showConfirmDialog` | An integer representing the chosen option |
| `showOptionDialog` | An integer representing the chosen option |
| `showInputDialog` | The string that the user supplied or selected |

The `showConfirmDialog` and `showOptionDialog` return integers to indicate which button the user chose. For the option dialog, this is simply the index of the chosen option or the value `CLOSED_OPTION` if the user closed the dialog instead of choosing an option. For the confirmation dialog, the return value can be one of the following:

```
```
OK_OPTION
CANCEL_OPTION
YES_OPTION
NO_OPTION
CLOSED_OPTION
```
```

This all sounds like a bewildering set of choices, but in practice it is simple. Follow these steps:

+   1. Choose the dialog type (message, confirmation, option, or input).
+   2. Choose the icon (error, information, warning, question, none, or custom).
+   3. Choose the message (string, icon, custom component, or a stack of them).
+   4. For a confirmation dialog, choose the option type (default, Yes/No, Yes/No/Cancel, or OK/Cancel).