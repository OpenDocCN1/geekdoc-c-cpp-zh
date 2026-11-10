
### 9.4.3 Using the MESSAGE Addition to Raise an Exception

SAP NetWeaver 7.5 introduced a new addition, `MESSAGE`, which can be used when raising exceptions. Using the `MESSAGE` addition, you can pass the message specifications, such as the message type, message ID, and message number, as well as the placeholders for the message.

If the message class implements the `IF_T100_DYN_MSG` interface, you can pass the message type using the `TYPE` addition, and the placeholders for the message can be passed using the `WITH` addition (see Listing 9.9). However, if the message class implements the `IF_T100_MESSAGE` interface, then you can’t pass the message type and the message placeholders using the `WITH` addition.

Listing 9.9 shows example code to raise an exception when the `IF_T100_DYN_MSG` interface is implemented in the message class. In this example, we’re using the `MESSAGE` addition to pass the message specifications. The attributes and the message type can be passed directly without having to define them separately in the exception class, because the `IF_T100_DYN_MSG` interface provides built-in support.

```
RAISE EXCEPTION TYPE zcx_no_material
  MESSAGE ID sy-msgid
         TYPE sy-msgty
       NUMBER sy-msgno
        WITH sy-msgv1 sy-msgv2 sy-msgv3 sy-msgv4.
```

**Listing 9.9** Raising Exception with IF_T100_DYN_MSG Interface Implemented

### 9.5 Summary

In this chapter, you learned how errors can be handled in your programs to exit applications gracefully. We also looked at both procedural exceptions and class-based (object-oriented) exceptions. In the final section of this chapter, we discussed the use of messages in exception classes and explained how to use both the OTR and messages from message classes. We also identified some new concepts introduced in SAP NetWeaver 7.5.

At this point, you should be comfortable raising exceptions from your procedures and catching exceptions in your programs that are raised by other procedures.

In the next chapter, we'll discuss ABAP Data Dictionary in greater detail and go over how to create various dictionary objects.

## 10 ABAP Data Dictionary

ABAP Data Dictionary has been discussed in previous chapters on an as-needed basis. This chapter reviews the concepts already mentioned and offers a complete discussion of those topics that haven't yet been covered.

ABAP Data Dictionary is the central store used to create and manage data definitions (metadata). Maintaining data definitions centrally in ABAP Data Dictionary helps avoid redundancies. In addition, because ABAP Data Dictionary is a central repository, any modifications made to its data definitions will be reflected in programs automatically. In other words, ABAP Data Dictionary ensures data integrity, data consistency, and data security.

Using ABAP Data Dictionary, we can maintain a variety of objects, such as tables, views, data types, domains, type groups, search helps, and lock objects. Figure 10.1 shows the initial ABAP Data Dictionary screen (Transaction SE11). Using ABAP Data Dictionary objects, we can add additional functionality to screen fields automatically, such as input help (F1 help) and search help (F4 help).

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_394_0.png)

**Figure 10.1** ABAP Data Dictionary: Initial Screen

ABAP Data Dictionary is completely integrated with ABAP Workbench, so definitions maintained in ABAP Data Dictionary can be used seamlessly in all ABAP Workbench tools. As for all repository objects, to allow for continuous changes to ABAP Data Dictionary objects during the development phase, such objects are stored in active and inactive versions. Any changes that are made are saved as an inactive version, allowing all the related objects to be activated together and transported. The runtime system uses only the active version of the object and ignores the inactive version, allowing us to change objects without affecting dependent applications.

We've discussed some of the ABAP Data Dictionary objects in bits and pieces so far in this book on an as-needed basis. In this chapter, we'll discuss all of the ABAP Data Dictionary objects in greater detail, including the database tables, views, data types, type groups, domains, search helps, and lock objects. This chapter will also serve as a step-by-step guide to create all of these dictionary objects.

