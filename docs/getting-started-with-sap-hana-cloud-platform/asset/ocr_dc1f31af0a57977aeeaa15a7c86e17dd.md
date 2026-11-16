developers working together pays off in the long term. In such a team, a reasonable question arises: How can you scale out the development process in order for people not to depend on each other all the time? We’d strongly recommend exploring SAPUI5 Mock Server for that purpose.

# What Is SAPUI5 Mock Server?

SAPUI5 Mock Server mimics OData backend calls, simulating an OData provider that runs completely in the client (browser). We strongly recommend this for experimenting with different options for backend calls while designing the UI, thus eliminating the overhead to develop throughput code that might have to be changed multiple times before the user interaction and the UI are finalized.

To instantiate SAPUI5 Mock Server, create an instance of sap.ui.core.util.MockServer in your JavaScript tier, and then use the .start() method to start the server.

Important: Make sure to comment out that functionality once you’re ready with the final version of the UI!

Now that we’ve clarified the basic setup, let’s explore the different UI-level artifacts that may be delivered as part of an extension application. To start, frontend artifacts define content, structure, and metadata. All of these are delivered as part of the extension solution.

As you can see in Figure 11.4, UI artifacts are handled in multiple different layers in SAP HCP and in the extended solution. SAP HCP is being integrated deeply in all SAP Cloud solutions in order to enable a seamless experience for both administrators and end users.

![](bbox=[0.146, 0.62, 0.54, 0.86])

Figure 11.4 Types or UI-Related Artifacts and Where They Are Handled during Installation