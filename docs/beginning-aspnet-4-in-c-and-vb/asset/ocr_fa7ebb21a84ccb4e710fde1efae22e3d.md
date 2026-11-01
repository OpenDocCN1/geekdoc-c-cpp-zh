+   - A string that represents the location of the SQL Server Express database file or the name of the SQL Server that is used
+   - A connection string
+   - Another DataContext object

The first two string options also have the option of including your own database mapping file. After you have instantiated this object, you are then able to programmatically use it for many types of operations.

# Using the ExecuteQuery Method

One of the simpler things that you can accomplish with the DataContext object is to run quick commands that you write yourself using the ExecuteQuery<T>() method. For instance, if you are going to pull all the products from the Products table using the ExecuteQuery<T>() method, your code would be similar to the following:

```
```csharp
using System;
using System.Collections.Generic;
using System.Data.Linq;

namespace ConsoleApplication1
{
    class Class1
    {
        static void Main(string[] args)
        {
            DataContext dc = new DataContext(@"Data Source=.\SQLEXPRESS;
                AttachDbFilename=|DataDirectory|\NORTHWND.MDF;
                Integrated Security=True;User Instance=True");

            IEnumerable<Product> myProducts =
                dc.ExecuteQuery<Product>("SELECT * FROM PRODUCTS", "");

            foreach (Product item in myProducts)
            {
                Console.WriteLine(item.ProductID + " | " + item.ProductName);
            }

            Console.ReadLine();
        }
    }
}
```
```

code download ConsoleApplication1.sln

In this case, the ExecuteQuery<T>() method is called passing in a query string and returning a collection of Product objects. The query utilized in the method call is a simple Select statement that doesn't require any additional parameters to be passed in. Because there are no parameters passed in with the query, you can either use the double quotes as the second required parameter to the method call or not even provide that parameter. If you optionally substitute any values in the query, you construct your ExecuteQuery<T>() call as such:

```
```csharp
IEnumerable<Product> myProducts =
    dc.ExecuteQuery<Product>("SELECT * FROM PRODUCTS WHERE UnitsInStock > {0}",
    50);
```
```

In this case, the {0} is a placeholder for the substituted parameter value that you are going to pass in, and the second parameter of the ExecuteQuery<T>() method is the parameter that will be used in the substitution.