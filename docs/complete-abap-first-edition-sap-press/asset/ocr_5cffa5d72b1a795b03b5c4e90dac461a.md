# ## 19.2 Business Application Programming Interface

BAPIs are standard SAP interfaces that play an important role in the technical integration and exchange of data between different systems, including communication between SAP systems and between SAP and non-SAP systems.

BAPIs are integrated at the business level, which allows them to encapsulate underlying technical details and provide greater stability to integrate various systems.

BAPIs are typically used in the following scenarios:

+   - Connecting to third-party systems and software
+   - Connecting to legacy systems
+   - Implementing distributed environments in which different business components are implemented across various systems
+   - Enabling communications between PC programs, such as desktop applications developed using Visual Basic and so on, and SAP systems
+   - Connecting SAP systems to the Internet

In this section, we'll look at the different object types and components that can be accessed through BAPIs, the steps and tools used for developing BAPIs, the use of standardized BAPIs for implementing standard functionality, and finally the steps for implementing a BAPI.

# ### 19.2.1 Business Object Types and Business Components

BAPIs allow access to the business object types in an SAP system, and business object types allow you to break the SAP system into individual components that are easy to manage and that reduce complexity.

To understand the role of BAPIs, we need to understand what constitutes a business component and a business object type:

+   - **Business component**
+     A *business component* consists of business objects and provides autonomous functions. For example, the Human Resources business component consists of a business object type employee.