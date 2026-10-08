# Part I: Developer Tools

10. Bring Xcode to the foreground and press Command+R to run your application.

Something isn't quite right, as shown in Figure 4-14. The Application menu is still stuck with MyProject.

What's going on here? Your application supplies the text for your Application menu by using a string in its Info.plist file, not from the text you entered in Interface Builder. Go figure!

The Info.plist is a file that contains information about your application. You can find the version number for your application, assign an icon to the application, and set the default language for the application, among other tasks.

![](bbox=[0.115, 0.245, 0.215, 0.335])

Figure 4-14: Despite changes to the menu in Interface Builder, the project is still displaying the wrong name in the Application menu.

![](bbox=[0.245, 0.375, 0.725, 0.545])

11. Change the Info.plist file as follows:

+   a. In Xcode, expand the Resources group.

+   b. Select the InfoPlist.strings.

The Code editor displays the contents of this file, which you can edit.

+   c. Change the first line of code to read

```
CFBundleName = "SimpleCalculator";
```

12. In Xcode, press Command+R.

The Application menu appears with the corrected name. Figure 4-15 shows the results of the InfoPlist change.

13. Click the Interface Builder icon on the Dock to return to it.