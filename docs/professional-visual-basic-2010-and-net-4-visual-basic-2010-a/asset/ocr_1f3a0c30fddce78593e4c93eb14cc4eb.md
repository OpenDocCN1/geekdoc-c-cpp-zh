Make sure that the Launch Conditions node is selected in the editor, and add a new launch condition to the project by selecting Add Launch Condition from the Action menu. You need to give this new item a meaningful name; in this case, give it a name of Word2007Exists (see Figure 34-14).

This new item has a number of properties that you need to modify. The first property to change is called Message, and it is used to set the text of the message box that appears if this condition is not met. Enter any meaningful description that explains why the installation cannot continue.

The next property that you need to change is called Condition. It is used to define a valid deployment condition that is evaluated when the installation runs. The deployment condition entered must evaluate to True or False. When the installer is run, the condition is evaluated; if the result of the condition is False, then the message defined is displayed to the user and the installation stops.

For this example, you need to enter a condition that takes into account whether the winword.exe file was found. You can use the Windows Installer property defined earlier (WORDEXISTS) as part of the condition. Because the property is empty if the file was not found, and non-empty if the file was found, you can perform a simple test to determine whether the property is empty to create the condition. Enter WORDEXISTS <> "" as the value for the Condition property. At this point, the editor will look like Figure 34-14.

It is hoped that based on the preceding discussion of this search, you will be able to use the other searches and create your own launch conditions. That completes our brief tour of the editors that you can use to modify the resulting Windows Installer package to suit your needs. Although you have looked only briefly at the functionality of the editors, it should be clear that they are extremely powerful, and worth investment of your time for further investigation.

![](bbox=[0.47, 0.08, 0.88, 0.32])

FIGURE 34-14

# Building

The final step is to build the deployment or setup project you have created. There is no difference between how you build a Visual Basic .NET application and a deployment/setup project. If the project is the only project contained within the solution, then you can just use the Build item from the Build menu, which will cause the project to be built. As with the other projects, you are informed of what is happening during the build through the Output window.

The deployment/setup project can also be built as part of a multiproject solution. If the Build Solution item is chosen from the Build menu, then all the projects in the solution will be built. Any deployment or setup projects are built last. This ensures that if they contain the output from another project in the solution, they pick up the latest build of that project.

# INTERNET DEPLOYMENT OF WINDOWS APPLICATIONS

The earlier discussions of creating an installation package for your application assumed that you were able to transfer the MSI file to each machine that needed installation, either electronically or via some storage medium such as a CD-ROM. This works well for installations within an organization and can work acceptably for initial installation from CD-ROMs on distributed systems.