# Overview of UWP apps

The device revolution established new ways of obtaining and running software. Mobile devices normally get their applications from a central store, with automatic installation and updates, all with little user intervention. Once a user selects an app from the store, she can see the permissions the app requires to function correctly. These permissions are called capabilities and are declared as part of the package when it's submitted to the store. This way, the user can decide whether these capabilities are acceptable.

Figure 7-16 shows an example of a capabilities list for a UWP game (Minecraft, Windows 10 beta edition). The game requires internet access as a client and as a server to the local home or work network. Once the user downloads the game, she implicitly agrees the game may exercise these capabilities. Conversely, the user can be confident that the game uses only those capabilities. There is no way the game could use other capabilities, such as accessing the camera, on the device.

![](bbox=[0.166, 0.311, 0.918, 0.696])

**FIGURE 7-16** Part of an app's page in the store, showing capabilities,among other things.

To get a sense of the differences between UWP apps and desktop (classic) apps at a high level, consult Table 7-12. From a developer's perspective, the Windows platform can be seen as shown in Figure 7-17.