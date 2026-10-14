
![](img/c024ccf88e28c30c07dd410d4342288f_778_0.png)

## The starting code for a WCF service library

## Description

- By default, a new WCF service library includes two files named IService1.cs and Service1.cs. The IService1.cs file contains an interface named IService1, along with a class named CompositeType that defines a composite data type. The Service1.cs file contains a class named Service1 that implements the IService1 interface.
- To define the operations of a service, you code an interface that has the ServiceContract attribute. Then, you can code one or more methods that have the OperationContract attribute.
- To define the data that’s used by a service, you code a class that has the DataContract attribute. Then, you code one or more properties that have the DataMember attribute.
- To implement the operations of a service, you code a class that implements the interface for the service.
- To add a WCF service to the library, select the Project➜Add New Item command. Then, select the WCF Service item from the resulting dialog box, enter a name for the service, and click Add.

Figure 23-4　How to develop the code for a WCF service library

## The IProductService interface

```
using System.Runtime.Serialization;
using System.ServiceModel;

namespace HalloweenServiceLibrary
{
    [ServiceContract]
    public interface IProductService
    {
        [OperationContract]
        Product GetProduct(string productID);
    }

    [DataContract]
    public class Product
    {
        string name = "";
        string categoryID = "";
        decimal unitPrice = 0;

        [DataMember]
        public string Name
        {
            get { return name; }
            set { name = value; }
        }

        [DataMember]
        public string CategoryID
        {
            get { return categoryID; }
            set { categoryID = value; }
        }

        [DataMember]
        public decimal UnitPrice
        {
            get { return unitPrice; }
            set { unitPrice = value; }
        }
    }
}
```

## The ProductService class

```
namespace HalloweenServiceLibrary
{
    public class ProductService : IProductService
    {
        public Product GetProduct(string productID)
        {
            Product p = ProductDB.GetProduct(productID);
            return p;
        }
    }
}
```

## The ProductDB class

```
using System;
using System.ComponentModel;
using System.Data;
using System.Data.SqlClient;

namespace HalloweenServiceLibrary
{
    [DataObject]
    class ProductDB
    {
        [DataObjectMethod(DataObjectMethodType.Select)]
        public static Product GetProduct(string productID)
        {
            SqlConnection con = new SqlConnection(GetConnectionString());
            string sel = "SELECT * " +
                "FROM Products WHERE ProductID = '" + productID + "'";
            SqlCommand cmd = new SqlCommand(sel, con);
            con.Open();
            SqlDataReader rdr =
                cmd.ExecuteReader(CommandBehavior.CloseConnection);
            Product p = new Product();
            if (rdr.Read())
            {
                p.CategoryID = rdr["CategoryID"].ToString();
                p.Name = rdr["Name"].ToString();
                p.UnitPrice = Convert.ToDecimal(rdr["UnitPrice"]);
            }
            rdr.Close();
            return p;
        }

        private static string GetConnectionString()
        {
            return "Data Source=localhost\\sqlexpress;" +
                "Initial Catalog=Halloween;Integrated Security=True";
        }
    }
}
```

## The App.config file

```
<?xml version="1.0" encoding="utf-8" ?>
<configuration>

  <system.web>
    <compilation debug="true" />
  </system.web>

  <!-- When deploying the service library project,
  the content of the config file must be added to the host's app.config file.
  System.Configuration does not support config files for libraries. -->
  <system.serviceModel>

    <services>
      <service name="HalloweenServiceLibrary.ProductService">
        <endpoint address="" binding="wsHttpBinding" contract="HalloweenServiceLibrary.IProductService">
          <identity>
            <dns value="localhost" />
          </identity>
        </endpoint>

        <endpoint address="mex" binding="mexHttpBinding" contract="IMetadataExchange" />

        <host>
          <baseAddresses>
            <add baseAddress="http://localhost:8732/Design_Time_Addresses/ProductService/" />
          </baseAddresses>
        </host>
      </service>
    </services>

    <behaviors>
      <serviceBehaviors>
        <behavior>

          <!-- To avoid disclosing metadata information,
          set the value below to false and remove the metadata
          endpoint above before deployment -->
          <serviceMetadata httpGetEnabled="True"/>

          <!-- To receive exception details in faults for debugging purposes,
          set the value below to true. Set to false before deployment
          to avoid disclosing exception information -->
          <serviceDebug includeExceptionDetailInFaults="False" />

        </behavior>
      </serviceBehaviors>
    </behaviors>

  </system.serviceModel>
</configuration>
```

