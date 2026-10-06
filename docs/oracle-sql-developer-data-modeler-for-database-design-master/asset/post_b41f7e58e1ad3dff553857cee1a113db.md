
# 234 Oracle SQL Data Modeler for Database Design

![](img/431f8ac8f273fa89a28377c500ed60d7_260_0.png)

FIGURE 9-11. Updated model with previously exported XLS (XLSX)

![](img/431f8ac8f273fa89a28377c500ed60d7_260_1.png)

FIGURE 9-12. The entity Customer and its comments property updated in Microsoft Excel

# Summary

You need to make a few decisions before starting to use Subversion, specifically, about privileges, the number of Subversion repositories, and the structure for Subversion directories. Also, it is valuable to use templates for comments that will be used when committing to Subversion to make finding the right revision easier.

Data Modeler offers integration with Subversion, which means that you can use Subversion in Data Modeler fluently. Subversion can be used to enable a multiuser environment. In fact, Subversion can be used to version the database designs the same way the application design is versioned. Every design must have a working copy directory where changes are saved and then committed to Subversion. Every committed change in Subversion creates a new revision. In Pending Changes, you can see both incoming and outgoing changes as well as new files that should be added to Subversion.

If there are conflicts, someone must resolve them; they cannot be resolved automatically. Conflicts are resolved by merging, committing, or reverting, depending on the desired outcome. Conflicts often can be avoided by saving and committing right after you have finished making a change.

You can let end users edit the designs in Microsoft Excel and then upload those changes to Data Modeler easily.

![](img/431f8ac8f273fa89a28377c500ed60d7_262_0.png)

![](img/431f8ac8f273fa89a28377c500ed60d7_263_0.png)

# CHAPTER 10

# Documenting an Existing Database

# 238 Oracle SQL Developer Data Modeler for Database Design Mastery

It is important to have documentation for your databases. If you do not understand your data, you cannot keep it up to date, secure, of good quality, and so on. In addition, changing the data structures based on current requirements is impossible if you do not understand what you are changing. Documentation is vital when addressing problems related to data, such as poor performance.

Surprisingly, often databases don't have any documentation. This could be because the database came with an application product and the vendor did not deliver any documentation for the database. In these cases, it might be possible not to have documentation for the database because all the changes, problem solving, and so on, are done by the vendor; still, it is good to know what you have bought. In some cases, you might have some documentation for a database that was created during the software development process, but it was not maintained, and now it would be too much work to bring it up to date. In other cases, the documentation was handwritten and cannot be used, for instance, generate data definition language (DDL) scripts. There are many reasons why there is no expensive documentation.

You could, of course, document an existing database manually from scratch, which can be expensive and a lot of work, but Data Modeler offers several other possibilities that are far more efficient and cost-effective. It allows you to document an existing database by reverse engineering the database from the data dictionary or from existing DDLs. Or you can use the documentation you might have on a third-party modeling tool and import that into Data Modeler. You can also combine these methods.

# Setting Preferences and Properties

Data Modeler has preferences that will change the result of reverse engineering or importing from a third-party modeling tool. Choose Tools | Preferences to open the Preferences dialog.

On the Data Modeler | DDL tab, you can define two preferences for the import: Replace System Names During Import and Create Domains During Import. If Replace System Names During Import is not selected, the constraint names are imported from the dictionary as they have been defined (SYS_). If it is selected, the name is changed during the import according to the name standards defined in the design properties. If Create Domains Import is selected, domains are created from data types during the import operations. If it is not selected, no domains are created.

On the Data Modeler | DDL | DDL/Storage tab, you will see the DDL Storage Options for Import And Export options. Here you can define which storage parameters are imported and which are not. And on the main Data tab, you can define the default directory for imported files (Default Directory). After Import, you will always see the log after every import operation.

On the Data Modeler | Model | Relational tab, the Default foreign Key Delete Rule prevents the delete when a new foreign key is created. If you create a design by importing a DDL script or scripts, then ensure the option is required before import.

You can also define in the Preferences dialog whether the OCI(8) driver is used, instead of the JDBC (thin) driver, by default for Oracle Database connections if it is available. You set this on the Data Modeler tab with the preference Use OCI/Thick Driver.

# Reverse Engineering an Existing Database

If you have a database that has no documentation in another modeling tool, there are two ways of documenting your database: You can reverse engineer from the data dictionary, or you can import the DDLs that were used for creating the database. If you want to start designing the database with Data Modeler, you can use the Engineer To Logical Model functionality to generate a logical model, export physical models as explained in Chapter 12.

# Reverse Engineering from a Data Dictionary

You can reverse engineer from Oracle, but you can also import from other supported database management systems (RDBMS). At the moment, the supported databases are Microsoft SQL Server 2000 to 2012, IBM DB2/LUw v7-v10, IBM DB2 for OS/390, DB2 Mainframe/OS up to DB12, and ODBC/JDBC-compliant data dictionaries. The non-Oracle drivers are not included in the Data Modeler installation. To be able to import non-Oracle databases, you need to download the drivers and add them in the Preferences dialog. Specifically, after downloading the drivers, you must open the Preferences dialog, select Data Modeler | Third Party Drivers, and add the drivers by clicking the plus sign. You will see the non-Oracle database as a new tab in the New / Select Connection dialog, and you can create a new connection.

For instance, if you added Microsoft SQL Server, you will see a new tab called Server beside Oracle and JDBC in the New / Select Connection dialog, as shown in Figure 10-1. Depending on the RDBMS selected and the version of Data Modeler, there might be some other that you must do to get the connection working, such as with Java settings, but in general the process is downloading the drivers, extracting them, and setting the Data Modeler preferences for third-party drivers.

![](img/431f8ac8f273fa89a28377c500ed60d7_266_0.png)

FIGURE 10-1. Connection to Microsoft SQL Server

# Reverse Engineering from an Oracle Database

To reverse engineer from an Oracle database, choose File | Import | Data Dictionary. Then select the connection wanted from the connection list in the Data Dictionary Import Wizard, as shown in Figure 10-2. Or click Add to create a new connection using the New / Select Connection dialog shown in Figure 10-3.

You can create an Oracle connection or a connection based on JDBC drivers. Since Data Modeler 4.0.3, you can make the connection using Secure Shell (SSH) tunnels, and the proxy connection was moved to the same place within the settings. To create an SSH tunnel, click the Advanced button in the New / Select Connection dialog to be taken to the Advanced Properties dialog. Select the SSH tab and fill in the information needed for an SSH connection:

- Use SSH to define an SSH tunnel to be used. 
- Type the SSH server for Host.
- Type the SSH port for Port. The default port is 22.
