# Activate DirSync

Using the Unified Serviceability application, navigate to Tools > Service Activation. From the Server drop-down list, choose the Publisher. Find the Cisco DirSync service, check the box next to it, and click Save. Figure 9-8 shows the DirSync service activated.

![](bbox=[0.093, 0.153, 0.768, 0.597])

**Figure 9-8 *Activating Cisco DirSync***

# Configure the LDAP System

Follow these steps to enable LDAP Sync in CUCM:

+   1. Using the Unified CM Administration application, navigate to System > LDAP > LDAP System.
2. Check the Enable Synchronizing from LDAP Server box.
3. From the LDAP Server Type drop-down, choose the type of LDAP system with which CUCM will synchronize.
4. From the LDAP Attribute for User ID drop-down, select which LDAP attribute will map to the CUCM User ID attribute.
5. Click Save.

Figure 9-9 shows the LDAP System Configuration page.