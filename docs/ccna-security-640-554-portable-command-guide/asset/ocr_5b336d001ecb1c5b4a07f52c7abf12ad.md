In this example, informational (level 6) messages will be forwarded to a syslog server located at IP address 192.168.1.100. As well, debugging (level 7) messages will be sent to the router memory buffer.

After configuring these settings, click **OK**.

CCP displays the CLI configuration commands. Click **Deliver** to commit the configuration changes.

CCP now displays the syslog settings, as shown in Figure 6-13.

![](bbox=[0.095, 0.244, 0.719, 0.364])

**Figure 6-13** Revised Syslog Information Screen

**NOTE:** Use the `show logging` command to view logging settings and logging information sent to the memory buffer.

To monitor logging information with CCP, choose **Monitor > Router > Logging**, as shown in Figure 6-14. You can choose the logging information to view from the drop-down list.

![](bbox=[0.093, 0.562, 0.934, 0.932])

**Figure 6-14** Monitoring Syslog Screen