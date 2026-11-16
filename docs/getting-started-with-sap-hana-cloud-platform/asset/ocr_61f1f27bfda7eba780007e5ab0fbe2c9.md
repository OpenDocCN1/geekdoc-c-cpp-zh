```
</servlet-mapping>
...
<web-app>
```

# Listing 6.11 Exposing an OData Service Using Apache Olingo

To test the finished product, open the sample application, and click on the Test ODATA SERVICE link shown in Figure 6.14. This will open the OData service document. From here, you can test the service from within your web browser or via any number of freeware OData client and test tools available online.

![](bbox=[0.172, 0.3, 0.925, 0.45])

Figure 6.14 Testing the Incident OData Service

# Limitations of the Apache Olingo Type System

As of the time of writing, the Apache Olingo project is working on providing support for the OData 4.0 standard. During this transition period, we should point out that there are certain limitations with the Olingo type system that you should be aware of. In general, the current version of the library does not support all of the various data types that you can use to define entity attributes in the JPA. This is particularly the case with primitive types or temporal types, such as the java.sql.Date or java.sql.Time types.

# 6.2.4 Working with Java Database Connectivity

Despite its ease of use, the JPA approach to persistence does have a certain amount of overhead associated with it from a technical point of view. For application scenarios focused on processing a handful of objects at a time, this tiny amount of bloat may go unnoticed. On the other hand, if you’re building reporting or analytics applications, even the tiniest bit of overhead can have significant impacts on application performance.

For these reasons, and others, SAP allows you to take more direct control over the data access process using the familiar Java Database Connectivity (JDBC) API. In