## How to test a WCF service

Figure 23-7 shows how to test a WCF service. To do that, you can press F5 or click the Start Debugging button in the Standard toolbar. When you do, Visual Studio displays a WCF Test Client window like the one shown in this figure. Then, you can test any operation in any service in the library by double-clicking on the operation, entering any required parameters, and clicking the Invoke button.

Although you can’t see it in this figure, the WCF Test Client accesses the service with this URL:

```
http://localhost:8732/Design_Time_Addresses/ProductService/mex
```

Here, the /mex at the end of the URL indicates that the metadata exchange endpoint is used to access the service. If you look back to the App.config file, you can see that this URL corresponds with the address for the mexHttpBinding endpoint.

When you test a WCF service, it’s automatically compiled into a dll file. This file contains debugging information by default so you can debug the service using the Visual Studio debugger. When you finish testing a service, you’ll typically want to remove this debugging information so the service is more efficient. To do that, you can create a release build of the library as described in this figure.

## The WCF Test Client window

![](img/c024ccf88e28c30c07dd410d4342288f_784_0.png)

## Description

- To test a WCF service, you can press F5 or click the Start Debugging button in the Standard toolbar. When you do, Visual Studio displays a WCF Test Client window for the service library.
- To test a service operation, double-click on the operation in the left pane of the window to display a tab for the operation in the right side of the window. Then, enter any required parameters for the operation in the Request section of the tab and click the Invoke button. When you do, the Response section will show the data that’s returned by the operation.
- When you test a service, a dll file that contains debugging information is created and stored in the bin\Debug directory subordinate to the project directory. Then, you can use the Visual Studio debugger to debug the service.
- When you’re done testing a service, you can create a release build for the service that doesn’t contain debugging information. To do that, you can select the Release option from the Solution Configurations drop-down list in the Standard toolbar. Then, you can build or run the project to create a dll file that’s stored in the bin\Release directory subordinate to the project directory.

## How to create a web site that hosts a WCF service library

After you create and test a WCF service library, you can create a web site that hosts that library. Then, you’ll be able to run that web site under IIS.

## How to start a host web site

Figure 23-8 shows you how to create a web site that will host a WCF service library. To do that, you select the WCF Service template from the New Web Site dialog box. Then, you can use that dialog box to create either a file-system web site or a web site that runs under IIS. Although a file-system web site is fine for the initial development and testing, you’ll want to create a web site that runs under IIS to do your final testing.

When you use the WCF Service template, it automatically creates the Service.svc and Web.config files that you need to host a service. Then, you’ll typically rename the Service.svc file so it’s the same as the name of the service. In addition, you may need to make some changes to both of these files so they work correctly with the service. You’ll learn more about that in the next figure.

Earlier in this chapter, I mentioned that you can’t create a WCF service library using Visual Web Developer 2010 Express. However, you can still create a WCF service. To do that, you use the IService.cs and Service.cs files that are added to the App_Code folder of a WCF service web site by default. (This folder, along with the App_Data folder that’s also added by default, has been deleted from the web site shown in this figure since it’s not needed.) You write the code for these files just as you would for any other WCF service.

Unfortunately, when you create a WCF service directly in a WCF service web site, you can’t test the service as shown earlier in this chapter. Instead, you have to test it from a client application that uses the service. In addition, you won’t be able to host the web service in any other environments, such as a Windows application or WAS. Because of that, the service is much less flexible.

## How to add a reference to a service library

If you create a WCF service in a service library, you need to add a reference to that library to the host web site. To do that, you use the Add Reference dialog box shown in figure 23-8. From this dialog box, you can use the Browse tab of the Add Reference dialog box to navigate to the dll file for the WCF service library. In this case, I navigated to the HalloweenServiceLibrary.dll file in the bin\Debug directory of the project directory so I could debug the service from a client that uses the service. When I added a reference to this file, the files shown in the Bin directory in this figure were added to the project.
