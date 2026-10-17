![](bbox=[0.13, 0.17, 0.72, 0.33])

FIGURE 14.23 Establishing a target dependency

Since the importer should be a part of the app, you would need to take a few extra steps for it to become part of TestApp. First, select the app’s target, select the Build Phases tab, and drag the importer target into the Target Dependencies build phase (Figure 14.23) to instruct Xcode to build it first so it’s available when building the application target. Then, add the importer target to the app target’s Copy Bundle Resources build phase. The next time you build TestApp, the importer will be built first, then copied into the app bundle’s Resources folder when TestApp itself is built.

TIP: In Xcode 4.0, you cannot drag the importer target directly into the resources for some reason. You’ll need to click the Add (+) button and choose the product from the Products folder in the sheet.

The importer would not function as it currently exists. To make it work, you would need to customize the code in the MySpotlightImporter.m source file to teach it to interpret the application’s data. You would also need to teach Spotlight, by other means, how to gather interesting information from the data model you created in Chapter 10. The importer is otherwise harmless if left in the TestApp project, so you could leave it, customize it to get it working if you’re feeling adventurous, or remove the target and its source and resources from the project to keep things tidy.

NOTE: The code and knowledge necessary to customize the importer is beyond the scope of this book. Search the documentation for the Spotlight Importer Programming Guide for more information.