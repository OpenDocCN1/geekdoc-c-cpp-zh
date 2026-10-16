![](bbox=[0.105, 0.062, 0.894, 0.452])

# Figure 36.11

# Windows App Certification Kit

Before submitting an app package to the Windows Store, and also before sideloading it to other devices, you should run the Windows App Certification Kit. This tool is part of the Windows SDK that is installed alongside Visual Studio.

When you deploy your application to the Windows Store, it is necessary for the application to fulfill some requirements. You can check most of the requirements beforehand.

You should give the application some time when you’re running this tool. It requires several minutes to test the application and get the results. During this time you shouldn’t interact with the tool or your running application. The app is checking to make sure the package is correctly built using release and not debug code, the app does not crash or hang, only supported APIs are called, capabilities are used correctly, cancellation handlers of background tasks are implemented, and more. Just start the tool to see all the tests it runs.

Figure 36.12 shows a dialog for starting the certification kit where you can select what tests to run.