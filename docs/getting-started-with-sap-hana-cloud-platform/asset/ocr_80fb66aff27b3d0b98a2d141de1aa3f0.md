# ## 10.4 Implementing a Simple SOAP-to-SOAP Scenario

Back in Section 10.2, we discussed the different use cases for SAP HCI. As you’ll recall, one such use case was the ability to integrate a cloud application with an on-premise application. To understand this use case in a little more detail, consider an example where a cloud-based custom application needs to exchange data with an on-premise application, and both applications can be interfaced to and from using the SOAP adapter. In such a case, SAP HCI can be used as the ESB to perform integration using a simple SOAP-to-SOAP integration flow.

The general steps in implementing such a SOAP-to-SOAP scenario are as follows:

+   1. Create an initial integration flow.
+   2. Configure the sender system, receiver system (name of the sender and receiver system; this is optional), and sender authorization (this is the public key pair).
+   3. Import the WSDL file from the SAP PI repository or local file system.
+   4. Create a parameters file that contains attributes and metadata that can be referenced from the communication channels.
+   5. Create a mapping between sender and receiver systems, or import existing mapping objects from the SAP PI repository.
+   6. Create sender and receiver communication channels.
+   7. Deploy the integration project.
+   8. Monitor the project to make sure everything is running smoothly.

Each of these steps is discussed in more detail next.

# ## 10.4.1 Creating an Integration Flow

To create your initial integration flow, follow the steps below:

+   1. Switch to the Integration Designer perspective by going to WINDOW • OPEN PERSPECTIVE. Choose OTHER and then INTEGRATION DESIGNER.
+   2. Create an integration project by clicking on the PROJECT EXPLORER palette and selecting NEW • OTHER.
+   3. Then, select INTEGRATION PROJECT from the SAP HANA CLOUD INTEGRATION folder (see Figure 10.6).