# Summary

+   1. Windows supports Help files in HTML Help.
+   2. The HTML Help Workshop is a separate application that combines topic files (HTML pages), graphics and multimedia files, contents files, and index files into a Help project. The compiled file has the extension .chm.
+   3. The HelpFile can be assigned to the VB project at design time or run time. At run time, use the ShowHelp or ShowHelpIndex method.
+   4. Adding a HelpProvider component to a form adds properties to the other controls on the form. Set the HelpKeyword, HelpNavigator, and HelpString properties to determine how Help is displayed for each control.
+   5. For context-sensitive Help, set the HelpNavigator property of a control to Topic and the HelpKeyword property to the name of an HTML file.
+   6. You can display a Help button on a message box using one of several overloaded signatures for the MessageBox.Show method.
+   7. To display the Help button on the title bar of a form, set the form's HelpButton property to true and the MaximizeBox and MinimizeBox properties to false. For each control, set the HelpString property to the text that you want to display.
+   8. ToolTips and status bars also can be considered a part of the Help supplied by an application.

# Key Terms

+   - context-sensitive Help — 503
+   - Help topic — 493
+   - Help Viewer — 492
+   - HelpKeyword property — 500
+   - HelpNamespace property — 500
+   - HelpNavigator property — 500
+   - HelpProvider component — 500
+   - HelpString property — 504
+   - HTML Help ActiveX control — 492
+   - HTML Help Image Editor — 492
+   - HTML Help Workshop — 492
+   - ShowHelp method — 501
+   - ShowHelpIndex method — 501

# Review Questions

+   1. How is each Help topic defined in HTML Help?
+   2. How is the Help file connected to a VB project for F1 Help?
+   3. How do you connect individual forms and controls to specific Help topics?
+   4. What Help files(s) must be distributed with a VB application?
+   5. How do you display Help in code from a menu item?
+   6. How can you display a Help button on a message box?
+   7. What is popup Help?