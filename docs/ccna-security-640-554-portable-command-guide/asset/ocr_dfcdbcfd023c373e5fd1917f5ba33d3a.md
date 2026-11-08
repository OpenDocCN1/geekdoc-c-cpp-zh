Next, create the Dynamic NAT network object.

Click **Add > Network Object** a second time, and click the drop-down NAT arrows to display the configurable NAT parameters.

Then do the following:

+   - Enter the NAT network object name.
+   - Identify the inside network address and subnet mask.
+   - Check the **Add Automatic Address Translation Rules** box.
+   - Identify the type of NAT as Dynamic (other options include Dynamic PAT and Static).
+   - Click the **Translated Addr** ellipsis (...) to open the Browse Translated Addr window.
+   - Select the public pool network object name and click **OK**.

Figure 21-17 shows the revised Add Network Object window.

![](bbox=[0.12, 0.515, 0.65, 0.895])

**Figure 21-17**  Revised Add Network Object Dialog

Review the settings and click **OK** to complete the NAT configuration.

To view the NAT configuration, choose **Configuration > Firewall > NAT Rules**.