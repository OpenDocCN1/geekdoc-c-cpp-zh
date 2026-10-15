```
<system.serviceModel>
    <behaviors>
        <serviceBehaviors>
            <behavior name="">
                <serviceMetadata httpGetEnabled="true" />
                <serviceDebug includeExceptionDetailInFaults="false" />
            </behavior>
        </serviceBehaviors>
    </behaviors>
    <bindings>
        <customBinding>
            <binding name="ProVB_SLservices.Web.Service1.customBinding0">
                <binaryMessageEncoding />
                <httpTransport />
            </binding>
        </customBinding>
    </bindings>
    <serviceHostingEnvironment aspNetCompatibilityEnabled="true" />
    <services>
        <service name="ProVB_SLservices.Web.Service1">
            <endpoint address="" binding="customBinding" bindingConfiguration="ProVB_SLservices.Web.Service1.customBinding0" contract="ProVB_SLservices.Web.Service1" />
            <endpoint address="mex" binding="mexHttpBinding" contract="IMetadataExchange" />
        </service>
    </services>
</system.serviceModel>
</configuration>
```

Code snippet from web.config

This not only converts your message to binary, but gives you a significant boost to performance, as the binary objects are also compressed. This method also results in a slight security improvement because the objects are not sent across in plain text, where a network monitoring tool could see the data. It is not, however, secure enough to rely on this as your only method of security — you would still want to rely on SSL and other levels of security for highly secured applications.

While both WCF and ASMX Web services provide a great way to access your data, you still have to define all your function calls between the server and the client. For smaller applications this is not an issue, but imagine applications for which you may have 300 or more database tables that you need to send data back and forth. These types of situations lead us into the next type of service.

# ADO.NET Data Service

Now that you have seen the two most classic examples of Web services, this section looks at one of the latest Microsoft technologies for getting to your data. Microsoft has created ADO.NET Data Services to provide a REST-based Web service to expose LINQ to SQL, Entity Framework, or other ORM technology classes. REST (Representational state transfer) uses traditional Web-based standards to expose data for create, read, update, and delete (CRUD) operations. To do this with WCF, you would have to build your own CRUD operations for every table in your database, which for a large application can be impractical to implement.

To get started with ADO.NET Data Services, we’ll set up a few things in our project that we will use throughout the rest of the chapter. Rather than use the traditional Northwind database, we are going to build our own. We are going to create a basic “issue management system” where we keep track of customers and their issues. To begin, first add a SQL Server Database to the ASP.NET project as shown in Figure 20-4.