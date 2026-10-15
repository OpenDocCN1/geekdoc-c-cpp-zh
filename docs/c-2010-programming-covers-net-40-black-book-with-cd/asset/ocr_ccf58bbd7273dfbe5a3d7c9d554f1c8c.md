# Chapter 21: Deploying Windows and Web Applications

When the installation is completed, the Installation Complete page appears, as shown in Figure 21.43:

![](bbox=[0.293, 0.087, 0.708, 0.336])

Figure 21.43: Displaying the Installation Complete Page

5. Click Close to successfully close the DeploymentTestWebSetup wizard (Figure 21.43).

Now, you can run the DeploymentTestWebApplication application from the location where you have deployed it. To do so, open the browser and type the address of the virtual directory where the Web application is deployed, as shown in Figure 21.44:

![](bbox=[0.103, 0.428, 0.884, 0.738])

Figure 21.44: Running the Installed Application

Let’s now learn how to deploy a Web application using the XCopy command.

# XCopy Deployment

To deploy a Web application by using the XCopy deployment technique, open the Run dialog box from the Start menu of Windows. Type cmd in the Open text box of the Run dialog box and then click the OK button. This step opens the command prompt, where you need to type the following command:

```
xcopy /I /S c:\inetpub\wwwroot\DeploymentTestWebSetup d:\MyWebApp
```

In the preceding command, the source folder named DeploymentTestWebSetup exists in the c drive and the destination folder named MyWebApp exists in the d drive. When you execute this command, all the files and folders within the DeploymentTestWebSetup folder are deployed to the targeted folder. The /I parameter