When created, the deployment project does not contain any files. It has a folder called Detected Dependencies, which is discussed later. You will need to add the executable file from your Windows application SampleForDeployment to the deployment project.

You add files to a setup deployment project using the Add function, which is available in two places: You can select the deployment project in the Solution Explorer and use the Add option from the Project menu, or you can right-click the setup project file in the Solution Explorer and choose Add from the pop-up menu. Both methods enable you to choose from one of four options:

+   - If you select File from the submenu, you are presented with a dialog that enables you to browse for and select a particular file to add to the setup project. This method is suitable if a file needed by the application is not the output from another project within the solution.
+   - The Merge Module option enables you to include a merge module in the deployment project. Third-party vendors can supply merge modules or you can create your own with Visual Studio.
+   - The Assembly option can be used to select a .NET component (assembly) to be included in the deployment project.
+   - If the deployment project is part of a solution (as in this walk-through), you can use the Project ➔ Add ➔ Project Output submenu item. This enables you to add the output from any of the projects in the solution to the setup project.

![](bbox=[0.6, 0.23, 0.85, 0.48])

Add the output of the Windows Forms Application project to the setup project. Select the Project Output menu item to bring up the dialog shown in Figure 34-3.

The Add Project Output Group dialog is divided into several parts:

+   - The combo box at the top contains a list of names of all the nondeployment projects in the current solution. In your case, there is only one project: SampleForDeployment.
+   - Below the combo box is a list box containing all the possible outputs from the selected project. You are interested in the Primary output, so make sure that this is selected. (Other options for output are described in the MSDN for Visual Studio help files.)
+   - Below the list of possible outputs is a combo box from which you can select the configuration to use for the selected project. You will use the (Active) option here, because this uses whatever configuration is in effect when the project is built.

Click OK to return to the solution.

At this point, not only has the output from the Windows application been added to the Setup project, but the Detected Dependencies folder also contains an entry.

Whenever you add a .NET component to this deployment project, its dependencies are added to this folder. Any dependencies of the dependencies are also added, and so on until all the required files have been added. The files listed in the Detected Dependencies folder are included in the resulting setup and, by default, are installed into the application's directory as application-private assemblies. This default behavior helps reduce the possible effects of DLL hell by making the application use its own copies of dependent files.

If you don’t want a particular dependency file to be included in the resulting setup, you can exclude it by right-clicking the file entry under Detected Dependencies and selecting Exclude from the pop-up menu. For example, you may decide that you want to exclude a detected dependency from the setup of an application because you know that the dependency is already installed on the target computer. The dependency will then have a small “circle and slash” icon before its name to indicate that it has been excluded.