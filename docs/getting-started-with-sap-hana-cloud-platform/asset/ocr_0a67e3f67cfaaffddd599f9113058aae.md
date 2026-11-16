Kepler can be downloaded at https://www.eclipse.org/downloads/packages/release/kepler/sr2.

After installing Eclipse Kepler, you will need to install the appropriate SAP HCI plug-ins in Eclipse in order to have the necessary artifacts for creating, designing, and monitoring integration flows. Proceed as follows to add the plug-ins:

+   1. From the main menu, choose Help • INSTALL NEW SOFTWARE....

+   2. On the AVAILABLE SOFTWARE page of the install wizard, add the update site URL: https://tools.HANA.ondemand.com/kepler.

+   3. Select from the following three options:

+   Show only the latest version of AVAILABLE SOFTWARE

+   GROUP ITEMS BY CATEGORY

+   CONTACT ALL UPDATE SITES DURING INSTALL TO FIND REQUIRED SOFTWARE

+   4. Select the SAP HANA CLOUD INTEGRATION TOOLS category.

+   5. Click on NEXT.

+   6. Check the features selected for installation and click on NEXT.

+   7. Accept the terms of the licensing agreement and click on FINISH.

+   8. Restart the Eclipse IDE.

The Eclipse plug-in contains the following features:

+   Designer for SAP HCI

This feature contains plug-ins to develop and configure integration flows.

+   Operations for SAP HCI

This feature contains plug-ins to perform administrative tasks related to SAP HCI runtime clusters and to monitor integration flows.

+   Certificates and security artifacts

Depending on the type of scenario you mind, designing and deploying integration flows on an SAP HCI tenant requires you to take security aspects into consideration. Different types of security artifacts might need to be included. This could include SSL (certificate authority, private key, and public key) and SSH (private and public keys). Note that many CAs are currently supported (including SAP Passport CA), and more will be added as time goes by.