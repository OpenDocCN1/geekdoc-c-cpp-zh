You can deploy an XBAP application using either the XCopy or the Windows Installer deployment technique. However, once the XBAP is deployed, it is not automatically updated when a new version is published. Let’s perform the following steps to deploy an XBAP application using the Windows Installer deployment technique:

+   1. Create a WPF Browser Application. In our case, we have created XBAPApplication (also available on CD).
+   2. Right-click the solution name, in Solution Explorer, and select the Add→New Project option. The Add New Project dialog box opens (Figure 21.51).
+   3. Select Other Project Types→Setup and Deployment→Visual Studio Installer in the Recent Templates category.
+   4. Select the Web Setup Project template in the middle pane and enter a project name in the Name text box. In our case, we have entered DeploymentTestXBAP, as shown in Figure 21.51:

![](bbox=[0.215, 0.25, 0.845, 0.59])

# Figure 21.51: Creating Setup Project

+   5. Click the OK button to create a Web setup project (Figure 21.51).
+   6. Right-click the DeploymentTestXBAP icon in Solution Explorer and select Add→Project Output from the context menu. The Add Project Output Group dialog box opens.
+   7. Select XBAP Application in the Project combo box and Primary output in the list box from the Add Project Output Group dialog box.
+   8. Click the OK button to add the primary output to the XBAPApplication solution.
+   9. Select Build→Rebuild DeploymentTestXBAP to generate the the XBAPApplication.exe.manifest and XBAPApplication.xbap files.
+   10. Right-click the DeploymentTestXBAP icon in Solution Explorer and select Add→File from the context menu. The Add Files dialog box opens, in which you need to select the XBAPApplication.exe.manifest and XBAPApplication.xbap files.
+   11. Click the Open button to add both the files to the setup project.
+   12. Select the Web Application Folder and set the value of the DefaultDocument property to XBAPApplication.xbap in the Properties window in the File System editor.
+   13. Select Build→Rebuild DeploymentTestXBAP to compile the Setup project.

After compiling the project, open the Debug folder of the project where you can see two files, DeploymentTestXBAP.msi and Setup.exe. Copy the DeploymentTestXBAP.msi file and paste it to