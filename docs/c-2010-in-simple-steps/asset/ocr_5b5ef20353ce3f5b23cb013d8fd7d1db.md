# Listing 10.10: Using the Sum() Method in the AggregateOperatorExample Application

```
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace AggregateOperatorExample
{
    class Program
    {
        public static void Main(string[] args)
        {
            int[] numArray = { 1,2,3,4,5,6,7,8,9 };
            int numSum = numArray.Sum();
            Console.WriteLine("The sum of the numbers is {0}.", numSum);
            Console.ReadLine();
        }
    }
}
```
```

In Listing 10.10, the Sum() method is used to calculate the sum of numbers.

5 Press the F5 key to run the application. The output appears, as shown in Fig.C#-10.11:

![](bbox=[0.3, 0.49, 0.6, 0.6])

Fig.C#-10.11

Fig.C#-10.11 shows the sum of the numbers given in Listing 10.10 by using the Sum() method.

Now that you are familiar with the standard query operators available in LINQ, let's discuss programming with LINQ to ADO.NET in the next section.

# Explaining LINQ to ADO.NET

LINQ to ADO.NET is a term that describes the database-centric aspects of LINQ. LINQ to ADO.NET consists of two separate technologies, LINQ to DataSet and LINQ to SQL.

LINQ to DataSet is a set of extensions to the standard ADO.NET DataSet programming model that allows DataSet, DataTable, and DataRow objects to be a natural target for a LINQ query expression. LINQ to DataSet provides optimized querying capability over datasets.

LINQ to SQL allows you to interact with a relational database by removing the ADO.NET data types through the use of entity classes. LINQ to SQL enables you to directly query SQL Server database schemas.

Now, let's discuss the LINQ to DataSet, and LINQ to SQL technologies in detail in the following sections.

# Programming with LINQ to SQL

LINQ to SQL is a component that was introduced with .NET Framework 3.5. It is specifically designed to work with an SQL Server database. LINQ to SQL allows you to write queries to retrieve and manipulate data from SQL Server.