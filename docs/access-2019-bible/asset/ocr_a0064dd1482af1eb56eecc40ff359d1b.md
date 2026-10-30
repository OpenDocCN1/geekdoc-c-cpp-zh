# FIGURE 32.11

The Export Tables to SharePoint Wizard dialog box specifies the destination SharePoint site.

![](bbox=[0.185, 0.172, 0.752, 0.442])

# Things to Note Before Moving Access Tables to SharePoint

Before attempting to upsize your Access tables to SharePoint, keep in mind the following:

+   - **The export might fail if an Access table name does not conform to SharePoint naming rules.** For example, Access table names may contain spaces and limited punctuation characters, while SharePoint tables are plain text with no spaces. If the export fails, it's likely to be caused by a list-naming violation.
+   - **All the queries, forms, and reports that are based on the linked tables should function as before, with a few exceptions.** Because of incompatibilities between Access and SharePoint data, not every Access data type migrates to SharePoint. The incompatible fields are created in the SharePoint list, but they're added to the SharePoint list as text columns and are left empty.
+   - **Export issues are reported in a table named Move to SharePoint Site Issues, with one row for each problem.** A single Access field may generate multiple rows in the issues table. Most export problems are traceable to data incompatibility issues.
+   - **During the export process, several fields will be added to the SharePoint list that are required for list management on the SharePoint site.** These fields will be available in the linked table in Access but are not included in any of the queries, forms, or reports based on the table before it was exported to SharePoint. These additional fields are listed in the following table. It's possible that you may be able to make use of at least some of these columns, but by and large, they serve no purpose in an Access application.