+   - **Business object type**
+     A *business object type* represents one business entity. It includes the data and functions of this entity.
+   - **BAPIs**
+     BAPIs are added as an API method to the business object type. They allow object-oriented access to the SAP system through the methods of the business object types. BAPIs and business object types together define the interface at the business level. For example, a purchase order business object type can have different BAPIs added as API methods to create a purchase order, edit a purchase order, or display a purchase order.

Business object types allow you to structure data and processing according to business criteria. Because BAPIs are defined as API methods of business object types, many external applications can gain object-oriented access to the SAP system.

# 19.2.2 BAPI Development via BAPI Explorer

To help you find existing BAPIs in the SAP system and develop new BAPIs, SAP provides a tool called *BAPI Explorer*.

BAPI Explorer (Transaction BAPI) integrates all the tools required to develop and maintain BAPIs. Using BAPI Explorer, you can search for available BAPIs in the system either by application area or by alphabetical order, using the HIERARCHICAL tab or ALPHABETICAL tab, respectively, as shown on the left-hand side of the screen in Figure 19.15.

On the right-hand side of the screen (see Figure 19.15), BAPI Explorer contains different tabs that provide various information about the BAPI in the following areas:

+   - **DETAILS**
+     Provides the business object details, such as the object name, object type, package, component, release version, and so on, as shown in Figure 19.15.
+   - **DOCUMENTATION**
+     Displays the BAPI documentation, which helps explain the purpose and usage of the BAPI. Each BAPI should be well-documented during implementation to help external developers understand the BAPI’s usage.