# Part II: Application Development Using C#

Testing your Windows Mobile application on real devices could not be easier. All you need is to:

+   1. Connect your device to your development machine using ActiveSync.
+   2. Select Windows Mobile 6 Standard Device (see Figure 18-20) in Visual Studio 2008.

![](bbox=[0.3, 0.3, 0.65, 0.55])

3. Press F5.

The application is now deployed onto the device.

# Deploying the Application

Once the testing and debugging process is over, you need to package the application nicely so that you have a way to get it installed on your users' devices.

The following sections show how to create a CAB (cabinet) file — a library of compressed files stored as a single file — so that you can easily distribute your application. Subsequent sections explain how to create an MSI (Microsoft Installer) file to automate the installation process.

# Creating a CAB File

An easy way to package your Windows Mobile application is to create a CAB file so that you can transfer it onto the end user's device (using emails, web browser, memory card, and so on).

The following steps show you how:

+   1. Add a new project to the current solution in Visual Studio 2008 (see Figure 18-21).