In [Section 10.1](#), we'll discuss database tables, including how to create them and how to use primary and secondary indexes. We'll also touch on using the table maintenance generator, foreign keys, and include and append structures. Then, in [Section 10.2](#), we'll discuss creating, using, and maintaining database views, projection views, maintenance views, help views, and the new ABAP Core Data Services (CDS) views.

Next, in [Section 10.3](#), you'll learn how to create global data types, such as screen elements, structures, and table types. We'll then discuss how to use type groups to maintain global data type declarations in [Section 10.4](#), before shifting our attention to domains in [Section 10.5](#).

[Section 10.6](#) will examine elementary and collective search helps. Finally, in [Section 10.7](#), we'll provide information on using logical lock functionality in applications using lock objects. By the end of the chapter, you'll have a thorough understanding of the ABAP Data Dictionary objects and how to use them in your own projects.

### 10.1 Database Tables

*Database tables* are one of the most important objects in ABAP Data Dictionary. As you know, every SAP system consists of an underlying relational database or in-memory database, such as SAP HANA. However, we can define tables independently of databases in ABAP Data Dictionary. We don't work at the database level to define database tables; we always use ABAP Data Dictionary to maintain database table definitions.

Once the corresponding object (the table) is defined in ABAP Data Dictionary and activated, the system creates the database table physically in the underlying database with the same structure as the table definition defined in the ABAP Data Dictionary. The system automatically translates the definitions of the table in ABAP Data Dictionary to the definitions native to the underlying database. This allows us to not worry about the underlying database specifics; ABAP Data Dictionary acts as middleware between the database and the SAP system.

[Figure 10.2](#) shows the table definition of the transparent table `MAKT` maintained in ABAP Data Dictionary. [Figure 10.3](#) shows the corresponding database table created in the underlying database.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_396_0.png)

**Figure 10.2** Table Definition in ABAP Data Dictionary

A *transparent table* in ABAP Data Dictionary has a one-to-one projection of the underlying database table. In other words, when we define a transparent table in ABAP Data Dictionary, exactly one database table with identical names and fields is created in the underlying database.

In addition to transparent tables, we can define other categories of tables in ABAP Data Dictionary, such as cluster tables, pool tables, and global temporary tables. You'll learn more about these table categories in [Section 10.1.1](#).

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_397_0.png)

**Figure 10.3** Database Object Created in Underlying Database

A database table in ABAP Data Dictionary consists of the following components:

- **Table fields**: Each database table consists of fields. Table fields define the structure of the database table. Each database table field is fully defined by assigning a data type. The fields represent table columns, and the primary key of the table exists as a subset of table fields.
- **Foreign keys**: Foreign keys define the relationship between the current database table and other database tables in the database.
- **Technical settings**: Technical settings control the creation of the database table in the underlying database. We can maintain different settings, such as initial database table size, tablespace to create the database table, and so on.
- **Indexes**: The key fields of the database table form the primary index of the database table. Additional secondary indexes can be created to speed up data selection.

In this section, we’ll look at these database table components, as well as inputting data into a database table using a maintenance view. We’ll also discuss including structures in tables and using append structures to enhance standard SAP database tables.

But first, let’s walk through the steps for creating a database table in the ABAP Data Dictionary.

### 10.1.1 Creating a Database Table

The following is a step-by-step guide to create a database table in the ABAP Data Dictionary:

1. On the initial screen of the ABAP Data Dictionary (refer back to **Figure 10.1**), select the **DATABASE TABLE** radio button, enter the name of the database table you wish to create, and click the **CREATE** button. The name of the database table should be in the customer namespaces (starting with Y or Z).

2. The table will open in the **DICTIONARY: CHANGE TABLE** view. On this screen, provide a meaningful description for the table. By default, the system will create a transparent table. If you wish to create other types of tables, such as cluster, pool, or global temporary tables, use the menu path **EXTRAS • CHANGE/DISPLAY TABLE TYPE** to change the table category.

   The following table categories can be defined in ABAP Data Dictionary:

   - **Transparent table:** Each transparent table defined in ABAP Data Dictionary creates exactly one database table in the underlying database, with identical names and fields. All customer tables, including tables that store business data, should be defined as transparent tables.
