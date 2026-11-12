![](bbox=[0.038, 0.158, 0.898, 0.516])

**FIGURE 1.5** Building for the iPhone simulator

**FIGURE 1.6** The main view

**FIGURE 1.7** The flipside view

Utility applications should provide easy access to a single screen of information, with a backside view for modifying the preferences. The iPhone’s Weather app is a representative example. The main screen shows simple weather forecasts for the next week (though you can page through multiple cities). The flipside view allows you to edit the list of cities, as well as change between Fahrenheit and Celsius.

The Utility Application template creates the basic skeleton for this type of application. The template is, by itself, a fully functional app—it will build and run. Of course, it won’t do anything interesting, but we will fix that in a bit. For now, let’s look at what we get for free.

# RUNNING THE APPLICATION

First, we need to tell Xcode to use the simulator. Click the Scheme button in the Xcode toolbar and select iPhone 5.0 Simulator (Figure 1.5). Then click the Run button. Xcode will build the application and launch it in the simulator.

As you can see, the application has a gray main view with an info button in the lower-right corner (Figure 1.6). If you touch the info button, the screen flips over to show the flipside view with a title bar and a blue Done button (Figure 1.7). Touch the Done button and you flip back to the main view.