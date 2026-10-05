# TABLE 7-14 Package flags

| Flag | Meaning |
| PSM_ACTIVATION_TOKEN_PACKAGED_APPLICATION (0x1) | This indicates that the AppContainer UWP is stored in AppX packaged format. This is the default. |
| PSM_ACTIVATION_TOKEN_SHARED_ENTITY (0x2) | This indicates that token is being used for multiple executables all of the same AppX packaged UWP application. |
| PSM_ACTIVATION_TOKEN_FULL_TRUST (0x4) | This indicates that this AppContainer is used to host a Project Centennial (Windows Bridge for Desktop) converted Win32 application. |
| PSM_ACTIVATION_TOKEN_NATIVE_SERVICE (0x8) | This indicates that this AppContainer token is used to host a packaged service created by the Service Control Manager (SCM)'s Resource Manager. See Chapter 9 in Part 2 for more information on services. |
| PSM_ACTIVATION_TOKEN_DEVELOPMENT_APP (0x10) | This indicates that this is an internal development application. Not used on retail systems. |
| BREAKAW_INHIBITED (0x20) | The package cannot create a process that is not itself packaged as well. This is set by using the PROC_THREAD_ATTRIBUTE_DESKTOP_POLICY_ATTRIBUTE process-creation attribute. (See Chapter 3 for more information.) |

# EXPERIMENT: Viewing UWP process information

There are several ways to look at UWP processes, some more obvious than others. Process Explorer can highlight processes that use the Windows Runtime in color (cyan by default). To see this in action, open Process Explorer, open the **Options** menu, and **Configure Colors**. Make sure the **Immersive Processes** check box is selected.

![](bbox=[0.176, 0.636, 0.403, 0.901])