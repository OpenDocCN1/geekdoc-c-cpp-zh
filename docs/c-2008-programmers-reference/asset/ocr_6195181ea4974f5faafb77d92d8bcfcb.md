# Part II: Application Development Using C#

(continued)

```
{
    //---application is not installed using ClickOnce---
    MessageBox.Show("Application is not installed " +
        "using ClickOnce",
        "Updates not available",
        MessageBoxButtons.OK, MessageBoxIcon.Information);
}
```

You first check to see if the application is deployed using ClickOnce. This can be done by using the IsNetworkDeployed property from the ApplicationDeployment static class. If the application is indeed deployed using ClickOnce, you proceed to obtain an instance of the deployment using the currentDeployment property of the ApplicationDeployment class. Using this instance of the deployment, you call the CheckForUpdate() method to check whether there is a newer version of the application available from the publishing server. If there is, you prompt the user by asking if he wants to update the application. If he does, you update the application, using the Update() method. After that, you force the user to restart the application, using the Restart() method.

To test the update, first run an instance of the PhotoViewer application by launching it from the Start menu. Next, republish the application in Visual Studio 2008. Click the Update button to see if an update is available. You should see the prompt shown in Figure 16-28. Click Yes, and the application will be updated.

![](bbox=[0.2, 0.67, 0.85, 0.9])

Figure 16-28