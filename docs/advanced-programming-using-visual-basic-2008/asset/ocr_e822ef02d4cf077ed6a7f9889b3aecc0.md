# Continuing the Step-by-Step Exercise

It's time to add the compiled Help file to a VB project.

# Open the Project

+   STEP 1: Open the solution file in the Ch12BSHelp folder.
+   STEP 2: Display the form in the designer.

# Connect the Help File for F1 Help

+   STEP 1: Add a HelpProvider component from the Components section of the toolbox to the form.
+   STEP 2: Set the HelpNamespace property of HelpProvider to your Help file (RnAHelp.chm). You can browse to select the file, which should be in the HTML folder.
+   STEP 3: Set the form's ShowHelp on HelpProvider property to true.
+   STEP 4: Set the form's HelpNavigator on HelpProvider 1 property to TableOf-Contents.
+   STEP 5: Run the program and press F1. Your Help screen should pop up with the Table of Contents displayed.
+   STEP 6: Close the form.

# Adding Help to a Menu

You can use two methods of the Help object to display Help in code: the ShowHelp method and the ShowHelpIndex method.

# ShowHelp Method—General Forms

```
Help.ShowHelp(control, helpfile)
Help.ShowHelp(control, helpfile, HelpNavigatorSetting)
Help.ShowHelp(control, helpfile, string for keyword to display)
Help.ShowHelp(control, helpfile, HelpNavigatorSetting, TopicID)
```

The various options allow you to specify whether the Index, Table of Contents, or a specific topic should display.

# ShowHelp Method—Examples

```
Help.ShowHelp(Me, "RnAHelp.chm")
Help.ShowHelp(Me, "C:\My Documents\RnAHelp.chm")
```

Notice that you can use the full path for the Help file, but for development, it works best to place a copy of the .chm file in the bin\Debug folder for the project and specify the filename as a string without the path.

The ShowHelpIndex method is similar to the ShowHelp, but it always displays the Index tab of the Help file.