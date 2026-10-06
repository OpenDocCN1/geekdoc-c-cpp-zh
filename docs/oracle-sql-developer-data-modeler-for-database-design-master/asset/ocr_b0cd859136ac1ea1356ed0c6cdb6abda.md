# 246 Oracle SQL Data Modeler for Database Design

![](bbox=[0.118, 0.125, 0.831, 0.335])

**FIGURE 10-9.** Preferences for a Hive connector

Cloudera JDBC drivers from www.clouden.com/content/clouden/en/downloads.html. The Cloudera JDBC drivers for Hive are delivered in .zip files: Cloudera_HiveJDBC3_<version>.zip and Cloudera_HiveJDBC4_<version>.zip. These files compile with the JDBC 3.0 and 4.0 standards. Extract the files in Cloudera_HiveJDBC3_<version>.zip. SQL Developer and Data Modeler are using the JDBC 4.0 standard because the Java Runtime Environment (JRE) is 6.0 or newer. Start Data Modeler or SQL Developer. Choose Tools | Preferences and select Data Modeler | Third Party JDBC Drivers and add the drivers to the list. Click the green plus and find the files extracted from Cloudera_HiveJDBC4_<version>.zip, as shown in Figure 10-9.

Close Data Modeler or SQL Developer and restart it. Choose File | Import | Data Dictionary and click Add in the Data Dictionary Import Wizard to create a new connection.

For Data Modeler, the Hive connection is a JDBC connection, so just select the JDBC tab and define the JDBC URL and Driver Class settings for the connection. When you download the drivers, you will also get a PDF file that explains what to insert here. For SQL Developer, in the New / Select Database Connection dialog, as you can see in Figure 10-10, there is a new tabbed Hive for creating connections to Hive. Insert the connection details and click Test to make sure the connection works. Then click Save to save the connection settings. Now you can import (reverse engineer) from Hive to Oracle using this connection.