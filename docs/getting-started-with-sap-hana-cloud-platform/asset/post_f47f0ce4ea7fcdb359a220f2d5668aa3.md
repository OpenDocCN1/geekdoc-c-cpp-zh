
initializeODataJPAContext() method that Olingo uses to link with the target JPA persistence unit. You can see how we implemented this class in the sample application by looking at the ODataServiceFactory class of the com.sap.press.hcbook.chp06.persistence package. Here, the only real trick was to figure out how to supply the ODataJPAContext instance with a jaxrs-persistence.EntityManagerFactory instance. Because the sample application uses CMP, we had to introduce a JPAUtilities class to store an EntityManagerFactory loaded from a faceless Servlet called BootstrapServlet that gets loaded at startup.

- 3. Once you define the OData service factory, you have everything you need to set up the service. For this final task, simply open up the web.xml file and configure a Servlet class that was included in the libraries that were copied over in step 1: org.apache.cxf.jaxrs.servlet.CXFNonSpringJaxrsServlet. Listing 6.11 contains an excerpt of the web.xml file contained within the sample application. With minimal configuration, Olingo has everything it needs to bootstrap the service.

```xml
<web-app>
...
<servlet>
    <servlet-name>IncidentODataProviderServlet</servlet-name>
    <servlet-class>
        org.apache.cxf.jaxrs.servlet.CXFNonSpringJaxrsServlet
    </servlet-class>
    <init-param>
        <param-name>
            javax.ws.rs.Application
        </param-name>
        <param-value>
            com.sap.press.hcbook.chp06.persistence.rest.app.ODataApplication
        </param-value>
    </init-param>
    <init-param>
        <param-name>
            org.apache.olingo.odata2.service.factory
        </param-name>
        <param-value>
            com.sap.press.hcbook.chp06.persistence.ODataServiceFactory
        </param-value>
    </init-param>
    <load-on-startup>2</load-on-startup>
</servlet>
...
<servlet-mapping>
    <servlet-name>IncidentODataProviderServlet</servlet-name>
    <url-pattern>/IncidentProcessing.svc/*</url-pattern>
</servlet-mapping>
...
</web-app>
```

### Listing 6.11 Exposing an OData Service Using Apache Olingo

To test the finished product, open the sample application, and click on the Test ODATA SERVICE link shown in Figure 6.14. This will open the OData service document. From here, you can test the service from within your web browser or via any number of freeware OData client and test tools available online.

![](img/cf7012644082c115a2181376d9b7486d_242_0.png)

Figure 6.14 Testing the Incident OData Service

## Limitations of the Apache Olingo Type System

As of the time of writing, the Apache Olingo project is working on providing support for the OData 4.0 standard. During this transition period, we should point out that there are certain limitations with the Olingo type system that you should be aware of. In general, the current version of the library does not support all of the various data types that you can use to define entity attributes in the JPA. This is particularly the case with primitive types or temporal types, such as the java.sql.Date or java.sql.Time types.

## 6.2.4 Working with Java Database Connectivity

Despite its ease of use, the JPA approach to persistence does have a certain amount of overhead associated with it from a technical point of view. For application scenarios focused on processing a handful of objects at a time, this tiny amount of bloat may go unnoticed. On the other hand, if you’re building reporting or analytics applications, even the tiniest bit of overhead can have significant impacts on application performance.

For these reasons, and others, SAP allows you to take more direct control over the data access process using the familiar Java Database Connectivity (JDBC) API. In this section, we'll learn how to incorporate JDBC-based persistence scenarios into Java web applications.

### Getting Started with JDBC

If you haven't worked with JDBC before, then a brief introduction is in order. Logistically, the core classes and interfaces that make up the JDBC API are contained within the java.sql and javax.sql packages of the Java SE library. As you browse through these packages, you'll notice that roughly 90% of the API is defined using interfaces. This design choice was made in order to separate the core JDBC interface from implementation details specific to various database vendors (e.g., Oracle vs. Microsoft SQL Server). The lower-level implementation details are provided in the form of a vendor-specific JDBC driver library packaged as one or more JAR files.

