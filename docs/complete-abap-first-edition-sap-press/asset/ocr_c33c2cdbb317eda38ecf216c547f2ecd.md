+   - **Screen exits**
+   
+     *Screen exits* allow you to enhance standard SAP program screens to add custom fields. For example, if you want to capture additional information while creating a purchase order using the standard SAP Transaction ME21N, then you can use the screen exit to add additional fields to the Transaction ME21N screen.

+   - **Menu exits**
+   
+     Using a *menu exit* (or GUI exit), you can enhance the standard SAP menu. You can add custom function codes to the GUI status of a standard SAP transaction to provide additional functionality; for example, you can add additional menu items to standard SAP applications to provide additional functionality for the user.

+   - **Field exits**
+   
+     *Field exits* allow you to process the input fields of a screen. These are obsolete and should no longer be used; you should use conversion routines instead. Because these exits are no longer used and not recommended, we won't discuss them further here.

There are different ways to search for a customer exit. You can search using Transaction SMOD, in which you can use `F4` help in the ENHANCEMENT field to search based on the exit name, short description, package, or application component, as shown in Figure 20.17. Another method to search for available enhancements is to use lookup table MODSAP in ABAP Data Dictionary. All enhancements are saved in database table MODSAP, so you can search table MODSAP by using wild cards for a program name (e.g., SAPLV60B).

In addition, customer exits are called in standard SAP programs using the `CALL CUSTOMER` statement; therefore, you can search the standard SAP program code using the `CALL CUSTOMER` keyword to identify the customer exits called in the program. This isn't a straightforward method to find customer exits and may not be useful if many other programs are called from the main program and the call to the customer exit is implemented in one of the called programs.

In this section, first we'll walk through the process of creating a customer exit. Then, we'll look at function module exits, screen exits, and menu exits in more detail.