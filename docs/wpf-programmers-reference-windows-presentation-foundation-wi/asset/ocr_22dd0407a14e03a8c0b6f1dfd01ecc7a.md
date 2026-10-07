When the user opens the Data menu, the mnuData_SubmenuOpened event handler executes. It searches a data directory and adds menu items to this menu list network data files that the user might to load.

The Show Costs item is clickable and initially checked. When the user checks it, the menuDataShowCosts_Checked event handler executes and replays the current network with costs displayed. When the user unchecks this menu, the mnuDataShowCosts_Unchecked event handler executes and replays the current network with costs hidden.

# PASSWORDBOX

The PasswordBox is a textbox that hides its text on the screen, displaying a dot, asterisk, or other character for each character typed (see Tables D-20 and D-21).

TABLE D-20: Key Properties of PasswordBox

| PROPERTY | PURPOSE |
|---|---|n| Password | Determines the current password in plaintext. |
| PasswordChar | Determines the character displayed on the screen for each character entered in the PasswordBox. |
| SecurePassword | Returns the current password as a SecureString. |

TABLE D-21: Key Events for PasswordBox

| EVENT | PURPOSE |
|---|---|n| PasswordChanged | Occurs when the password changes. |

# EXAMPLE Using Password

The following code creates two PasswordBoxes. The first uses the default font and PasswordChar so it displays a filled circle for each character. The second uses the Wingdings font with PasswordChar = N so it displays little skulls and bones.

```
<PasswordBox Password="Secret" />
<PasswordBox Password="Secret" FontFamily="Wingdings" PasswordChar="N" />
```