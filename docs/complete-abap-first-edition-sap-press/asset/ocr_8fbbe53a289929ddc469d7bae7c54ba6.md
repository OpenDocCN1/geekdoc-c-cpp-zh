code, the user can directly input the transaction code in the command field to run the program. Letters A to X are reserved for standard SAP applications; transaction codes for custom applications should be created in the customer namespace Y or Z.

SAP follows a standard naming convention for most of the standard SAP applications. Transaction codes ending with a 1 generally are used for creation, transaction codes ending with a 2 are for editing, and transaction codes ending with 3 are for displaying. The following are some example transaction codes that hold to this pattern:

+   - MM01 (Material Master Create)
+   - MM02 (Material Master Change)
+   - MM03 (Material Master Display)
+   - VF01 (Billing Document Create)
+   - VF02 (Billing Document Change)
+   - VF03 (Billing Document Display)
+   - ME21N (Purchase Order Create)
+   - ME22N (Purchase Order Change)
+   - ME23N (Purchase Order Display)

Transaction codes ending with N are called *enjoy transactions*. Enjoy transactions were released with the SAP ERP release, which was also known as the *Enjoy* release. These transactions implement the Control Framework elements, such as docking containers, custom containers, ALV grids, and picture controls. These transactions replaced older transactions. For example, Transaction ME21N is an SAP enjoy transaction for Transaction ME21.

Next, we'll explain how transactions can be used to navigate within the system and how to open them.

# 3.1.5 Navigating and Opening Transactions

There are couple of ways to open a transaction (application). You can use the tree structure in the **SAP Menu** on the SAP Easy Access screen, or you can input the transaction code in the command field directly.