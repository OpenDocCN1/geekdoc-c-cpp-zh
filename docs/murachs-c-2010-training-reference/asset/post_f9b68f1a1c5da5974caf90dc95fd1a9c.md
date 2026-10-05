
The options in the Publish Version let you specify the version of the application that's built. Initially, the version is set as shown in figure 25-3. Then, each time the application is published again, the version number is incremented by one. However, you can also change the version number manually, and you can remove the check mark from the Automatically Increment Version option so that the version isn't incremented automatically. Note that when an application is published with a new version number, it's treated as an update.
You'll learn more about updating an application using ClickOnce later in this chapter.

Once you have all the sets you want, you can simply click the Publish Now button to publish the application. As part of the publishing process, a web page is created that provides for installing the application. This page is then displayed so you can install and test the application on your own computer.

## How to select the files that are published

If you click the Application Files button on the Publish page of the Project Designer, the Application Files dialog box shown in figure 25-4 is displayed. This dialog box lists the output files for the project and indicates which ones will be published. By default, only the exe and .manifest files will be published. If you want to publish the pdb file as well, you can select the Include option from the Publish Status drop-down list.

## How to select the prerequisites

If you click the Prerequisites button on the Publish page, the Prerequisites dialog box shown in figure 25-4 is displayed. This dialog box lets you select the components that must be installed for the application to work correctly. Windows Installer 3.1 and the target framework (usually .NET Framework 4 Client Profile) are selected by default, which is usually what you want.

In some cases, additional components will be required. If an application uses a SQL Server 2008 database that's installed on the user's computer, for example, the user must have SQL Server 2008 Express installed. You'll learn more about that in this chapter.

By default, the components you select are downloaded from the vendor's web site and then installed by ClickOnce. For example, if the .NET Framework or SQL Server Express are needed, they're downloaded from Microsoft's web site. If the components are available from the computer where you are developing the application, you can publish them to the same location as the application. Then, if you select the second option in the Prerequisites dialog box, the components will be downloaded from the same location as the application. If you make the components available from another location, you can also use the third option to specify that location.

## Chapter 25 How to deploy an application

## Application Files and Prerequisites dialog boxes

![](img/3148667e42d4db35b3d08576aaa1fa01_782_0.png)

## Description

- Only the exe and exe.manifest files for an application are installed by default. If you want to include the pdb file, you can display the Application Files dialog box, check the Show All Files, and then change the publish status of this file.
- The target framework for the application is included as a prerequisite by default, which is usually what you want. Then, the installation program will download and install the Framework from Microsoft's web site.
- Windows Installer 3.1 is also included as a prerequisite by default. Windows Installer is a service that's used to install and configure applications.
- If additional components, such as SQL Server 2008 Express, are required by an application, you can include them by selecting the appropriate options from the Prerequisites dialog box.

## Note

- The exe.manifest file contains the application manifest, which contains information about the application that's being deployed.

Figure 25-4 How to select the files that are published and the prerequisites

Section 5 Other skills for C# developers

## How to set the update options

By default, an application doesn't check for updates, which isn't usually what you want. To change how this works, you use the Application Updates dialog box shown in figure 25-5. To display this dialog box, you click the Updates button on the Publish page of the Project Properties window.

To start, you select the check box at the top of the dialog box that indicates that the application should check for updates each time the user runs it. When you do, the two options that follow become available, and the second option will be selected by default. This option causes the application to check for updates each time the user runs it. Then, if an update is available, a dialog box is displayed that lets the user install the update. You'll see that dialog box in a minute.

You can also specify that an application not install updates until the next time it runs by selecting the After the Application Starts option. If you select this option, you can also specify how frequently the application checks for updates. By default, it checks for updates every time it's run, but you can also have it check at the interval of days you specify.

You can also use the Application Updates dialog box to specify the lowest version number of the application that must be installed. Then, when the user runs the application, if that version or a higher version hasn't been installed, it's installed automatically.

Finally, the Application Updates dialog box lets you specify where application updates are located. In most cases, you'll publish the updates to the same location as the original application, so you can leave this option blank.

## The Application Updates dialog box

![](img/3148667e42d4db35b3d08576aaa1fa01_784_0.png)

## Description

- By default, an application doesn't check for updates. If you want to include the pdb file, you can display the Application Files dialog box, check the Show All Files, and then change the publish status of this file.
- The target framework for the application is included as a prerequisite by default, which is usually what you want. Then, the installation program will download and install the Framework from Microsoft's web site.
- Windows Installer 3.1 is also included as a prerequisite by default. Windows Installer is a service that's used to install and configure applications.
- If additional components, such as SQL Server 2008 Express, are required by an application, you can include them by selecting the appropriate options from the Prerequisites dialog box.

## Note

- The exe.manifest file contains the application manifest, which contains information about the application that's being deployed.

Figure 25-4 How to select the files that are published and the prerequisites

Figure 25-5 How to set the update options

## How to set the options

The Publish Options dialog box, which is displayed when you click the button on the Publish page of the Project Properties window, lets you set a variety of options. These options are divided into four tabs, as you can see in figure 25-6. In most cases, you'll leave the remaining options in the Publish Options dialog box at their default settings. If you publish your application to a CD, however, you may want to select the second last option on the Deployment tab. Then, the installation will start automatically when the CD is inserted. And if you want to create a shortcut on the user's desktop when the application is installed, you can select the last option on the Manifests tab.
