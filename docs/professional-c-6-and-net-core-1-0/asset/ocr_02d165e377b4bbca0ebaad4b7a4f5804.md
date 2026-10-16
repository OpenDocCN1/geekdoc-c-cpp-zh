![](bbox=[0.1, 0.06, 0.9, 0.37])

# Figure 36.7

You can set up the application so that it runs in either online or offline mode. In offline mode the application can be run from the Start menu and acts as if it were installed using the Windows Installer. Online mode means that the application runs only if the installation folder is available.

# Application Cache for ClickOnce Files

Applications distributed with ClickOnce are not installed in the Program Files folder. Instead, they are placed in an application catch that resides in the %LocalAppData%\Apps\2.0 folder. Controlling this aspect of the deployment means that multiple versions of an application can reside on the client PC at the same time. If the application is set to run online, every version that the user has accessed is retained. For applications that are set to run locally, the current and previous versions are retained.

This makes it a very simple process to roll back a ClickOnce application to its previous version. If the user selects the Install/Uninstall Programs control panel applet, the dialog presented contains the options to remove the ClickOnce application or roll back to the previous version. An administrator can change the manifest file to point to the previous version. If the administrator does this, the next time the user runs that application, a check is made for an update. Instead of finding new assemblies to deploy, the application restores the previous version without any interaction from the user.

# Application Installation

Now let’s start the application installation. Copy the files from the publish folder to the network share that was specified when you