+   - Open the local configuration (config) file.
+   - Select **Open Delta File** from the **Environments** menu and load the appropriate override configuration (dconfig) file.
+   - Set the **Environment Configuration File** property in the properties pane for the environment to the path and name for the merged configuration file for that environment.
+   - Right-click on the title of the environment and click **Export Merged Environment Configuration File**.

5. Deploy the merged configuration file in the target environment.

Enterprise Library also contains a command-line utility named MergeConfiguration.exe that you can use to merge configuration and delta files if you do not have the configuration console deployed on your administrator system. It can also be used if you wish to automate the configuration merge as part of your deployment process. Information about MergeConfiguration.exe is included in the documentation installed with Enterprise Library.

> *You cannot use environmental overrides with redirected sections or inherited configuration settings. You can only use them when the entire configuration of your application is defined within a local configuration source.*

For more information on all of the scenarios presented here, see the documentation installed with Enterprise Library and available online at http://go.microsoft.com/fwlink/?LinkId=188874.