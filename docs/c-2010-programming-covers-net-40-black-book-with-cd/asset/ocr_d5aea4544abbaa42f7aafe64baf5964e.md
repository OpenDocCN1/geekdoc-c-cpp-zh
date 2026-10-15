allows the XCopy command to create the destination folder if it does not exist. Figure 21.45 shows the output of the preceding command:

![](bbox=[0.17, 0.109, 0.806, 0.322])

Now, you need to create a virtual directory on the target server and map that virtual directory with the physical directory that is created by the XCopy command on the target server.

Next, you learn how to deploy a WPF application.

# Deploying a WPF Application

To deploy a WPF application, you can use a variety of techniques, such as using XCopy deployment, Microsoft Windows Installer, and ClickOnce deployment. In our case, we have created a WPF application named LocalAnimation. The design and source code of the LocalAnimation application is available on CD.

Now, let’s perform the following steps to know how the LocalAnimation application can be deployed using the Windows Installer deployment technique:

+   1. Right-click the LocalAnimation solution name in Solution Explorer and select the **Add→New Project** option. The Add New Project dialog box opens (Figure 21.46).
+   2. Select **Other Project Types→Setup and Deployment→Visual Studio Installer category**.
+   3. Select the Setup Project template in the middle pane and enter a project name in the Name text box. In our case, we have entered `deploymentTestWPFApplication`, as shown in Figure 21.46:

![](bbox=[0.214, 0.619, 0.786, 0.907])