Under Type, select SYSTEM COMMAND and enter “/H” in the Command field. For Location, select DESKTOP and then click FINISH. This will create a shortcut on your desktop. You can drag and drop this shortcut onto any modal dialog box to turn on debugging for the window.

# 17.2 New Debugger

The Classic Debugger loads in the same session as the program. This poses certain technical challenges for debugging ABAP programs. This also restricts developing a new UI design for the debugger. To overcome such challenges, SAP introduced the New Debugger.

In the following sections, we’ll look at the UI and tools offered with the New Debugger that differ from the Classic Debugger. We’ll also look at the overall layout and the use of sessions.

# 17.2.1 UI and Tools

The New Debugger provides a feature-rich UI that can be customized to display up to four tools in a desktop. Figure 17.19 shows the New Debugger with the UI customized to display different tools. One tool shows the source code, another tool shows an internal table, the third tool shows an object, and the fourth tool shows variables.

Each tab is called a desktop in the New Debugger, and there are twelve total desktops, with each desktop capable of displaying four tools. Each tool has its own options, as shown in Figure 17.20. Using the available options for the tool, you can load new tools in the desktop, replace the tool, swap the tool, maximize the tool, and so on. There are also specific services for the tool that can be accessed using the SERVICES OF THE TOOL icon.