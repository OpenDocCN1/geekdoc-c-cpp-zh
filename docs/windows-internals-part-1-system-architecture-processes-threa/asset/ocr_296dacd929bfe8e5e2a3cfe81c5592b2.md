# TABLE 7-18 UAC options

| Slider Position | When administrative user not running with administrative rights... | Remarks |
|---|---|---||
| Highest position (Always Notify) | ...attemts to change Windows settings (for example, use certain Control Panel apps) | ...attempts to install software or run a program whose manifest calls for elevation, or use Run as Administrator | This was the Windows behavior. |
| Second position | UAC elevation occurs automatically with no prompt or notification. | UAC elevation prompt appears on the Secure Desktop. | Windows default setting. |
| Third position | UAC elevation occurs automatically with no prompt or notification. | UAC elevation prompt appears on the user's normal desktop. | Not recommended. |
| Lowest position (Never Notify) | UAC is turned off for administrative users. | UAC is turned off for administrative users. | Not recommended. |

The lowest position is strongly discouraged because it turns UAC off completely as far as administrative accounts are concerned. All processes run by a user with an administrative account will run with the user's full administrative rights in effect; there is no admin token. Registry and system virtualization are disabled for these accounts, and the Protected mode of Internet Explorer is disabled. However, virtualization is still in effect for non-administrative accounts, and non-administrative accounts will still be OTS elevation prompt when they attempt to change Windows settings, run a program that requires elevation, or use the Run as Administrator menu option in Explorer.

The UAC setting is stored in four values in the registry under HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System, which are seen in Table 7-19. ConsentPromptBehavior controls the UAC elevation prompt for administrators running with a filtered admin token, and ConsentPromptBehavior controls the UAC prompt for users other than administrators.

# TABLE 7-19 UAC values

| Slider Position | ConsentPromptBehavior | ConsentPromptBehaviorUser | EnableLUA | PromptOnSecureDesktop |
|---|---|---|---||
| Highest position (Always Notify) | 2 (display UAC elevation prompt) | 3 (display OTS UAC elevation prompt) | 1 (enabled) | 1 (enabled) |
| Second position | 5 (display UAC elevation prompt, except for changes to Windows settings) | 3 | 1 | 0 (disabled; UAC prompt appears on user's normal desktop) |
| Third position | 0 | 3 | | 0 |
| Lowest position (Never Notify) | 0 | 3 | 0 (disabled; logins to administrative accounts do not create a restricted admin access token) | 0 |

734 CHAPTER 7 Security