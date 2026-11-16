annotation. Both techniques are demonstrated in the code excerpt contained in Listing 6.14.

```
public class DataSourceTest extends HttpServlet {
private DataSource mainDataSource;

@Resource(name="jdbc/AltDS"):
private DataSource altDataSource;

private void initMainDataSource()
{
try
{
javax.naming.InitialContext ctx =
new javax.naming.InitialContext();

mainDataSource = (DataSource)
ctx.lookup("java:comp/env/jdbc/MainDS");
}
catch (Exception ex)
{
}
}
...
```

# Listing 6.14 Working with Multiple Data Sources in a Java Web Application

# Advantages of Using JDBC vs. JPA

When compared to the ease of use afforded by the JPA, there's really no getting around the fact that JDBC-based persistence scenarios are tedious to implement. Having said that, though, there are many reasons that it might make sense to utilize a JDBC approach to persistence. Some of these reasons include the following:

+   Minimized resource utilization

In many situations, the JPA pulls back more information from the database than you might need. For example, in the simple query scenario demonstrated in this section, we only pulled back selected columns from the Incident and Involved-Person entities. This use of SQL projection reduced the memory footprint of the query results considerably. When you imagine a productive system with thousands of records, you can see that this reduction in memory footprint can have significant impacts on application performance. Suffice to say that there are times when you really want to exert control over what gets queried and when.