
the usual Edit, Delete, and Show All Items links used by the Details page template. Listing 9.4 shows the code-behind.

## LISTING 9.4 Custom Order Page with Fulfill Button (Code-Behind)

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web.DynamicData;
using DataModel;

namespace WebApplication.Samples.Ch9.ContextMethod
{
    public partial class SamplePage : System.Web.UI.Page
    {
        protected MetaTable ordersTable;

        protected void Page_Init(object sender, EventArgs e)
        {
            this.ordersTable = MetaModel.Default.GetTable(typeof(Order));
            this.formView.SetMetaTable(this.ordersTable);
            this.dataSource.Include = this.ordersTable.ForeignKeyColumnsNames;
        }

        protected void FulfillButton_Click(object sender, EventArgs args)
        {
            using (var context = new NorthwindEntities())
            {
                int orderId = (int)this.formView.DataKey.Value;
                context.FulfillOrder(orderId);
                context.SaveChanges();
                this.Response.Redirect(
                    this.ordersTable.GetActionPath(PageAction.Details,
                    new List<object>(new object[] { orderId })));
            }
        }
    }
}
```

The FulfillButton_Click method handles the Click event of the Fulfill button. Because the event handler is invoked during a postback, the original Order entity instance displayed by the page is no longer available. In this example, OrderID is extracted from the DataKey property of the FormView control. Alternatively, if this were a custom page template and the OrderID was available in the URL, you could have obtained it by calling the GetColumnValuesFromRoute method of the MetaTable object discussed in Chapter 7.

The new version of the FulfillButton_Click event handler wraps a try/catch block around the FulfillOrder and SaveChanges method calls, which could throw validation exceptions. The catch block intercepts all exceptions and passes them to the HandleException method of the UnleashedValidator (defined at the top of the page in Listing 9.3). If the HandleException method returns false, the code rethrows the exception.

As discussed in Chapter 8, the UnleashedValidator class inherits from the built-in DynamicValidator and extends error handling to support AggregateException. The HandleException method receives an Exception object as a parameter, iterates over all UnleashedValidator controls on the page, including those in field templates, and attempts to handle the exception by passing it to each validator's ValidateException method. The HandleException returns true if one or more validators on the page were able to handle the exception by setting their ValidationException properties. For complete details, please refer to the UnleashedValidator source code in the Unleashed.DynamicData project accompanying the book.

Figure 9.8 shows an example of an error message displayed because of the ValidationException thrown in the FulfillOrder business rule method.

![](img/11b373b78859e17d318fd76939a0df9d_315_0.png)

FIGURE 9.8 Validation error from calling a business rule method.

**NOTE**

The read-only field templates do not include validators by default. With less than ten read-only field templates included in a Dynamic Data project out of the box, you can add the UnleashedValidator controls to the field templates and improve display of property-specific errors. However, if you choose to do it, make sure the validators are hidden when there are no errors; otherwise, the increase in the size of generated HTML and JavaScript could have a significant impact on performance of all read-only pages in the application.

## Business Rules in the Database

Some of the business logic discussed in this chapter is similar to what you can do with database stored procedures, triggers, and check constraints. It is indeed possible to implement robust business rules directly at the database level; however, doing so has an immediate impact on performance and scalability of the overall system, which are especially important for high-volume web applications.

A system scales up when its performance can be increased by installing faster or additional CPUs and RAM on a single physical computer. On the other hand, a system scales out when its performance can be increased by adding more computers. Scaling up is expensive; the cost of both hardware and software grows exponentially as the number of CPUs and amount of RAM increases beyond typical commodity levels. In practice, this means that performance you can get out of a database server has a practical limit, sometimes called a glass ceiling, which would require unreasonably high costs to break through. Scaling out is much cheaper, as the cost of adding commodity servers to the system grows only linearly. Unfortunately, most relational database management systems that exist today scale up much better than they scale out; in fact, scaling out a database server is nearly impossible without redesigning the system itself.

In general, scalability of an information system can be improved by performing CPU-bound tasks on the application servers (such as a web server in our example) and I/O-bound tasks on the database server. Most of the business rules discussed so far are CPU-bound, or in other words, they only need CPU cycles to execute and do not need to access the database. Therefore, implementing them in the entity classes of the application allows you to scale out the system by adding application servers and leaving the precious resources of the database server available for compiling queries and calculating execution plans.

However, some types of business logic, such as validation of uniqueness or referential integrity, are I/O-bound. They require access to data and can be implemented more efficiently on the database server. Suppose that all products in the Northwind database must have unique names. If you implement this validation logic in the Product entity class, the application would need to send one request to the server to query the Products table for products with a given name, followed by another request to insert a new record. However, if you create a UNIQUE KEY constraint for the Products table in the database, the application only needs to send a single request to insert the new record and can rely on the database server to verify that the ProductName of the new record is unique. Both implementations require the same number of logical operations; however, the database implementation requires fewer server requests, results in less data sent back and forth, and allows the database server to choose the best way to enforce the uniqueness rule.

## Integrating Database Validation in Dynamic Data Applications

Here is a T-SQL script you can use to implement validation of the ProductName uniqueness at the database level:

```
ALTER TABLE [dbo].[Products]
    ADD CONSTRAINT [UK_Products]
    UNIQUE (ProductName)
```

Without additional changes, an attempt to create a new Product with a duplicate name through the Dynamic Data web application results in a yellow screen of death, as shown in Figure 9.9.

![](img/11b373b78859e17d318fd76939a0df9d_317_0.png)

FIGURE 9.9 Default error page generated for database exceptions.

Obviously, a yellow screen of death is not acceptable in a production-ready web application, and you need to change it to report the error consistently with other validation results implemented in the application code. In particular, you need to catch the appropriate exceptions and rethrow them wrapped inside of ValidationException instances. Here is how you can override the SaveChanges method of the NorthwindEntities class to do this:

```
public override int SaveChanges(SaveOptions options)
{
    try
    {
        return base.SaveChanges(options);
    }
    catch (UpdateException e)
    {
        HandleSqlException(e);
        throw;
    }
}
```

The new version of the SaveChanges method puts the call to the base method inside of a try/catch block to intercept database errors reported as instances of the UpdateException class by the Entity Framework. The UpdateException itself provides a very generic error message saying that an error has occurred when trying to save changes; however, the underlying database error is still available through its InnerException property used in the HandleSqlException method shown here:

```
private static void HandleSqlException(Exception e)
{
    SqlException error = e.InnerException as SqlException;
    if (error != null)
    {
        if (error.Number == 547)
            HandleReferenceConstraintViolation(error);
        else if (error.Number == 2627)
            HandleUniqueKeyConstraintViolation(error);
    }
}
```

In this example, Microsoft SQL Server is used, so the inner exception will be of type SqlException defined in the System.Data.SqlClient namespace. You can determine what kind of error has occurred by looking at the SQL error Number, which for the violation of a UNIQUE KEY constraint will be 2627 and for a FOREIGN KEY violation will be 547.
