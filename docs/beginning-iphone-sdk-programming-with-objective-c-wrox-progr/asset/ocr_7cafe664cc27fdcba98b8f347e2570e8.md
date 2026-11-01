+   3. The Active SDK item allows you to select whether to deploy your application to a real device or the iPhone Simulator (see Figure 2-6).

![](bbox=[0.62, 0.16, 0.9, 0.3])

# How It Works

By adding commonly used items to the Xcode toolbar area, you can improve the efficiency of your development process. In this case, you have added the Active SDK toolbar item to the toolbar area so that you can quickly switch between testing your application on the iPhone Simulator and on a real device simply by selecting the active SDK on the toolbar.

# Using Interface Builder

Until now, this project has had no UI. To prove this fact, simply press Command-R (or select Run ↻ Run), and your application is deployed to the included iPhone Simulator. Figure 2-7 shows the blank screen displayed on the iPhone Simulator. It's good to see this now, because as you go through the chapter you will see what changes occur based on your actions.

Obviously, a blank screen is not very useful. So, it's time to try adding some controls to the UI of your application. If you examine the list of files in your project, you notice two files with the .xib extension — MainWindow.xib and HelloWorldViewController.xib. Files with .xib extensions are basically XML files containing the UI definitions of an application. You can edit .xib files by either modifying their XML content, or more easily (and more sanely), edit them using Interface Builder.

Interface Builder comes as part of the iPhone SDK and allows you to build the UI of an iPhone (and Mac) applications by using drag-and-drop.

Double-click the HelloWorldViewController.xib file to launch Interface Builder. Figure 2-8 shows Interface Builder displaying the content of HelloWorldViewController.xib (which is really empty at this moment). As you can see, the Library window shows all the various controls that you can add to the UI of your iPhone application. The View window shows the graphical layout of your UI. You will see the use of the other windows shortly.

![](bbox=[0.68, 0.52, 0.9, 0.86])