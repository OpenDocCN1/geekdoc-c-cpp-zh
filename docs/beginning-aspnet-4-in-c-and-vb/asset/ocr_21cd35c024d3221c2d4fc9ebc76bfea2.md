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

# Custom Actions Editor

The Custom Actions editor allows you to define custom steps that will take place during certain phases of the installation. Custom actions are created beforehand and consist of a DLL, EXE, script, or Installer class. The action would contain special steps to perform that can’t be defined in the standard deployment