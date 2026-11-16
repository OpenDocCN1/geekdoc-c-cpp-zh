# Running SQL Traces

Whether you implement persistence scenarios using JPA, JDBC, or a combination of the two, the end result from a runtime perspective is that a series of SQL commands will be issued against the database instance(s) your Java applications are bound to. Sometimes, if you’re not careful, the performance of these SQL commands at runtime may not be what you expect. For example, a query that performs well in a development environment might end up running rather poorly in production if a size of the target table grows exponentially. In these circumstances, it’s important to be able to trace the performance of SQL commands so that you can identify performance bottlenecks.

Within the SAP HCP Cockpit, you can turn on a SQL trace via the logger configuration screens of the JAVA APPLICATION DASHBOARD, as described in Section 4.2.4 of Chapter 4. Here, the target logger is com.sap.core.persistence.sql.trace, as shown in Figure 6.26. By setting the LOG LEVEL to Debug or higher, you can immediately turn on the SQL trace for the selected Java application. Similarly, you can turn the SQL trace off by dialing the logging level back.

![](bbox=[0.145, 0.47, 0.765, 0.8])

Figure 6.26 Turning on the SQL Trace in the SAP HCP Cockpit

Once the SQL trace is turned on, the default trace log will be filled with detailed information about JDBC data source or connection allocation and statement