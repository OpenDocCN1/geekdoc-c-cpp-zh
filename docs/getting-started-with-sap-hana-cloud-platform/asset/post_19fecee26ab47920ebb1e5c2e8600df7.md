
**Note**
You can define your own set of integration flow patterns; these are the so-called user-defined templates.

6. Click on the Finish button to complete the initial creation steps.

The resulting integration flow generated from the point-to-point channel template looks like the image shown in Figure 10.8.

![](img/cf7012644082c115a2181376d9b7486d_443_0.png)

Figure 10.8 Basic Integration Flow from the Point-to-Point Channel Pattern Template

Now it's time to extend this empty integration flow and further configure it.

## 10.4.2 Configuring Sender and Receiver Systems

To properly configure the sender and receiver systems, follow the steps below:

- 1. From the integration flow presented in Figure 10.8, click on the sender system (on the left side of the diagram), check the property area, and enter an appropriate name without whitespaces for your sender system.
- 2. Under SENDER AUTHORIZATION, click on the Browse option to import your public SSL key (see Figure 10.9). Adding the SSL key is required for certificate-based authentication.

![](img/cf7012644082c115a2181376d9b7486d_444_0.png)

- 3. Repeat the previous steps to configure the receiver system name. Note that there is no need to browse for the public key on the receiver side.

## 10.4.3 Importing WSDL Files from SAP PI or Your Local File System

For the sake of simplicity, we will assume that you will reuse existing service interfaces for this scenario. You will then need to import them from your ESR. In order to import the service interfaces, proceed as follows:

- 1. Right-click on the name of the integration project in the PROJECT EXPLORER palette, choose the IMPORT PI CONTENT option, and choose the type of artifact to be imported. You will be asked to choose from among MESSAGE MAPPING, OPERATION MAPPING, and INTERFACE. For this example, choose the INTERFACE option, which will load the list of service interfaces for you to choose from. After selecting the desired service interface, click on the FINISH button.
- 2. Import the WSDL/service interface for the receiver system as well. These two service interfaces (for the sender and receiver) will be used during mapping. Note that the WSDL file could also be imported from a local file system instead of the ESR.

## 10.4.4 Creating a Parameters File

The parameters file contains the reference parameters to be used in your integration flow. Parameters can be created for a variety of attributes. A typical example includes the location of the WSDL file and the endpoint to be used during the configuration of the communication channels. To create the parameters file, proceed as follows:

- 1. Right-click on the integration project and choose New > Other. From the subsequent screen, select GENERAL and then FILE. Enter “parameters.prop” for the file name.
- 2. Follow the wizard, and make sure that the newly created file is saved in the src/main/resources directory.
- 3. Click on the Finish button.
- 4. Populate the newly created file with different parameters and their corresponding values (see Figure 10.10 for an example configuration file).

![](img/cf7012644082c115a2181376d9b7486d_445_0.png)

Figure 10.10 Parameters File

To reference these parameters during the configuration of a communication channel, the values on the left-hand side of the = sign are enclosed in double curly braces—for example, {{SOAP_soapWsdlURL}}.

## 10.4.5 Mapping between Sender and Receiver Systems

There are two possible ways to implement the mapping between the sender and receiver:

  - Reuse an existing mapping.
  - Create a new mapping from within SAP HCI Designer.

If you opt to create a new mapping, then proceed as follows:

- 1. Right-click on the integration project and select New > Other. Under SAP HANA CLOUD INTEGRATION, choose MESSAGE MAPPING, and then follow the wizard.
- 2. Specify the name of the message mapping, and click on FINISH.
- 3. The Overview screen of the newly created mapping opens. Choose the DEFINITION tab to select the source and target structures to be used in your mapping.
- 4. Create a mapping between the source and target structures. The structure needs to be selected from the WSDL file imported earlier (see Figure 10.11). Here, the mapping capability is equipped with a number of predefined functions that can be used for defining the mapping logic.

![](img/cf7012644082c115a2181376d9b7486d_446_0.png)

Figure 10.11 Mapping Definition between Source and Target Structures

- 5. Go back to the integration flow and add a mapping artifact. This can be achieved by using the context menu on the horizontal line between the START and End icons within the INTEGRATION PROCESS box. Select the ADD MAPPING option. A new mapping artifact will be placed.
- 6. Use the context menu on the newly added mapping artifact, and select the ASSIGN MAPPING option. On the resulting selection screen, select the previously created message mapping.

## 10.4.6 Configuring Sender and Receiver Communication Channels

The communication channels need to be configured to the desired adapter type. To configure a communication channel, proceed as follows:

- 1. Right-click on the channel artifact on the sender side. This is the horizontal line between the sender and the INTEGRATION PROCESS box. Choose the CONFIGURE CHANNEL option.
- 2. The integration flow jumps into the CHANNELS tab. From there, provide a name for the communication channel and choose the desired adapter type. In this case, choose the SOAP adapter.
- 3. You will also need to go to the ADAPTER SPECIFIC tab to specify further adapter details. The details to be specified include the endpoint and a link to a WSDL URL. The parameters defined in the parameters.prop file can be used here.
- 4. You will need to perform the same configuration steps for the receiver communication channel.

The final configuration of the integration flow looks like the one presented in Figure 10.12.

![](img/cf7012644082c115a2181376d9b7486d_447_0.png)

Figure 10.12 Final Simple Integration Flow Configured in SAP HCI

If a red marker appears on the integration project after saving, then that signals that the configuration is not complete. Please check the problem console to see more details about the error.

## 10.4.7 Deploying the Integration Project

Once all the configurations are done and all the changes saved, it's time to deploy the integration flow to your SAP HCI tenant. To deploy the project to the cloud, right-click on the project and choose the DEPLOY INTEGRATION CONTENT option. A popup will ask for the tenant ID. Once you've provided the ID, the deployment will be performed.

## 10.4.8 Monitoring

To monitor your flows directly from the Eclipse IDE, switch to the INTEGRATION OPERATION perspective. Figure 10.13 shows the sample messages received by SAP HCI and further detail; different search functionalities can be used from the monitoring tool.

![](img/cf7012644082c115a2181376d9b7486d_448_0.png)

Figure 10.13 Message Monitoring from the Eclipse IDE

In Message Monitoring, you can search messages based on different filtering criteria. The monitoring screen shows different messages that have been received by a server. You can also see their statuses. Note that this perspective also provides a DEPLOYED ARTIFACTS tab. As its name indicates, this tab lists all the artifacts that have been deployed to the SAP HCI server—including integration flows.

Now that you have a pretty good understanding of what it takes to use Eclipse as the development IDE for SAP HCI, it's time to look at the web UI.

## 10.5 Introduction to the Web UI for SAP HANA Cloud Integration

As an alternative to the Eclipse IDE, you can use the web UI client for SAP HCI. The SAP HCI web UI is a web-based IDE; it’s also known as SAP HCI Spaces. It has numerous advantages compared to the Eclipse IDE. One of the most significant ones is that developers don’t need to install anything locally; there is no need to worry about the consistency of versions between the local IDE and the server. The developer only needs a browser and Internet connection in order to start development activities. This fact alone reduces the development effort and saves costs.

In this section, we will explore the different tools that make up the web UI development platform. The landing page of the web UI can be accessed via http://<operations server url>/<spaces>.

As can be seen on the left side of Figure 10.14, the SAP HCI web UI consists of the following four main sections:

  - DISCOVER
  - DESIGN
  - RUN
  - MONITOR

![](img/cf7012644082c115a2181376d9b7486d_449_0.png)

Figure 10.14 Landing Page of the Web UI

Each of these sections will be explored in more detail next.
