
# 290 Oracle SQL Data Modeler for Database Design Mastery

and in Synchronize Data Dictionary With Model it is the database. If you do not want to use the synchronizing functionality to compare the database, there are a couple other options: import DDLs or import from a data dictionary.

The difference between these methods is at the beginning of the process: All these methods end up at the same Compare Models dialog introduced in the previous section. The only difference is in Synchronize Data Dictionary With Model because the Compare Models screen for that also includes a Sync New object.

If you are using the synchronization functionality to compare the database, you need to create a connection to the database if you have not done so before. There is no particular place to create a connection, but it can be done with Import. Choose File | Import Dictionary. Click Add to create a new connection and insert the information needed for the connection. Test the connection works by clicking Test, and when you are done with it, click Save. Now the connection is created, and you do not need to continue with the importing anyone, so click Cancel.

With the Synchronize Model With Data Dictionary button, you can view what has changed in the database and get those changes to your model. Click the arrow pointing to the left, as shown in Figure 12-4. Select your connection from the Redirect Connection and click OK. Now you will see the Compare Models dialog. Data Modeler suggests that the objects that exist only in the database should be added to the design, and the objects that exist only in the design and not in the database should be removed from the database. You can use this comparison to get changes made directly to the database to the design as well. Select the changes you want to perform. You can view the DDL preview before clicking the Merge button to make sure your model is updated the way you want. You can also use the DDL script Data Modeler gives you to alter the database. Check the design before saving it to what you want.

![](img/431f8ac8f273fa89a28377c500ed60d7_316_0.png)

FIGURE 12-4. Synchronize Model With Data Dictionary and Synchronize Dictionary With Model buttons

# Chapter 12: Comparing Designs and the Database 291

With the Synchronize Data Dictionary With Model button, you can see what has changed in the design and make those changes to the database. Click the arrow pointing to the right, as shown in Figure 12-4. Select your connection from the Redirect Connection list and click OK. You will see the Compare Models dialog again. Data Modeler shows the objects that exist only in the database should be deleted from the database and the objects that exist only in the design should be added to the database. You can use this comparison when you have made changes to the design but have not implemented them in the database yet. Note that the Merge button is not disabled in Figure 12-4 because there are no changes that can be performed in the design. Note also that there is a new button called Sync New Objects when synchronizing the data dictionary with the model. Select the changes you want to perform and order the DDL preview. Check that the script is correct and save it. Run the script in the database. This is the ALTER script to change your database to match the model. Depending on what you have selected, this script can include elements for creating new objects in the database and for deleting or altering objects.

You can also use the DDLs that were used for creating the database to make comparisons against the design. Choose File | Import | DDL File to do. You can either compare to the existing relational model in the design (target) or create a new relational model based on the DDLs. If you want to import the DDL design as the target, you can select Swap Target to change the model from the DDL as the target. You then select the database site (RDBMS site) to be compared to. After that, you can view the log in the View Log dialog and save it if desired. Another option is to import from the data dictionary. Select the desired connection and select the schemas to import, the relational model where to import them, the desired The same Compare Models screen will open that that you have seen before. If you want, you can select Swap Target Model as explained earlier. Select the objects you want to import. The Compare Models screen will open.

For example, suppose somebody has changed the name and data type of a column in the database. The Compare Models dialog does not know. It shows that there is a column in the design that does not exist in the database, and vice versa. Select the column on the source and right-click. Map To Existing Column and select the column it should be mapped to. You have just created a compare mapping, and Data Modeler will remember it the next time you do a comparison. This is only for comparisons between the design and a database, a DDL script, or a data dictionary. If you compare two designs, Data Modeler recognizes it is the same column, and there is no need to create a compare mapping. You can see the existing compare mapping in Design Properties, as shown in Figure 12-5. If you want to perform the operation (change the name and data type), click Merge.

# 292 Oracle SQL Developer Data Modeler for Database Design Mastery

![](img/431f8ac8f273fa89a28377c500ed60d7_318_0.png)

# Summary

There are several ways of comparing designs to each other and comparing a design to a database. As a result of a comparison, you can also change the design or the database accordingly.

Designs can be compared either with the Import functionality or with Compare/Merge. Import compares all the design, whereas Compare/Merge only the relational models.

A design and a database can be compared either with synchronization or by importing the DDLs for creating the database. Compare/Merge on the design gets the DDLs to change the data type of a column. There are several parameters that can get the kind of DDLs you want. Remember to always check the DDLs before running them.

# Symbols

- * (asterisk) for global search, 273, 277
- as quantifier, 274
- {} (curly braces), as quantifier, 274

# B

- bitmap join indexes, 161
- Boolean domain, list of values, 29, 30
- Branch/Tag option, Subversion, 215
- branches, design, 225–228
- Browser pane, Data Modeler, 12–14
- bubble help, New, 43–44
- business information, adding to Data Modeler 55–56

# A

- Abbreviated Only, naming standards, 22, 23
- abbreviations, name, 130–132
- Add New Prefix, 134
- Adequate Normalized property, logical model, 96
- administering RDBMS sites, 142–144
- advanced model, search operations, 274–276
- agile database design, 2–4
- Allow Columns Reader During Engineering, relational model, 93–94
- analytic workspace (AW), Oracle, 194, 200–201
- AND button, advanced method, 275
- application design, database design vs., 2–3
- Apply Name Translation, Engineer to Relational Model, 104–105, 111
- arc, definition of, 81
- arc solution engineering of, 112, 114
- in inheritance, 81–82
- * (asterisk) for global search, 273, 277
- as quantifier, 274
- Attribute Properties dialog defining domain constraints, 80, General tab of, 65–66
- sensitive data and, 71
- as constraints, 76–80
- of entity properties, 45–46
- marked as deprecated, 67
- overlapping, 100
- with property deprecated, 275
- relationship, 74–75
- setting to not null, 79
- types of, 65–66
- Auto Increment Column Templates settings, 140–141
- Available Collections, Custom Reports Template dialog, 262, 263
- Available Objects box, permissions dialog, 147
- Available Reports, 259–260
- AW (analytic workspace), Oracle, 194, 200–

# 293

![](img/431f8ac8f273fa89a28377c500ed60d7_319_0.png)
