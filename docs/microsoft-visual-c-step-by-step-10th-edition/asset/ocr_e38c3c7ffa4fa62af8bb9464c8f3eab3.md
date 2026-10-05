8. In the firstName field, type O%, in the lastName field, type %a%, leave the other fields at their default value (%), and select Execute. This search should return all customers whose first name starts with O and that have an a somewhere in their last name. The query should return three customers, with Ids 348, 452, and 29511.

9. Try some searches of your own. When you're finished, close the web browser, close the Debug Console window, and return to Visual Studio.

The web API is currently running IISExpress on your computer. To make it available to other users, you should deploy it to Azure. You can do this by using the Publish wizard available with Visual Studio 2022, as described in the following exercise.

# Deploy the web service to the cloud

+   1. In Solution Explorer, right-click the AdventureWorksService project, and then select Publish.

+   2. In the Publish wizard, on the Target page, select Azure, and then select Next.

![](bbox=[0.166, 0.506, 0.882, 0.893])