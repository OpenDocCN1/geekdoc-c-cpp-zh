+   - Install — Executes actions at the end of the installation phase
+   - Commit — Executes actions when the installation completes successfully
+   - Rollback — Executes actions when the rollback phase has completed
+   - Uninstall — Executes actions when uninstall has completed

Custom actions are run in the same order as they appear in the Custom Actions editor. However, you can also reorder them by dragging or using the Cut/Paste command.

# Launch Conditions Editor

The Launch Conditions editor allows you to specify certain conditions that must be met to continue the installation. For example, if you want to install an application on a specific version of the Windows operating system, the installation first checks the presence of specific conditions and runs the process only when the conditions are met. Otherwise, the installation is terminated at that point. You can view the Launch Conditions editor by selecting View→Editor→Launch Conditions in the Visual Studio 2010 IDE, as shown in Figure 21.6:

![](bbox=[0.22, 0.3, 0.835, 0.61])

Figure 21.6: Displaying the Launch Conditions Editor

The Launch Conditions editor (Figure 21.6) displays the following requirements on a target computer:

+   - Search Target Machine — Specifies search conditions to determine if a particular file, registry key, or Microsoft Windows Installer component exists on the target computer. Some examples of search conditions are: File Search, Registry Search, and Windows Installer Search.
+   - Launch Conditions — Specifies predefined launch conditions for an application

Next, you learn how to add the prerequisites for deploying an application.

# Including Prerequisites for an Application Deployment

To install and run an application on a target computer, you should ensure that the target computer has the prerequisites of running the application. A prerequisite is a component that must be installed on a target computer, as it is required to run your application. For instance, the target computer must be having a particular version of Common Language Runtime (CLR) on the computer. The prerequisites of your applications are selected in the Prerequisites dialog box. These prerequisites install the .NET Framework and other dependencies for your applications on the target computer, as a part of your installer application. You can access the Prerequisites dialog box by first right-clicking a project node in Solution Explorer and selecting the Properties option from the context menu. As a result of this, project properties dialog box appears. Now, select the Publish tab in project properties dialog box, as shown in Figure 21.7: