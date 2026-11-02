# How It Works

You may recall that the original project files created by the Tab Bar Application template contain only one view controller — `FirstViewController` — which corresponds to the first view in the Tab Bar View Controller. The second view is represented by the `SecondView.xib`, but it does not have a corresponding View Controller class. To ensure that this view supports all orientations, you need to add a new View Controller class to the project so that it can override the implementation provided by the base `UIViewController` class. You then override the `shouldAutorotateToInterfaceOrientation:` method so that each View Controller returns `YES` to support all orientations.

# MAXIMUM NUMBER OF TAB BAR ITEMS

The Tab Bar supports at most five Tab Bar Items. After you have more than five items, you will see a More item, and touching the More item displays the rest of the items in a Table View (see Figure 8-17).

![](bbox=[0.6, 0.42, 0.85, 0.76])

# NAVIGATION-BASED APPLICATIONS

Tab Bar applications are suitable for situations in which you have several views, each view displaying different information so the user can quickly switch among them. However, sometimes you have hierarchical data that requires users to move from one screen to another based on what they have selected. In this situation, it is better to use a Navigation-based application.