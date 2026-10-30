![](bbox=[0.22, 0.12, 0.78, 0.32])

Figure 6.30 Osp::System consists of a group of self-contained utility classes.

Using the PowerManager class you can implement and register listeners to be notified when the screen switches on or off (IScreenEventListener) or when the charging state of the device changes (IChargingEventListener). PowerManager also includes the KeepScreenOnState method, which can be used to keep the screen on until the application is sent to the background. This is useful when using features such as media players or the camera.

# Osp::Telephony

# Declared In:

FTelephony.h

# Library:

FTelephony

# Privileges Required:

To use the features of this namespace you need the following privilege group:

| Privilege group | Privilege level | Description |
|---|---|---|
| TELEPHONY | NORMAL | Getting network and SIM information |

# Summary

Selected important classes:

+   - CallManager
+   - NetworkManager
+   - SimInfo

This namespace provides classes to access the telephony features of the device and contains methods for getting information about the current call and network information, and access to information from the SIM card (see Figure 6.31).