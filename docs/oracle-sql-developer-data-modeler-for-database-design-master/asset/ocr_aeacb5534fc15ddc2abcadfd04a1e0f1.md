# 106 Oracle Developer Data Modeler for Database Design Mastery

![](bbox=[0.118, 0.116, 0.178, 0.143])

TIP
For the Preferred Abbreviation property, you do not actually need to define an abbreviation. You can also use it, for instance, if you want to have singular names in entity names and plurals in table names. For example, you can type STUDENT for the entity Name and type STUDENTS for the entity. Then select both Name Translation and Use Preferred Abbreviations when engineering. Now your tables will have plural names, while your entities will still have singular names. Make sure to leave the Preferred Abbreviation property empty for those entities and attributes you do not want to use abbreviations for relational objects.

![](bbox=[0.118, 0.437, 0.178, 0.464])

TIP
You can also use the Name Abbreviations utility on the Tools menu to convert abbreviations to names, and vice versa. You will learn more about that in Chapter 8.

If you select For Columns From Entity Hierarchies, the column names for tables in hierarchies will have the table name as a prefix for a foreign key or a primary key column even though you might have Applied Name Translation and Use Preferred Abbreviations for all other column names. If Prefix Columns From Entity Hierarchies is not selected, the same rules for other tables will be followed.

Sometimes there are technical columns you would like to add to your tables, but there is no need to have those on your entities. These columns could be, CreatedDate, Creator, ModifiedDate, and Modifier. There is a simple way of adding these columns to every table or a set of tables with Data Modeler during the Engineer To Relational Model transformation. All you need is a table called_template that will include only the columns you want to add to other tables. In this example, that would be table_template (CreatedDate, Creator, ModifiedDate, Modifier). On the Engineer To Relational Model screen, first select all the tables where you want to add those columns and select Use Template Table. Then select the table_template from the Use Template list and click Engineer. You do not need to worry if you have already created the columns because the functionality will add the columns only if they have not been added.