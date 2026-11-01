> **NOTE** The Badge property is a nifty way for you to set some numbers or other text on the Tab Bar Item so that it can serve as a quick visual cue to users to remind them of something.

4. In Xcode, right-click the Classes folder in Xcode and choose Add ⌥ New File. Click the Cocoa Touch Classes category and select the `UIViewController` subclass. Name the file `SearchViewController.m` (check the “With XIB for user interface” option).

5. Double-click the newly created `SearchView.xib` file to open it in Interface Builder. Add a Label view to it (see Figure 4-50).

> **NOTE** You won’t be doing much in this SearchView.xib file. You’re just adding a Label view so that you will see that this view loads successfully when the user taps on the Tab Bar Item.

![](bbox=[0.1, 0.62, 0.8, 0.82])

FIGURE 4-50

6. Back in `MainWindow.xib`, select the Tab Bar Item and view its Attributes Inspector window (see Figure 4-51). Set its NIB name to `SearchViewController`.

7. In the Identity Inspector window for the Search Tab Bar Item, set the Class name to `SearchViewController` (see Figure 4-52). This step is important; without it, you will get a runtime error later on when you create outlets and actions on the View Controller class.

8. Save the project in Interface Builder.

9. That’s it! Press Command-R to test the application on the iPhone Simulator. You can now touch the third Tab Bar Item (Search) to view the label (see Figure 4-53).