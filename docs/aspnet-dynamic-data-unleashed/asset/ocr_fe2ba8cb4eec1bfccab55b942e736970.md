![](bbox=[0.11, 0.13, 0.54, 0.45])

FIGURE 2.6 Adding database objects to the model.

The Update Wizard is very similar to the Entity Data Model Wizard you used to create the model initially. It uses the connection string stored in the application configuration file to retrieve the list of database tables, views, and stored procedures that exist in the target database but have not been added to the entity model yet. Any tables that were previously included in the model are refreshed automatically, meaning that database schema changes are merged in the model. For this example, add the Suppliers table and click the Finish button.

> NOTE
> 
> Note that the Update Wizard uses the pluralization and foreign key column options you selected when creating the model. Avoid changing these options; it results in inconsistently named entity classes and object set properties.

When the Update Wizard finishes updating the model, you see the new entity types, Supplier in this case, displayed in the Entity Designer along with the association (shown as a dotted line) that was created based on the SupplierID foreign key, similar to what is shown in Figure 2.7.

The Entity Framework supports several different types of associations. What we have in this case is a one-to-many association between Supplier and Product entities. In other words, for each Supplier instance there might be zero or more Product instances as indicated by the * symbol on the design surface. The SupplierID property is nullable, so a Product does not have to have a Supplier specified, which is indicated by the 0..1 multiplicity in the model. If the SupplierID column did not allow null values, making a