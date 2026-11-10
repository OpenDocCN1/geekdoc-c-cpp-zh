
In this chapter, we will discuss the different methods and tools that can be used to develop various types of interface programs. We begin in Section 19.1, where we discuss direct and batch input for batch data communication (BDC). In Section 19.2, we look at how Business Application Programming Interfaces (BAPIs) can be used to transfer data into SAP.

From there, in Section 19.3, we look at the various data exchange formats (i.e., EDI/ALE/IDocs), before turning our attention to migrating data from legacy systems using the Legacy System Migration Workbench (LSMW) in Section 19.4. In this section, we’ll include step-by-step instructions of the migration process.

In Section 19.5 and Section 19.6, we discuss web services and OData services, respectively. First, we’ll explore the framework of a web service and the steps for consuming a web service. Then, we’ll look at the process of creating OData services, including data model definition, service maintenance, and service implementation.

Section 19.7 walks through serialization and deserialization via XSL transformations and Section 19.8 offers a brief overview of data representation via XML and JSON. Finally, we end the chapter in Section 19.9, with a discussion on ABAP channels.

## 19.1 Batch Data Communication

SAP provides different methods to transfer data into an SAP system, such as via BAPIs, batch input, or direct input. BAPIs are standardized programming interfaces that provide external access to SAP data and business processes, which we’ll discuss in Section 19.2.

*Batch input* is a standard technique used to move large volumes of data into an SAP system. The advantage of batch input is that all the transaction-level checks can be performed on the data as if it were entered online, and the data is updated through the transactions.

*Direct input* is similar to batch input in that all the transaction-level checks can be performed on the data. However, with direct input, the data is updated into the database directly as opposed to via transactions. All these data transfer methods allow you to move data from external systems into your SAP system, either as one-time transfers or as regular periodic transfers.

Almost any data transfer project involves the following steps:

- **1. Identifying the data that needs to be transferred**  
  The first step is to identify the data that should be transferred into an SAP system—for example, material master data from a legacy system. Once the data is identified, it should be exported from the legacy system into a flat file. The exported data should be cleaned up to remove any inconsistencies or any old data. You can clean up all the data that was temporarily created and is no longer used, such as one-time customers' data or any materials that no longer exist or don't need to be transferred.

- **2. Identifying the frequency of transfer**  
  The next step is to identify the frequency of data transfer. Based on this, you can identify which data transfer technique is most suitable. For example, if you need to transfer the data only once, a batch input or a direct input method may be more suitable. If the data needs to be transferred frequently and in real time, then using a BAPI might be more suitable.

- **3. Identifying the conversion logic**  
  External data should be converted to an SAP-specific format. For example, if the material number is stored as a ten-character field in the legacy system, it may need to be converted to an eighteen-character field (SAP format) before transferring the data into the SAP system. This is typically done via a transfer program.

- **4. Processing the data transfer program**  
  A transfer program uploads the flat file and processes the data to be transferred into the SAP system. Once the data is processed and converted to SAP format, it will be posted in the SAP system.

- **5. Handling any errors**  
  Any errors that arise during data transfer need to be addressed. For example, if there are errors in the data, the errors should be corrected in the source file and reprocessed.

- **6. Verifying the transferred data**  
  After successful transfer of the data, it needs to be verified to ensure data consistency. For example, if we transferred material master data from a legacy system to an SAP system, the material data should be verified in the SAP system for consistency and completeness after the successful transfer.

As mentioned, there are two methods we use to transfer mass data: direct input and batch input. The direct input method relies on certain function modules to validate the data, whereas a batch input program relies on the screens of the corresponding transaction to validate the data.

These methods are suitable for transferring mass data for one-time transfer or periodic transfer, but they're not suitable if real-time data transfer is required. We typically use these methods when moving data from a legacy system into an SAP system just before go-live.

In the following subsections, we'll discuss the direct and batch input methods in greater detail.

### 19.1.1 Direct Input

SAP provides certain direct input programs that can be used to move data from an external system into an SAP system. These direct input programs typically use function modules to validate the data and update it in the database. The function modules subject the data to the same level of validations as a corresponding transaction. For example, when you create a material master record using Transaction MM01, the transaction validates the data you input on the screen (e.g., material group, unit of measure, etc.).

When the material master data is transferred using the corresponding direct input program, the direct input program subjects the data to the same validations that are performed by Transaction MM01.

For example, a material master record transferred using the direct input program `RMDATIND` will be subjected to same set of validations as a material created using Transaction MM01. Transaction MM01 allows you to create a material manually, whereas the direct input program can be used for bulk transfer.

Table 19.1 lists the direct input programs provided by SAP for different application areas.

**Table 19.1** Direct Input Programs

| Program | Application | Description |
|---|---|---|
| `RFBIBL00` | FI | Used for entering accounting documents and clearing open items |
| `RMDATIND` | MM | Transfers material master data |
| `RVASSO` | SD | Creates billing documents |
| `RAALT011` | AM | Direct data import for asset accounting |
| `RKEVEXTG` | CO-PA | Transfers external data to CO-PA |

A direct input program is faster than a batch input program because it doesn't depend on transaction screens to validate the data. Direct input programs are executed in the background and support error reporting. In case of any errors, the data transfer can be resumed after correcting the errors. A background job can be scheduled to run the programs at regular intervals.

Direct input programs are run in the background and managed using Transaction BMVO (see Figure 19.1). Running direct input programs in the background is the preferred method for production runs, but you can also execute these programs in the foreground for testing the data transfers.

The program documentation for each of the direct input programs provides more information on their usage.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_806_0.png)

**Figure 19.1** Direct Input Management

### 19.1.2 Batch Input

Unlike direct input programs, batch input programs rely on the corresponding transactions to validate the data. Batch input programs allow you to capture the steps involved in processing the data and automate this process.

For example, to create a material, you'd go through the following steps:

- **1. Go to Transaction MM01, which will take you through a series of screens in which you input certain details on each screen. For this example, input the MATERIAL, INDUSTRY SECTOR, and MATERIAL TYPE on the initial screen of Transaction MM01, as shown in Figure 19.2.**  
  ![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_807_0.png)
  
  **Figure 19.2** Initial Screen of Transaction MM01

- **2. On the next screen, select the view to input further data, as shown in Figure 19.3.**  
  ![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_807_1.png)
  
  **Figure 19.3** Second Screen of Transaction MM01

- **3. The system will present the selected view, and you can input further details of the material, such as its description, MATERIAL GROUP, BASE UNIT OF MEASURE, and so on, as shown in Figure 19.4.**

- **4. Once the information is entered, click the SAVE button to create a material.**
