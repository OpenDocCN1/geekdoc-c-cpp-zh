> **NOTE** *For a more detailed look at how you can test your application on a real device, refer to Appendix E.*

# Uninstalling Applications from the iPhone Simulator

The user domain of the iPhone OS file system for the iPhone Simulator is stored in the `~/Library/Application Support/iPhone Simulator/User/` folder.

> **NOTE** *The `~/Library/Application Support/iPhone Simulator/User/` folder is also known as the `<iPhoneUserDomain>`.*

All third-party applications are stored in the `<iPhoneUserDomain>/Applications/` folder. When an application is deployed onto the iPhone Simulator, an icon is created on the Home screen (shown on the left in Figure 1-9) and a file and a folder are created within the `Applications` folder (shown on the right in Figure 1-9).

![](bbox=[0.15, 0.62, 0.9, 0.78])

FIGURE 1-9

To uninstall (delete) an application, execute the following steps:

+   1. Click and hold the icon of the application in the Home screen until all the icons start wriggling. Observe that all the icons now have an "x" button displayed on their top left corners.
+   2. Click the x button (see Figure 1-10) next to the icon of the application you want to uninstall.
+   3. An alert window appears asking if you are sure you want to delete the icon. Click Delete to confirm the deletion.

![](bbox=[0.75, 0.78, 0.95, 0.94])

FIGURE 1-10