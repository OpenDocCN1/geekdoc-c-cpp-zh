# Different Editors for Deployment of the Applications

When you create an installer file for your application, you might need to specify where the files of the application should be installed on a target computer, specify what registry keys should be added, or add custom dialog boxes for installation. It is also possible that you need to customize the user interface that is shown during the installation of your application, or run the application to perform some specific actions on a target computer. You can specify and customize the settings related to the deployment of an application by using the deployment editors that are available in Visual Studio 2010. Note that these editors are available only when you add a setup and deployment project in your application. Visual Studio 2010 provides the following deployment editors:

+   - File System editor
+   - Registry editor
+   - File types editor
+   - User interface editor
+   - Custom actions editor
+   - Launch conditions editor

# File System Editor

The File System editor allows you to add the project outputs, files, assemblies, and other items to a deployment project and specify the target location where these files will be deployed. It displays a standard set of deployment folders by default. You can add your own folders and special folders with the editor. In addition, you can specify the desktop and Start menu shortcuts for the application within the File System editor. The files that are part of the deployment must be referenced from within the File System editor. To view the File System editor, click View→Editor→File System menu item. The File System editor appears, as shown in Figure 21.1:

![](bbox=[0.13, 0.465, 0.81, 0.782])

# Registry Editor

The Registry editor specifies registry keys and data values that you want to add to the registry of the target computer. When you open the Registry editor for the first time, it displays a standard set of registry keys. To view the Registry editor, click View→Editor→Registry. The Registry editor appears, as shown in Figure 21.2: