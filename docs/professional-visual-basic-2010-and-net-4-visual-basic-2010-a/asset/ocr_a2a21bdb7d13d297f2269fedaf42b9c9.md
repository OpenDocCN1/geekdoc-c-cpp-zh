# FIGURE 30-3

![](bbox=[0.145, 0.092, 0.77, 0.4])

# Uninstalling the Service

Uninstalling the service is very similar to installing it. The service must be in a stopped state before it can be uninstalled, but the uninstall operation will attempt to stop the service if it is running. The uninstall operation is done in the same command window as the install operation, and the command used is the same as the one for installation, except that the option /u is included just before the name of the service. Remember that you need to navigate to C:\Users\[ user ]\Documents\Visual Studio 2010\Projects\ FileWatcherService\ FileWatcherService\obj\Debug (or the equivalent Release directory, depending on your current configuration) to run this command:

```
InstallUtil.exe /u FileWatcherService.exe
```

You can tell that the uninstall was successful if the information displayed by the utility contains the following line:

```
Service FileWatcherService was successfully removed from the system.
```

If the uninstall is not successful, then read the rest of the information to determine why. Besides typing in the wrong pathname, another common reason for failure is trying to uninstall a service that is in a running state and could not be stopped in a timely fashion.

Once you have uninstalled FileWatcherService, it will no longer show up in the list of available services to start and stop (at least, after a refresh it won’t).

![](bbox=[0.545, 0.47, 0.933, 0.685])

# FIGURE 30-4

> A Windows Service must be uninstalled and reinstalled every time you make changes to it.