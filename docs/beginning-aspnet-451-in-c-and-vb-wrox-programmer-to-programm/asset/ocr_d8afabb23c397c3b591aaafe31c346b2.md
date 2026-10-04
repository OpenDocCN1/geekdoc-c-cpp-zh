# Preparing for Deployment | 729

![](bbox=[0.17, 0.098, 0.729, 0.456])

FIGURE 19-33

+   3. Open the drop-down at the top of the screen and create New Profile. Enter a name such as To local disk and click OK.

+   4. On the Connection tab choose File System. In the text box for Target Location, enter C:\BegASPN\Release. This folder does not have exist yet; Visual Studio will create it for you when publishing the site. Click Next

Note: If your host supports Web Deploy, you can choose that instead and enter the details, as the server name and your user credentials. The remaining steps in this exercise you selected File System.

+   5. In the Settings tab, Debug should be selected, which is what you need for this exercise. Click Next again.

+   6. On the Preview tab, click Publish to start the publishing process. After a short delay you should see a message in the Output window that the publishing process has completed successfully. If you had selected Web Deploy as the publish option, this dialog would have enabled you to review a preview of the changes by checking the files on the server or with local files.

+   7. On the Solution Explorer, click the Refresh icon and then expand the App_Data folder. You should see a file called To local disk.pubxml under the PublishProfiles subfolder.

+   8. Open the folder C:\BegASPN\Release in File Explorer. Now how all files have been copied to the output folder. If you look at the Web.config file in the Release folder you should see it's identical to the one in Visual Studio. You may learn how to generate a Web.config specifically for the deployment server.