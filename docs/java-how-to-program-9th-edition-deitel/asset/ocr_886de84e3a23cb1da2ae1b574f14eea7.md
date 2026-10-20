The next several sections explain how to build the AddressBook application. First, we set up the database (Section 30.2.1). Next, we present class AddressBean (Section 30.2.2), which enables the app’s Facelets pages to interact with the database. Finally, we present the index.xhtml (Section 30.2.3) and addentry.xhtml (Section 30.2.4) Facelets pages.

# 30.2.1 Setting Up the Database

You’ll now create a data source that enables the app to interact with the database. As part of this process, you’ll create the addressbook database and populate it with sample data.

# Open NetBeans and Ensure that Java DB and GlassFish Are Running

Before you can create the data source in NetBeans, the IDE must be open and the Java DB and GlassFish servers must be running. Perform the following steps:

+   1. Open the NetBeans IDE.
+   2. On the Services tab, expand the Databases node then right click Java DB. If Java DB is not already running the Start Server option will be enabled. In this case, Select Start server to launch the Java DB server.
+   3. On the Services tab, expand the Servers node then right click GlassFish Server 3. If GlassFish Server 3 is not already running the Start option will be enabled. In this case, Start server to launch GlassFish.

You may need to wait a few moments for the servers to begin executing.

# Creating a Connection Pool

In web apps that receive many requests, it’s inefficient to create separate database connections for each request. Instead, you should set up a connection pool to allow the server to manage a limited number of database connections and share them among requests. To create a connection pool for this app, perform the following steps:

+   1. On the Services tab, expand the Servers node, right click GlassFish Server 3 and select View Admin Console. This opens your default web browser and displays a web page for configuring the GlassFish server.
+   2. In the left column of the page under Common Tasks, expand the Resources node, then expand its JDBC node to show the JDBC Resources and Connection Pools nodes (Fig. 30.2).

![](bbox=[0.38, 0.7, 0.6, 0.86])

Fig. 30.2 | Common Tasks window in the GlassFish server configuration web page.