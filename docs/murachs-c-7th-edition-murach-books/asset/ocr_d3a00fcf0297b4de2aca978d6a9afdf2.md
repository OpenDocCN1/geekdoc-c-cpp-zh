# A query that uses eager loading to load related entities

```
var selectedCustomer = context.Customers.Include("Invoices")
.Where(c => c.CustomerId == customerID).Single();
```

# Code that explicitly loads the entities on the many side of a relationship

```
var selectedCustomer = context.Customers
.Where (c => c.CustomerId == customerID).Single();

if (!context.Entry(selectedCustomer).Collection("Invoices").IsLoaded)
context.Entry(selectedCustomer).Collection("Invoices").Load();
```

# Code that explicitly loads the entity on the one side of a relationship

```
var selectedInvoice = context.Invoices
.Where(i => i.InvoiceId == invoiceID).Single();

if (! context.Entry(selectedInvoice).Reference("Customer").IsLoaded)
context.Entry(selectedInvoice).Reference("Customer").Load();
```

# A query that uses lazy loading to load related entities

```
var customerInvoices = context.Customers
.Where(c => c.CustomerId == customerID)
.Select(c => new { c.Name, c.Invoices }).Single();
```

# Description

+   • By default, only the entity objects that are specifically requested by a query are loaded into the DB context. To load related objects, you can use eager loading, explicit loading, or lazy loading.
+   • For eager loading, you use the Include() method with a query path that specifies the related objects to include in the query results.
+   • For explicit loading, you use the Load() method to load the related objects.
+   • To load the related objects on the many side of an association using the Load() method, you use the Entry() method of the DB context to get the entity on the one side of the relationship. Then, you use the Collection() method of that object to get the entities on the many side of the association.
+   • To load the related object on the one side of an association using the Load() method, you use the Entry() method of the DB context to get the entity on the many side of the association. Then, you use the Reference() method of that object to get the entity on the one side of the association.
+   • Before you load related entities explicitly, you should use the IsLoaded property to check that the entities aren’t already loaded. Otherwise, the current data will be overwritten, which may not be what you want.
+   • To use the Include() or Load() method, the query must return an entity type.
+   • For lazy loading, you include the navigation property for the relationship in the query results. For this to work, you must enable lazy loading as shown in the next figure.

Figure 20-9 How to load related objects