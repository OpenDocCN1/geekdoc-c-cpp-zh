+   - To connect to the database from a web app, you configure a data source name (p. 1281) that will be used to locate the database. The data source name is associated with a connection pool that manages the connections to the database.
+   - JNDI (Java Naming and Directory Interface) is a technology for locating application components (such as databases) in a distributed application (such as a multitier web application).

# Section 30.2.2 @ManagedBean Class AddressBean

+   - A DataSource (p. 1285; package javax.sql) enables a web application to obtain a Connection to a database.
+   - The annotation @Resource (p. 1285) can be used to inject a DataSource object into a managed bean. The annotation’s name attribute specifies the JNDI name of a data source.
+   - The @Resource annotation enables the server to hide all the complex details of locating a connection pool. The server creates a DataSource for you that’s configured to use a connection pool and assigns the DataSource object to the annotated variable. You can then trivially obtain a Connection for interacting with the database.
+   - Database connections are limited resources, so you should use and close them quickly in your web apps. You can use a CachedRowSet to store the results of a query for use later.

# Section 30.2.3 index.xhtml Facelets Page

+   - You can use an h:dataTable element (p. 1286) to display a collection of objects, such as the rows in a CachedRowSet, in tabular format.
+   - If you specify an h:commandButton’s action attribute (p. 1286) with a value that is the name of a web page (without the file name extension), the JSF framework assumes this is a page in the app, appends .xhtml extension to the action attribute’s value and returns the page to the client browser.
+   - The h:dataTable element’s value attribute (p. 1287) specifies the collection of data you wish to display. The h:dataTable iterates over its value collection and, one at a time, assigns each element to the variable specified by the var attribute (p. 1288). This variable is used in the h:dataTable’s nested elements to access each element of the collection.
+   - The h:dataTable rowClasses attribute (p. 1288) is a space-separated list of CSS style class names that are used to style the rows in the tabular output. You can specify as many styles as you like—they’ll be applied in the order you list them one row at a time until all the styles have been applied, then the h:dataTable will automatically cycle through the styles again for the next set of rows. The columnClasses attribute works similarly for columns in the table.
+   - The headerClass attribute (p. 1288) specifies the column header CSS style. The footerClass attribute (p. 1288) works similarly for column footers in the table.
+   - The styleClass attribute (p. 1288) specifies the CSS styles for the entire table. The cellPadding and cellSpacing attributes (p. 1288) specify the number of pixels around each table cell’s contents and the number of pixels between table cells, respectively.
+   - An h:column element (p. 1288) defines a column in an h:dataTable.
+   - To display a column header above a column, define an f:facet element (p. 1288) and set its name attribute to "header". Similarly, to display a column footer, use an f:facet with its name attribute set to "footer".

# Section 30.2.4 addentry.xhtml Facelets Page

+   - You can call a managed bean’s methods in EL expressions.
+   - When you call a managed bean method with the action attribute, if the method returns a value, that value is used to request the corresponding page from the app. If the method does not return a value, the current page is re-requested.