
- Environment String Value
- Binary Value
- DWORD Value

Using this menu, you can create a new registry key below the currently selected key (via Key), or you can create a value for the currently selected registry key using one of the four Value types: String, Environment String, Binary, and DWORD.

For example, suppose you need to create a registry entry that informs the application whether or not to run in Debug mode. The registry value must be applicable to a particular user, must be called Debug, and must contain the text True or False.

The first step is to select the following registry key in the left pane of the editor:

```
HKEY_CURRENT_USER\Software [Manufacturer]
```

The registry key HKEY_CURRENT_USER is used to store registry settings that apply to the currently logged-in user.

Now you want to create a value that it is applicable to only this application, not all applications created by you. You need to create a new registry key below the HKEY_CURRENT_USER ➔ Software ➔ [Manufacturer] key that is specific to this product, so select Action ➔ New ➔ Key.

When the key is created, the key name is editable, so give it a name of [ProductName] and press Enter. This creates a key that is given the name of the product contained within this Windows Installer package. The ProductName property of the setup was discussed earlier in this chapter.

Now that you have created the correct registry key, the next step is to create the actual registry value. Make sure that your new registry key is selected, choose String Value from the Action ➔ New menu, and give the new value a name of “Debug.”

Once the value has been created, you can set a default value for it in its Properties window; in this case False. When the Windows Installer package is run, the value will be created and given a name of Debug and a value of False. If a value already exists in the registry, then the Windows Installer package will overwrite the existing value with what is defined in the Registry Editor.

You can move around most keys and values in the Registry Editor by using cut and paste or simply by dragging and dropping the required item.

The alternative to creating registry entries during installation is to have your application create registry entries the first time they are needed. However, this has one significant difference from registry keys created with a Windows Installer package. The uninstall corresponding to a Windows Installer installation automatically removes any registry keys created during the install. If the registry entries are created by the application instead, then the uninstall has no way of knowing that these registry entries should be removed.

## Importing Registry Files

If you already have a registry file (a .reg file) containing the registry settings that you would like to be created, you can import the file into the Registry Editor. To import a registry file, you need to ensure that the root node (“Registry on Target Machine”) is selected in the left pane of the editor. You can then use the Import item of the Action menu to select the registry file to import.

> Registry manipulation should be used with extreme caution. Windows relies heavily on the registry, so you can cause yourself a great number of problems if you delete, overwrite, or change registry values and keys without knowing the full consequences of the action.

If you want to create the registry entries that are required to create file associations, then use the editor covered next.

## The File Types Editor

The File Types Editor can be used to create the required registry entries to establish a file association for the application being installed. A file association is simply a link between a particular file extension and a particular application. For example, the file extension .docx is normally associated with Microsoft WordPad or Microsoft Word.

When you create a file association, not only do you create a link between the file extension and the application, you also define a set of actions that can be performed from the context menu of the file with the associated extension. For example, when you right-click a document with an extension of .docx, you get a context menu that can contain any number of actions, such as Open and Print. The action in bold (Open, by default) is the default action to be called when you double-click the file, so in the example, double-clicking a Word document starts Microsoft Word and loads the selected document.

Let’s walk through the creation of a file extension for the application. Suppose that the application uses a file extension of .set and that the file is to be opened in the application when it is double-clicked. Start the File Types Editor, which contains a single pane. In a new deployment project, this pane will only contain a root node called “File Types on Target Machine.”

To add a new file type, make sure the root element is selected in the editor. You can then choose Add File Type from the Action menu, or right-click on the root node and select Add File Type. Give the new file type the name “Example File Type.”

Next, you must set the extension and application for this file type. Use the Properties window (shown in Figure 34-8). Enter .set as the value for the Extensions property.

![](img/d99870e80390742f93963da7be0b2e61_1114_0.png)

FIGURE 34-8

To associate an application with this file type, use the Command property. The ellipses button for this property presents you with a dialog from which you can select an executable file contained within any of the folders defined in the File System Editor. In this case, you’ll select Primary Output from WindowsApplication (active) from the Application Folder as the value for Command.

When this new file type was first created, a default action was added for you called &Open — select it. Now take a look at the Properties window again. Notice the Arguments property: You can use this to add command-line arguments to the application defined in the last step. In the case of the default action that has been added for you, the arguments are "%1", where the value "%1" will be replaced by the filename that invoked the action. You can add your own hard-coded arguments (such as /d). You can set an action to be the default by right-clicking it and selecting Set as Default from the pop-up menu.

## The User Interface Editor

The User Interface Editor is used to manage the interface that is shown during installation of the application. This editor enables you to define the dialogs that are displayed to the user and in what order they are shown. The User Interface Editor is shown in Figure 34-9.

![](img/d99870e80390742f93963da7be0b2e61_1115_0.png)

FIGURE 34-9

The editor uses a tree view with two root nodes: Install and Administrative Install. Below each of these nodes are three nodes that represent the stages of installation: Start, Progress, and End. Each of the three stages can contain a number of dialogs that are displayed to the user when the resulting Windows Installer package is run. A default set of dialogs is predefined when you create the deployment project. Which default dialogs are present depends on the type of deployment project: Setup Project or Web Setup Project. Figure 34-9 shows the dialogs that were added by default to a Setup Project. However, if you are creating a Web Setup Project, the Installation Folder dialog will be replaced by an Installation Address dialog.

Using Figure 34-9, the following section discusses the two modes in which the installer can be run, and explains the three stages of the installation.

### Installation Modes

The installation can run in two modes, which correspond to the two root nodes of the editor: Install and Administrative Install. These distinguish between an end user installing the application and a system administrator performing a network setup.

> To use the Administrative Install mode of the resulting Windows Installer package, you can use msiexec.exe with the /a command-line parameter: msiexec.exe /a < PACKAGE > .msi.

The Install mode is most frequently used and is what you will use in this exercise. As mentioned earlier, the installation steps are divided into three stages, represented as subnodes of the parent installation mode.
