Chapter 1: Introducing Database Design and Oracle SQL Developer Modeler 5

When selecting the tool for database design, you'll want one that supports these features: ER notation, an automatic transformation process from the conceptual design to the logical design, the ability to work in a multiuser environment, version control, reporting capabilities, scripts for generating the database objects automatically (preferably adjustable), and strong documentation tools. It would be a bonus if the tool also has for the standardization of naming, processes, and design rules; the ability to alert scripts for changing the database to design; and the ability to compare designs to each other and to compare a design to a database.

# What Is Oracle SQL Developer Data Modeler?

Oracle SQL Developer Data Modeler (referred as Data Modeler in this book) is a free tool for designing and documenting databases and data architecture. It supports not only Oracle databases but also DB2 and Microsoft Server databases, and at a certain level, any standards-based database has a Java Database Connectivity (JDBC) connector. Data Modeler supports all the steps in database design and has easy forward and backward engineering. After you have designed the database and have a physical model for it, you can export the scripts to the database objects. Data Modeler also supports different kinds of databases and multidimensional models. Data Modeler helps you keep your databases documented and enables to be agile. The tool is available as a stand-alone product, but it is also integrated into Oracle SQL Developer, so you can decide which is the best for you to use the tool. Installing the tool is simple, and is provided by Oracle if you have a database support contract.

Data Modeler offers the following features for database designers:

+   - Database design tools A collection of metadata about database is called a design in Data Modeler. A design consists of the logical models, multidimensional models, relational models, relational models, data type models, processes, business information, and requests requests as as well as all the objects models need ( Every object (entity,, and so,) is a single Extensible Markup Language (XML) file in a hierarchy that the tool creates automatically. The design itself is saved with the extension .dmd, and the .dmd file contains pointers to individual XML files.

+   - Customization You can tweak Data Modeler to your liking. In Preferences, you can, for instance, define where to keep your working copy of designs.

+   - Version control Data Modeler is integrated into a version control tool called Subversion. This integration allows you to have multiple users