**NOTE:** Use the `show ssh` command to display the SSH connection’s status. Use the `show ip ssh` command to display the SSH version and SSH configuration data.

# Securing VTY Access with SSH Using CCP Example

Choose **Configure > Router > Router Access > VTY** to open the VTY information screen (see Figure 6-1).

![](bbox=[0.056, 0.218, 0.882, 0.543])

**Figure 6-1**   VTY Information Screen

Click **Edit** to change the vty parameters.

In the example in Figure 6-2, the vty interface is set with an executive timeout of 5 minutes (the default is 10) and accepts only incoming SSH connections from hosts identified in the ADMIN-IN ACL. The ACL specified must be preconfigured on the router.