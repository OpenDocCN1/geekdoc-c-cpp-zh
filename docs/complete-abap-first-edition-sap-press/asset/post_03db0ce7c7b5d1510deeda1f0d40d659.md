
## Using IDocs with EDI

Because EDI involves the exchange of documents directly between computers without any human intervention, a common standard needs to be defined, describing what data is exchanged for a business document and in what format the data is presented. For this reason, there are several EDI standards in use today, such as ANSI, EDIFACT, TRADACOMS, and so on. Each standard also has multiple versions, such as an ANSI5010, EDIFACT version D12, and so on. When two businesses agree to exchange documents using EDI, they agree to use a specific EDI standard and version.

Businesses typically use a translator program to convert the company's internal format to an EDI-specific format before exchanging documents. For example, in an SAP system, when an application document such as a purchase order is created, the data is stored in the database in an SAP-specific format (e.g., the date is stored in YYYYMMDD format). If this application document needs to be sent to a business partner, it has to be converted first to the agreed-upon EDI standard.

Converting the document to EDI standard produces just another way of representing the same data. However, EDI standards keep evolving, and if SAP selects to take on the task of converting application documents to EDI standards, then SAP needs to keep updating its system each time an EDI standard changes. To avoid such a problem, SAP has outsourced the translation to third-party software vendors. The translator software is called the EDI subsystem. Using a third-party subsystem allows SAP not to worry about ever-changing EDI standards; it's the job of the subsystem vendors to update their translation program to keep in sync with the changing standards.

However, there’s still one challenge. SAP needs the flexibility to change its own internal format and application documents. If the subsystem depends on the SAP application data directly, then each time SAP changes its application format, the subsystem needs to be updated to keep in sync with the changes.

To overcome such challenges, SAP uses the IDoc format. When the application document is created in the system, an IDoc is generated based on the application document. IDoc is another way of representing the same data. The subsystem uses the IDoc for conversion to the EDI document. SAP guarantees that no matter how an application changes internally, the subsystem always receives data in a fixed IDoc format. This allows SAP the flexibility to change its internal applications without worrying about the subsystems being affected.

The role of the subsystem is to convert the IDoc to an EDI document and transmit it to the business partner. Similarly, when the EDI transmission is received from a business partner, the EDI subsystem translates the EDI document into an IDoc. Exchange of business documents involves an outbound process, in which a document is sent from your system to a business partner's system, and an inbound process, in which a document is received from a business partner and posted in your system.

We'll discuss the inbound and outbound processes further in the following subsections.

## Outbound and Inbound Processing

[Figure 19.27](#figure-19-27) shows the steps involved in the outbound and inbound processes.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_838_0.png)

**Figure 19.27** Outbound and Inbound Processes

In the outbound process, the application document is first created in the SAP system. If the document needs to be transmitted through EDI (e.g., via message control), then it triggers the EDI process.

In the EDI process, an ABAP program selects the application data from the database and generates an IDoc. This IDoc is then pushed to the OS level, to a specific directory from which the subsystem will pick up the IDoc for processing. The subsystem will first perform a syntax check to ensure the IDoc is in the correct format and all mandatory fields are filled.

The IDoc consists of a control record, multiple data records, and multiple status records:

- **Control record**: The *control record* consists of the general information about the IDoc, such as the type of document (called the message type), the business partner details, and so on. You'll learn more about the control record when we discuss IDoc development in the upcoming subsections.
- **Data records**: *Data records* consist of the actual data of the document.
- **Status records**: *Status records* are updated with the status of the IDoc at each processing step.

The subsystem converts the IDoc to EDI format. It uses the control record of the IDoc to identify the partner details and the message type being exchanged. Based on the message type, the required syntax checks are performed to ensure data consistency. The subsystem takes care of stripping the control record before transmitting the document to the business partner.

Once the IDoc is converted to an EDI document, the subsystem establishes a connection with the business partner's system (either through direct connection to the partner's network or through VAN) and transmits the document. Once the acknowledgment is received from the business partner that the document has been received successfully, the subsystem updates the IDoc with the status message. The IDoc is updated with the status message at each step of the process to help identify any issues.

In the inbound process, the EDI transmission is received by the subsystem and takes care of converting the EDI document to an IDoc. SAP provides program `STARTRFC` to start any RFC-enabled function module from the operating system level. The subsystem uses program `STARTRFC` to call the `EDI_DATA_INCOMING` function module to trigger the inbound processing. The control record of the IDoc is used to identify the partner profile, using which the ABAP posting program is executed.

The posting program processes the IDoc and posts the application document in the SAP system.

The subsystem, even though not part of SAP, plays a crucial role. It takes care of processing IDocs, performs a syntax check on the document before transmission, establishes a connection with the business partner's network to transmit the file, and acknowledges the successful transmission.

### 19.3.2 Application Link Enabling

ALE is a proprietary SAP technology used to create and run distributed applications. ALE allows you to integrate business processes between SAP systems and between SAP and non-SAP systems. When communicating with non-SAP systems, special SAP-certified third-party translator programs are used. ALE allows you to exchange data between application systems in a distributed environment in a controlled and consistent manner.

*A distributed environment* refers to a landscape in which various business functions of an organization are distributed across multiple systems. Due to increased globalization of markets, a distributed environment is required to decentralize such systems. For example, the accounts system is maintained in a central location, with manufacturing systems maintained locally at each plant.

Distributed environments also improve system performance, because different business functions run in different systems as opposed to all business functions running in the same system. ALE is middleware that allows you to integrate different components of a business process. It allows you to integrate processes from vendors and customers; business processes aren't restricted to one organization only, but instead involve vendors and customers as business partners.

The applications of ALE integrated systems are loosely coupled, and the data is exchanged asynchronously using IDocs. Synchronous connections are used to read the data only. Asynchronous exchange of data ensures that the data arrives in the receiver system even if the system is offline when the data is sent.

ALE guarantees the distribution and synchronization of master data, customization data, and transaction data. There are many configurations that need to be set up for ALE integration. Transaction SALE is used to maintain all the required settings in the system.
