```
72      private javax.swing.JComboBox tasksJComboBox;
73      // End of variables declaration
74   }
```

![](bbox=[0.13, 0.16, 0.81, 0.285])

![](bbox=[0.13, 0.29, 0.87, 0.42])

![](bbox=[0.13, 0.43, 0.76, 0.61])

Fig. J.2 | Use Desktop to launch the default browser, open a file in its associated application and compose an e-mail in the default e-mail client. (Part 3 of 3.)

# J.4 Tray Icons

Tray icons generally appear in your system’s system tray, taskbar status area or notification area. They typically provide quick access to applications that are executing in the background on your system. When you position the mouse over one of these icons, a tooltip appears indicating what application the icon represents. If you click the icon, a popup menu appears with options for that application.

Classes SystemTray and TrayIcon (both from package java.awt) enable you to create and manage your own tray icons in a platform independent manner. Class SystemTray provides access to the underlying platform’s system tray—the class consists of three methods:

+   - static method getDefaultSystemTray returns the system tray
+   - method addTrayIcon adds a new TrayIcon to the system tray
+   - method removeTrayIcon removes an icon from the system tray