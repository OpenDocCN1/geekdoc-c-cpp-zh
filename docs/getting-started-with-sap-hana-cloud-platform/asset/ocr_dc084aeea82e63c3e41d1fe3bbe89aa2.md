# Calling RFC Functions within a Java Application

Because the RFC protocol is proprietary to SAP, you can’t simply use a Java SE or Java EE API to invoke an RFC function. Instead, you must use a specialized connector library that SAP provides called the SAP Java Connector (JCo). In many respects, the JCo library is utilized in much the same way that you use the JDBC library to connect to database systems. Classes and interfaces are provided to create connections, build RFC function calls, parse through the results, and so on.

Within the context of SAP HCP, the JCo library is essentially built into the Connectivity Service. This means that you don’t have to worry about bundling the library within your web applications or making sure that the library is on the application classpath at runtime. It also means that you don’t have to worry about connection allocation like you would if you were using the standalone version of JCo. Here, instead of hard-coding the connection parameters or externalizing them in a jco.properties file, you can use the RFC destination object created in the SAP HCP Cockpit (or elsewhere) as the starting point for creating a connection object.

The version of the JCo library installed on SAP HCP is stripped down from the standalone version. If you’re familiar with JCo programming concepts, some notable items that are missing in the SAP HCP version of JCo include support for server-side programming, IDoc consumption, and dynamic connection configuration and allocation.

The code excerpt contained in Listing 6.17 illustrates the connection allocation process. Here, you use the getDestination() method of the com.sap.conn.jco.JCoDestinationManager class to fetch the JCo destination that matches up with the specified destination name. As you can see, the destination name you’re using matches up with the one that you created within the SAP HCP Cockpit in the previous section. At runtime, the Connectivity Service will use this destination name as a key to fetch the configured destination properties and allocate a com.sap.conn.jco.JCoDestination object that represents the JCo connection to the back-end. From here on out, it’s JCo programming as per usual.

```
@import com.sap.conn.jco.*;
@Stateless
@LocalBean
public class RfcProxyBean
{
```