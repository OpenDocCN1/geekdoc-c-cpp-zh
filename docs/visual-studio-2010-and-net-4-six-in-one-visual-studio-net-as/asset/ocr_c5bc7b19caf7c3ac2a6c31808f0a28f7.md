The information you provide here will be used in the source code generated for the package, and will be displayed in the About dialog. The "Company name" will be used in the namespace of generated types, as well as the "VSPack name," which also names the class representing the package in code. The "VSPack version" is additional information to provide a way for distinguishing separate package releases. Text typed in the "Detailed information" will be displayed in the About dialog, and can supply the user with more information than the name about what the package does.

When you click the Next button, the wizard moves you to the VSPack Options page (Figure 6-28) to set a few more code-generation options.

![](bbox=[0.147, 0.296, 0.663, 0.589])

**FIGURE 6-28: You can select a few code generation options**

In this sample, you will create only a menu command that pops up a message on the screen, so when you click the Menu Command option. If you selected the Tool Window option, the VSPackage wizard would create some code for a simple tool window, and code to display it on the screen. For this exercise, leave that option and the Custom Editor option unchecked.

Click the Next button and the wizard moves you to the page where you specify a few details about the menu command to create, as shown in Figure 6-29.

The command will be added to the Tools menu of Visual Studio, and in "Command name" field, you specify the text for the menu item. According to the internal command-handling architecture, each command has an identifier. The Command ID field supplies a name for this identifier, and the VSPackage wizard will generate an ID value behind this name.

When you click Next, the wizard moves to the Select Test Project Options page, as shown in Figure 6-30.