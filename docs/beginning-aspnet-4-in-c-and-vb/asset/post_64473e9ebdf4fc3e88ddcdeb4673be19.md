
## File Types Editor

The File Types editor is used to establish associations between files and applications. For example, when you double-click a file with the .doc extension, the file is opened in Word. You can create these same associations for your application.

To add an association, execute the following steps:

- 1. Select File Types on Target Machine from the Action menu.
- 2. Then select Add File Type. In the properties window, you can now set the name of the association.
- 3. In the Extension property, add the file extension that should be associated with the application. Do not enter the periods; you can separate multiple extensions with a semicolon, like this: ex1;ex2.
- 4. In the Command property, select the Ellipsis button.
- 5. Now, select the file (typically an executable) that you want to associate with the specified file types. Keep in mind that any one extension should be associated with only one application.

By default, the editor shows &Open as the Document Action. You can add others. The order in which the actions appear in the editor is the order in which they will appear in the context menu when the user right-clicks the file type. Keep in mind that the first item is always the default action. You can set the Arguments property for the actions. This is the command-line argument used to start the application.

## User Interface Editor

Sometimes you might want to ask the user for more information during the installation process. The User Interface editor is used to specify properties for a set of predefined dialog boxes. The editor is separated into two sections, Install and Admin. One is for the standard installation and the other is used for an administrator's installation. Each section is broken up into three subsections: Start, Progress, and End. These subsections represent the three basic stages of the installation process (see Figure 17-3).

![](img/d7d2ffa0a76feaab821930e95daace93_484_0.png)

The following table lists the types of dialog boxes that you can add to the project.

| DIALOG BOX | DESCRIPTION |
|---|---|
| Check Boxes | Contains up to four check boxes. Each check box has a Label, Value, and Visible property. |
| Confirm Installation | Gives the user the ability to confirm the various settings before installation takes place. |
| Customer Information | Has edit fields for the collection name, organization name, and serial number. Organization name and serial number are optional. |
| Finished | Displayed at the end of the setup process. |
| Installation Address | For web applications, displays a dialog box so that users can choose an alternative installation URL. |
| Installation Folder | For client applications, displays a dialog box so that users can select an alternative installation folder. |
| License Agreement | Displays the license agreement that is located in a file specified by the LicenseFile property. |
| Progress | Displays a progress indicator during the installation process that shows the current installation status. |
| Radio Buttons | Contains up to four radio buttons. Each radio button has a Label and Value property. |
| Read Me | Shows the readme information contained in the file specified by the ReadMe property. |
| Register User | Executes an application that will guide the user through the registration process. This application must be supplied in the setup project. |
| Splash | Displays a bitmap image. |
| Text Boxes | Contains up to four text box fields. Each text box has a Label, Value, and Visible property. |
| Welcome | Contains two properties: the WelcomeText property and the CopyrightWarning. Both are string properties. |

Each of these dialog boxes also contains a property for setting the banner bitmap, and most have a property for banner text. You can also change the order in which the dialog boxes appear by dragging them up or down in the editor window.

Now that you can capture some of this information, the question is, how do you make use of it? This is where the Condition property that appears on most of the objects in the project comes in. The Condition property must evaluate to true for the installation step to proceed. For example, say the installation comes with three optional installation components. In this case, you would add a dialog box with three check boxes. The dialog should be somewhere after the Welcome and before the Confirm Installation dialog box. Change the Label property of each check box to describe the action. The first action could be “Install Component A,” the second could be “Install Component B,” and so on. In the File System editor, select the file that represents Component A. Assuming that the name of the check box on the dialog box is CHECKBOXA1, the Condition property of the file would be CHECKBOXA1=Checked — that is, if CHECKBOXA1 is checked, install the file; otherwise, don’t install it.

## Custom Actions Editor

The Custom Actions editor allows you to define custom steps that will take place during certain phases of the installation. Custom actions are created beforehand and consist of a DLL, EXE, script, or Installer class. The action would contain special steps to perform that can’t be defined in the standard deployment.

Because the action is code that you develop outside the deployment project, you have the freedom to add just about anything that adds a professional touch to your application. The thing to remember is that such an action happens after the phase it is associated with is complete. If you select the Install phase, the action will not execute until after the install phase has completed. If you want to make determinations before the process, you will want to create a launch condition.

## Launch Conditions Editor

The Launch Conditions editor allows you to specify that certain conditions must be met before installation can continue. Launch conditions are organized into types of conditions. The basic launch conditions are File Search, Registry Search, and Windows Installer Search. When the editor is first started you see two groups (see Figure 17-5): Search Target Machine and Launch Conditions. Typically, a search is conducted, and, based on the success or failure of that search, a condition is executed. This happens by setting the Property property of the search. The Property property can be accessed by the installation process. It can be checked in the Condition property of other actions, for example. You can also add a launch condition in the editor. In this condition, you set the Condition property to the value of the Property property in the search. In the condition, you can specify a URL that will download the file, registry key, or installer component that was being searched for. Notice in Figure 17-5 that a .NET Framework condition is added by default.

![](img/d7d2ffa0a76feaab821930e95daace93_487_0.png)

FIGURE 17-5

File Search will search for a file or type of file. You can set many different file-related properties that determine how files are searched, including filename, folder location, various date values, version information, and size. You can also set the number of subfolders that are searched.

Registry Search allows you to search for keys and values. It also allows you to set the root key for searching.

Windows Installer Search looks for the specified Installer component. The search is conducted by GUID.

The Launch Conditions editor provides two prepackaged launch conditions: the .NET Framework Launch Condition, which allows you to search for a specific version of the runtime, and a search for a specific version of MDAC, which uses the registry search to find the relevant MDAC registry entries.

## SUMMARY

Deploying software has become difficult for developers of desktop software. As web sites have grown more complex, the deployment of server-based software has become more difficult. This chapter looked at the options and capabilities that Visual Studio 2010 and version 3.5 of the .NET Framework provide to help make deployment easier and less error-prone.

After reading this chapter, you should be able to create a deployment package that resolves almost any deployment issue that you might have. Client applications can be deployed locally or via the Internet or an intranet. The extensive features of deployment projects and the ways that deployment projects can be configured were covered. You can also use no-touch deployment and ClickOnce to deploy applications. The security features of ClickOnce will make this a secure and efficient way of deploying client applications. Using deployment projects to install web applications can make the process of configuring IIS much easier as well. Publishing a web site provides the added benefit of precompiling the application.
