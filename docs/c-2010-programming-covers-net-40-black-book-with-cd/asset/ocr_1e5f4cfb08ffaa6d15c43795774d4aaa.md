# Deploying a Web Service

After creating a Web service, the next step is to make the Web service available to other Web applications over the Internet. You need to transfer the Web service from the development environment to the production environment to make a Web service available to other applications.

You can do this by deploying the Web service over the Web server on which you want to run the Web service. You can deploy this Web service by using the Web Setup Project template of Visual Studio 2010. Now, let’s learn how to deploy a Web service, say, CalculateSimpleInterest, created earlier. To do this, open the CalculateSimpleInterest Web service in Visual Studio 2010 and follow these steps:

+   1. Click the File→Add→New Project option in Visual Studio 2010 to display the New Project dialog box.
+   2. Expand the Other Project Types node in the Installed Templates of the New Project dialog box (Figure 18.8).
+   3. Select the Setup and Deployment option → Visual Studio Installer from the Other Project Types node (Figure 18.8).
+   4. Select the Setup Project template from the middle pane (Figure 18.8).
+   5. Change the name Setup Project with SimpleInterestSetup in the Name text box and Select the Add to solution from the Solution drop-down list (Figure 18.8).
+   6. Click the OK button to add the SimpleInterestSetup project in the Solution Explorer, as shown in Figure 18.8:

![](bbox=[0.06, 0.387, 0.92, 0.792])

The File System editor appears (Figure 18.9).

+   7. Select Application Folder displayed in the File System editor and right-click the SimpleInterestSetup project in Solution Explorer. A context menu appears (Figure 18.9).
+   8. Select Add→Project Output from the context menu, as shown in Figure 18.9: