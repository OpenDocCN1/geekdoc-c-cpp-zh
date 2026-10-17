FIGURE 16.6 Linking the TestApp product against the shared framework

![](bbox=[0.28, 0.16, 0.68, 0.23])

FIGURE 16.7 Adding the shared framework to the Copy Frameworks build phase

![](bbox=[0.28, 0.255, 0.712, 0.38])

Note the new “Workspace” group at the top of the list. Xcode knows that a framework target exists within one of the projects within the TestApp Suite workspace. Select TestAppSharedFramework.framework and click Add. The framework is now part of TestApp (Figure 16.6).

To test it, clean the workspace by selecting Product > Clean from the main menu. Then make sure the TestApp scheme is selected in the Scheme pop-up and build the application.

Of course, as you learned in Chapter 15, TestAppSharedFramework isn’t a system-provided framework, so you’ll need to distribute it within TestApp. Although TestApp would run in the development environment, it would crash due to a missing library were you to distribute it in its current state (recall this from Chapter 15 when you added a Copy Frameworks build phase for the foreign Foo.framework). You can simply drag TestAppSharedFramework.framework from the TestApp project into the TestApp target’s Copy Frameworks phase (Figure 16.7).