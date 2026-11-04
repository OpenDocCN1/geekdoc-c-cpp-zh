Import the following namespace:

```
using System.Deployment.Application;
```

Code the Update button like this:

```
private void btnUpdate_Click(object sender, EventArgs e)
{
    //---check if the application is deployed by ClickOnce---
    if (ApplicationDeployment.IsNetworkDeployed)
    {
        //---Get an instance of the deployment---
        ApplicationDeployment deployment =
            ApplicationDeployment.CurrentDeployment;

        //---if there is any update---
        if (deployment.CheckForUpdate())
        {
            DialogResult response =
                MessageBox.Show("A new version of the " +
                "application is available. " +
                "Do you want to update application?",
                "Application Updates",
                MessageBoxButtons.YesNo);

            //---if user wants to update---
            if (response == DialogResult.Yes)
            {
                Cursor.Current = Cursors.WaitCursor;

                //---update the application---
                deployment.Update();

                //---prompt the user to restart---
                MessageBox.Show("Update completed. You need to restart" +
                    " the application.",
                    "Update Completed", MessageBoxButtons.OK,
                    MessageBoxIcon.Information);

                //---restart the application---
                Application.Restart();
            }
        }
        else
        {
            //---application is up-to-date---
            MessageBox.Show("Application is up-to-date.", "Update",
                MessageBoxButtons.OK, MessageBoxIcon.Information);
        }
    }
    else
```