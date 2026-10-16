![](bbox=[0.105, 0.062, 0.895, 0.298])

# Figure 36.13

To install a Windows app with sideloading, you can use WinAppDeployCmd.exe. This tool is part of the Windows 10 SDK.

This tool allows you to scan all devices on the network available for installation using

```
WinAppDeployCmd.exe devices
```

To install an app on a device, use the following install option:

```
WinAppDeployCmd.exe install -file SampleApp.appx -ip 10.10.0.199 -pin ABC3D5
```

To update an app, you can use the update option:

```
WinAppDeployCmd.exe update -file SampleApp.appx -ip 10.10.0.199
```

And to uninstall an app, you use the option uninstall:

```
WinAppDeployCmd.exe uninstall -package packagename
```

# Summary

Deployment is an important part of the application life cycle that you need to consider from the beginning of the project because the deployment method influences the technology you use. Deploying different application types has been shown in this chapter.

You’ve seen the deployment of Windows applications using ClickOnce. ClickOnce offers an easy automatic update capability that can also be triggered directly from within the application, as you’ve seen with the System.Deployment API.

You also learned how to deploy UWP apps, which you can publish in the Windows Store, but you can also deploy using command-line tools without using the store.

The next chapter is the first of a group covering services and web applications, starting with ADO.NET to access the database.