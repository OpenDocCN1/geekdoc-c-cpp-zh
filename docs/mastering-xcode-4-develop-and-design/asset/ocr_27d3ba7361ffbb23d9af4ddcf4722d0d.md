![](bbox=[0.282, 0.171, 0.6, 0.257])

# ACTIVATING ENTITLEMENTS AND SANDBOXING

You can turn on entitlements for your app by selecting the Enable Entitlements check box at the top of the list. You then choose an entitlements file from the Entitlements File pop-up. Xcode helpfully creates one matching the name of your target and adds it to your project (Figure 14.42). The file is a simple preference list. You can edit it by selecting it using the same preference list editor you’ve used elsewhere, but it is easier to use the Entitlements section you’re exploring now.

To sandbox your application, select the App Sandbox check box. Now you must grant your application access to the functionality it needs.

# SETTING SPECIFIC ENTITLEMENTS

The remaining settings in the Entitlements section grant specific entitlements to your application.

# FILE SYSTEM

Use the File System pop-up to allow your application to read and write, to read-only, or to have no access to the file system. Select the Allow Downloads Folder Access check box to grant access to the Downloads folder regardless of the general file system access setting. File system access is disallowed by default.

# NETWORK

Use the Network check boxes to allow incoming or outgoing connections. Network communication is disallowed by default.

# HARDWARE

Use the Hardware controls to allow access to cameras, microphones, USB devices, and printers attached to or accessible by the system. None of these are allowed by default.