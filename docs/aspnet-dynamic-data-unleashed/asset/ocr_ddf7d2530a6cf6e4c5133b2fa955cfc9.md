As discussed in Chapter 8, the overridden `SaveChanges` method of the `UnleashedObjectContext` class calls the `BeforeSaveChanges` method for every added, modified, or deleted entity before submitting changes to the database. This method receives an `ObjectStateEntry` that stores both current and original property values of an entity. It checks if the entity implements the `ISavableObject` interface, calls its `BeforeSave` method.

When your object context class inherits from the `UnleashedObjectContext` or has an equivalent functionality, property interaction rules are automatically invoked when an entity object is saved to the database. In other words, whenever a new page changes an `Order` entity through the `NorthwindEntities` context, the `SubmittedDate` is updated automatically based on the value of the `OrderStatus` property. No changes are required in the web page itself, whether it is a custom page created for editing Order entities or the dynamic Edit page template.

> > **NOTE**
> >
> > The `ISavableObject` interface and its `BeforeSave` method work a lot like the UPDATE triggers in Microsoft SQL Server and other relational database management systems. Although you could have indeed implemented this logic in a database trigger, working at the entity level gives you more flexibility and better tools for implementing business rules. You still have the option of using triggers as an optimization step (see *Business Rules in the Database* later in this chapter).

# Entity Interaction Rules

Complex interaction rules might not be limited by a single entity object or even a single entity type. For example, when an order is fulfilled, the system needs to update the product inventory to decrement the number of items in stock by the number of items shipped to the customer. In the Northwind sample, this means that when the `OrderStatus` property of the Order entity changes to `Fulfilled`, values of the `Quantity` property of the `Order_Detail` entities need to be subtracted from the `UnitsInStock` properties of the corresponding Product entities. In other words, the fulfillment business rule spans three classes, `Order`, `Order_Detail`, and `Product`, and fits into the category of *entity interaction rules*.

There are several different approaches you can take when implementing entity interaction rules with Entity Framework, including (but not limited to):

+   - Implementing Entity Interaction Rules as BeforeSave Methods
+   - Implementing Entity Interaction Rules as Entity Methods
+   - Implementing Entity Interaction Rules as Context Methods