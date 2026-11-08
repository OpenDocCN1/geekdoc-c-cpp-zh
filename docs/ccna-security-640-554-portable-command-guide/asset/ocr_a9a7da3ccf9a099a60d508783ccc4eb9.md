# Generating a Mirror Configuration Using CCP

To generate a mirror configuration that you can use as a template for the other peer, click the **Generate Mirror** button. The resulting configuration provides identical IPSec policy names, IKE policies, and transform sets.

To generate a template configuration for the peer VPN router, choose **Configure > Security > VPN > Site-to-Site VPN > Edit Site-to-Site VPN**.

Select the VPN connection that you want to use as a template, and click **Generate Mirror**.

CCP displays the Generate Mirror dialog shown in Figure 17-13.

![](bbox=[0.074, 0.293, 0.587, 0.657])

**Figure 17-13**  Generate Mirror Dialog

**CAUTION:** Do not apply the mirror configuration to the peer device without editing! This configuration is a template that requires additional manual configuration. Use it only as a starting point to build the configuration for the VPN peer.

The suggested configuration for the identified peer device appears on the Generate Mirror dialog.

Click Save to display the Windows Save File dialog, and save the file as a text file.

Open the resulting text file using a text editor such as Notepad and make any needed changes to the template configuration. Figure 17-14 highlights sections of a sample configuration that should be verified or altered.