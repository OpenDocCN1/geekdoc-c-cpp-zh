# 164 Oracle SQL Data Modeler for Database Design Mastery

A data definition language (DDL) is for creating database objects. Generating DDL scripts with Oracle SQL Data Modeler is quite simple, and it can be done over and again to find the right settings to get the kinds of scripts. The difficult task is to decide which kind of DDL files you want. Do you want a version of a whole database at a certain time in just one file, or do you want a file per object or something else? Where do you plan to keep the files, and who will have access to them? Are you going to do with these files? Do you need a file for creating a whole database of a particular version? Maybe you also need a file for creating the latest version of the Customer table for production? Before creating the DDL files, you must decide what they are for so you know what you need. You need different versions of DDLs for production and test. How are they different? Where do you keep the DDLs? Chapter 12 talks about comparing models to a database and generating DDL scripts for altering the database objects. Before the DDLs are run in the database, they must be reviewed, and there should be a documented process for that. There should also be clear understanding of who runs the DDLs on the database and when and how this person documents what has run.

The DDLs are based on the relational model and one of its physical objects. If you do not have any physical models open, only the relational model is used, and the DDLs will be basic without physical parameters. You might want to use this, for instance, creating objects for your test database where you have defined the defaults for tablespaces and users and creating an object does not need physical parameters of its own.

# Setting Preferences and Properties

Certain preferences affect how the generation of DDLs will be performed and how the generated DDLs will look. In every new version of Data Modeler there are new preferences to make the generation more tunable. The DDL preferences should be studied carefully setting them correctly will get you the kind of DDLs you want from the tool without any manual work.

Figure 7-1 shows the Preferences dialog open to the Data Modeler | DDL tab. With Statement Termination Character for DB2 And UDB, you can define the termination character for DDL clauses for IBM DB2 and UDB databases. You type the character you wanted as a terminator in the box.

On this tab are several parameters for defining the trigger generation.

+   - The Create Type Substitution Triggers For Oracle And UDB setting whether type substitution triggers are generated in Oracle and IBM UDB.

+   - Create Arc Constraints defines whether the triggers for foreign key arc constraints are generated in the DDL scripts.