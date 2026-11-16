3. As the import runs, you'll encounter the confirmation dialog box shown in Figure 7.32. This dialog box is alerting you to the fact that the archive file contains files that will overwrite the current files you've defined in the application. You'll want to click on the OK button to proceed with the import.

![](bbox=[0.15, 0.195, 0.82, 0.515])

Figure 7.32 Importing the Sample Customer Project into the SAP Web IDE: Part 3

After the archive is imported, you'll see some new SAPUI5 content that displays relevant data from the backend OData service. To test this out, repeat the deployment steps outlined in Section 7.2.3 and Section 7.2.4. That is, you'll need to check the revised code in the Git repository and activate the changes in the SAP HCP Cockpit.

Figure 7.33 shows the finished product in action in a browser window. As you test through the application, you can use the developer tools in the browser to monitor the network traffic and see the OData service calls happening behind the scenes. This is demonstrated in Figure 7.34.