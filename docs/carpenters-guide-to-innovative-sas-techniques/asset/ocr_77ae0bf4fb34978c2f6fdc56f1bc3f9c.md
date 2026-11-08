+   - 1.5 SQL Pass-Through 32
+     - 1.5.1 Adding a Pass-Through to Your SQL Step 32
+     - 1.5.2 Pass-Through Efficiencies 33
+   - 1.6 Reading and Writing to XML 33
+     - 1.6.1 Using ODS 34
+     - 1.6.2 Using the XML Engine 34

A great deal of the process of the preparation of the data is focused on the movement of data from one table to another. This transfer of data may be entirely within the control of SAS or it may be between disparate data storage systems. Although most of the emphasis in this book is on the use of SAS, not all data are either originally stored in SAS or even ultimately presented in SAS. This chapter discusses some of the aspects associated with moving data between tables as well as into and out of SAS.

When moving data into and out of SAS, Base SAS allows you only limited access to other database storage forms. The ability to directly access additional databases can be obtained by licensing one or more of the various SAS/ACCESS products. These products give you the ability to utilize the SAS/ACCESS engines described in Section 1.1 as well as an expanded list of databases that can be used with the IMPORT and EXPORT procedures (Section 1.2).

# ### SEE ALSO

Andrews (2006) and Frey (2004) both present details of a variety of techniques that can be used to move data to and from EXCEL.

# # 1.1 LIBNAME Statement Engines

In SAS®9 a number of engines are available for the LIBNAME statement. These engines allow you to read and write data to and from sources other than SAS. These engines can reduce the need to use the IMPORT and EXPORT procedures.

The number of available engines depends on which products your company has licensed from SAS. One of the most popular is SAS/ACCESS® Interface to PC Files.

You can quickly determine which engines are available to you. An easy way to build this list is through the NEW LIBRARY window.

From the SAS Explorer right click on LIBRARIES and select NEW. Available engines appear in the ENGINE pull-down list.

Pulling down the engine list box on the 'New Library' dialog box shown to the right, indicates the engines,

![](bbox=[0.426, 0.669, 0.891, 0.909])