IntelliSense is also used to view code comments, function declarations, and variable type information. In Visual Studio IDE, the IntelliSense feature is enabled, by default. However, you can disable it by selecting Tools → Options → Text Editor → All Languages → General and deselecting the Auto list members and Parameter information check boxes. You can activate the disabled IntelliSense feature from the IntelliSense menu item in the Edit menu.

NOTE

To view the IntelliSense drop-down list in the transparent mode, press the CTRL key while this drop-down list is open. Viewing the IntelliSense drop-down list in a transparent mode enables you to look at the entire code without closing the IntelliSense feature, as shown in Figure 1.64:

![](bbox=[0.095, 0.235, 0.805, 0.605])

Figure 1.64: Displaying Transparent IntelliSense

The IntelliSense feature contains the following options:

+   - List Members — Displays a list of valid member variables or functions for the selected class or structure.

+   - Quick Info — Displays the complete declaration of an identifier. IntelliSense usually runs as soon as you type the period after a class instance. However, there are occasions where you need to force IntelliSense to appear. For example, suppose you misspell a method name, then the IntelliSense will not appear because of the wrong function name. In such a case, you can make IntelliSense appear by pressing CTRL+J keys together. This allows you to select the appropriate method through IntelliSense and replace the misspelled method name with the correct one.

+   - Parameter Info — Displays the complete declaration of a function and its parameter list. IntelliSense is extremely useful when you need to look up information about a parameter for a given method of a class in a file that is currently checked into Microsoft SourceSafe. You can view parameter information by simply placing the cursor over the parameter and pressing CTRL+SHIFT+SPACEBAR keys together.

+   - Complete Word — Displays a list containing the complete variable or function names once you have entered sufficient initial characters to differentiate the term. If the series of starting letters uniquely identifies a single word in the IntelliSense list, then the complete word will be inserted automatically. For example, to make FontFamily property appear quickly on the Code Editor, type Font on the Code Editor. An IntelliSense drop-down list appears with options starting from Font, such as Font, FontChanged,