Within a managed environment such as SAP HCP, database connections are abstracted in the form of a javax.sql.DataSource object, which is normally allocated using injection techniques within a Servlet or EJB component. From here, you can obtain a database connection, prepare a statement, and execute your queries or updates in procedural fashion.

The alternative here would be to manually lookup the data source within the Java EE container's JNDI context using the data source name provided as part of the schema binding definition, as described in Section 6.2.2.

To demonstrate how this works, let's look at how we implemented a slightly more advanced query from within our incident management application. Here, within our IncidentBean EJB façade, we defined a business method called getIncidentsByInvolvedPerson(). This method uses the JDBC API to build a dynamic query that incorporates fuzzy search logic to make it easier to search for incidents by involved persons. An excerpt of this method is contained within Listing 6.12.

```java
@Stateless
@LocalBean
public class IncidentBean {

@Resource(mappedName="java:comp/env/jdbc/DefaultDB")
private javax.sql.DataSource dataSource;

...

public List<Incident> getIncidentsByInvolvedPerson(
String firstName, String lastName)
throws java.sql.SQLException
{
java.sql.Connection conn = null;
List<Incident> incidents = new ArrayList<Incident>();
try
{
// Build the dynamic SQL query to fetch the incidents:
StringBuffer query = new StringBuffer();
String fname = (firstName == null) ? "" :
firstName.replaceAll("\\*", "%");
String lname = (lastName == null) ? "" :
lastName.replaceAll("\\*", "%");
...
query.append(
"SELECT i.id, i.title, i.reportedon, i.reportedat " +
"FROM Incident AS i INNER JOIN involvedperson AS p ");
query.append("ON i.id = p.incident_id");
...
// Create a database connection:
conn = dataSource.getConnection();
// Create a statement object to encapsulate the query:
PreparedStatement ps =
conn.prepareStatement(query.toString());
if (! fname.equals(""))
{
ps.setString(1, fname);
if (! lname.equals(""))
ps.setString(2, lname);
}
else
{
if (! lname.equals(""))
ps.setString(1, lname);
}
// Execute the query:
ResultSet rs = ps.executeQuery();
// Copy the results into DTOs to be transferred to
// the frontend:
while (rs.next()) {
Incident incident = new Incident();
incident.setId(rs.getString(1));
incident.setTitle(rs.getString(2));
incident.setReportedOn(rs.getDate(3));
incidents.add(incident);
}
}
finally
{
// Always remember to release the connection to
// conserve resources!!!
if (conn != null) {
try { conn.close(); } catch (SQLException se) {}
}
}
return incidents;
}
...
```

### Listing 6.12 Consuming the Persistence Service Using the JDBC API

As you can see in Listing 6.12, the JDBC approach to database access is highly procedural:

- 1. Use the getConnection() method of the injected javax.sql.DataSource to create or obtain a database connection. In a managed environment like SAP HCP, connections are pooled in such a way that the performance overhead with this step is minimized.

- 2. Create an instance of the java.sql.Statement interface, which is the rough JDBC equivalent of a database command-line prompt. In the code excerpt contained in Listing 6.12, we used the java.sql.PreparedStatement subinterface, because it provides for optimizations such as statement caching and precompilation. As the basis for our Statement, we provided a dynamically generated SQL SELECT statement.

- 3. To process the query, we used the executeQuery() method of the java.sql.Statement interface. If you look at the JavaDoc for this interface, you can find a number of other execute() methods that can be used to process DML statements and so on.

- 4. The result of the query is returned in the form of a java.sql.ResultSet object. This object provides a cursor that can be used to scroll through the data. Here, you can access selected columns using the plethora of getter methods included within the interface definition.

- 5. Once you're done with your queries, it's important to close out the connection using the close() method of the java.sql.Connection handle. Note that within a managed environment like SAP HCP, this method name is a bit of a
