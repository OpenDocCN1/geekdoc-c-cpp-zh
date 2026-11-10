
- The **NOT A BATCH INPUT SESSION** checkbox sets the flag to use the **CALL TRANSACTION** method.
- Click the **START RECORDING** button to run the transaction and capture the steps.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_814_0.png)

**Figure 19.8** Create Recording Screen

- 3. While recording the transaction, try to avoid any errors, because the error steps will also be recorded. Once the recording is complete, you can see all the screen-related information being captured, as shown in Figure 19.9.

  ![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_814_1.png)

  **Figure 19.9** Screen Recorder Data

- 4. Save the recording by clicking the Save button in the toolbar, and click the Back button to go back to the initial screen of the transaction recorded.
- 5. On the initial screen of Transaction Recorder, select the recording and click the Program button, as shown in Figure 19.10.

  ![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_815_0.png)

  **Figure 19.10** Create Program from Recording

- 6. In the Generate Program window, provide the Program Name and select the options shown in Figure 19.11.

  ![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_815_1.png)

  **Figure 19.11** Generate Program

The Read from File option generates additional code to allow the program to upload the data from a sequential file. The sequential file should have the fields in the same order as the structure of the internal table generated in the program (see Figure 19.12). The Test Data section allows you to generate the test data file in the application server directory, which the generated program can read.

```text
*** Generated data section with specific formatting - DO NOT CHANGE ***
data: begin of record,
* data element: MATNR
  MATNR_001(18),
* data element: MBRSH
  MBRSH_002(001),
* data element: MTART
  MTART_003(004),
* data element: XFELD
  KZSEL_01_004(001),
* data element: MATKL
  MATKL_005(009),
* data element: MEINS
  MEINS_006(003),
* data element: MATKL
  MATKL_007(009),
  end of record.
*** End generated data section ***
```

**Figure 19.12** Structure for Sequential File

The selection screen of the generated program, as shown in Figure 19.13, provides you the option to process the program using either the `SESSION` method or the `CALL TRANSACTION` method.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_816_0.png)

**Figure 19.13** Selection Screen of Generated Program

When processing via the `CALL TRANSACTION` method, the transaction is called immediately and the records are processed immediately. If the `SESSION` method is used, the program generates a session that can be processed later. The records will be updated when the session is processed. You can automate processing the session by scheduling a batch job to run program `RSBDCSUB`.

To process a session manually, proceed with the following steps:

- 1. Go to Transaction SM35.
- 2. Select the session from the list and click the Process button (see Figure 19.14) to process the session. If any errors occur during the processing, you can check the error log to identify the cause of the error.
- 3. After correcting the error, the session can be processed again to post only the records that returned an error. This ensures data consistency and avoids the same records being updated twice.
- 4. On the selection screen of the generated program, as shown in Figure 19.13, the KEEP SESSION checkbox ensures the session isn't deleted after successful processing, assuming no errors occur. If the KEEP SESSION checkbox isn't selected, the session will be deleted if all transactions are processed successfully.

  ![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_817_0.png)

  **Figure 19.14** Processing Session

- 5. You can also generate a function module from the recording via Transaction Recorder. The function module will act as an interface to transfer the data into the SAP system. Each field of the recording will be added as a parameter to the function module.
- 6. When processing the batch input session, the system uses the authorizations of the user currently processing the session. If the batch input session is executed using a background job, then you can assign the username of a user whose authorizations should be used to process the session.

## 19.2 Business Application Programming Interface

BAPIs are standard SAP interfaces that play an important role in the technical integration and exchange of data between different systems, including communication between SAP systems and between SAP and non-SAP systems.

BAPIs are integrated at the business level, which allows them to encapsulate underlying technical details and provide greater stability to integrate various systems.

BAPIs are typically used in the following scenarios:

- Connecting to third-party systems and software
- Connecting to legacy systems
- Implementing distributed environments in which different business components are implemented across various systems
- Enabling communications between PC programs, such as desktop applications developed using Visual Basic and so on, and SAP systems
- Connecting SAP systems to the Internet

In this section, we'll look at the different object types and components that can be accessed through BAPIs, the steps and tools used for developing BAPIs, the use of standardized BAPIs for implementing standard functionality, and finally the steps for implementing a BAPI.

### 19.2.1 Business Object Types and Business Components

BAPIs allow access to the business object types in an SAP system, and business object types allow you to break the SAP system into individual components that are easy to manage and that reduce complexity.

To understand the role of BAPIs, we need to understand what constitutes a business component and a business object type:

- **Business component**
  
  A *business component* consists of business objects and provides autonomous functions. For example, the Human Resources business component consists of a business object type employee.

- **Business object type**
  
  A *business object type* represents one business entity. It includes the data and functions of this entity.

- **BAPIs**
  
  BAPIs are added as an API method to the business object type. They allow object-oriented access to the SAP system through the methods of the business object types. BAPIs and business object types together define the interface at the business level. For example, a purchase order business object type can have different BAPIs added as API methods to create a purchase order, edit a purchase order, or display a purchase order.

Business object types allow you to structure data and processing according to business criteria. Because BAPIs are defined as API methods of business object types, many external applications can gain object-oriented access to the SAP system.

### 19.2.2 BAPI Development via BAPI Explorer

To help you find existing BAPIs in the SAP system and develop new BAPIs, SAP provides a tool called *BAPI Explorer*.

BAPI Explorer (Transaction BAPI) integrates all the tools required to develop and maintain BAPIs. Using BAPI Explorer, you can search for available BAPIs in the system either by application area or by alphabetical order, using the HIERARCHICAL tab or ALPHABETICAL tab, respectively, as shown on the left-hand side of the screen in Figure 19.15.

On the right-hand side of the screen (see Figure 19.15), BAPI Explorer contains different tabs that provide various information about the BAPI in the following areas:

- **DETAILS**
  
  Provides the business object details, such as the object name, object type, package, component, release version, and so on, as shown in Figure 19.15.

- **DOCUMENTATION**
  
  Displays the BAPI documentation, which helps explain the purpose and usage of the BAPI. Each BAPI should be well-documented during implementation to help external developers understand the BAPI’s usage.

- **TOOLS**
  
  Contains tools to create a web service from a BAPI and change the definition of the business object type.

- **PROJECT**
  
  Allows you to create a new project and carry out all the activities to implement a BAPI.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_820_0.png)

**Figure 19.15** BAPI Explorer

The external application developer can call BAPIs as methods of the business object types without needing to understand underlying technical complexities of the business process. Technically, BAPIs are implemented as *remote-enabled function calls* (RFC). RFC is SAP's own standard protocol to allow functions in remote systems to be called.

A BAPI development can be divided into four phases:

- 1. **Analysis**
  
  In the analysis phase, you determine which business process should be implemented using the BAPI. In this phase, you identify the business scenarios and
