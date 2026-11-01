You can also select all entities of a particular type by using the OfType LINQ extension method, such as the next query, which returns all entities of Customer type:

```
var customers = from c in context.Users.OfType<Customer>()
    select c;
```

Although these LINQ queries work with all three types of inheritance mapping, it is important that you understand how each type of mapping is implemented at the database level, how each type of LINQ queries are translated into SQL, and how they affect the performance of your application. If you are considering using inheritance in your entity model, carefully review the tradeoffs described in this section and measure the impact of inheritance on the performance of your system by profiling it. Do not assume that simple LINQ queries will be fast.

![](bbox=[0.1, 0.47, 0.55, 0.68])

FIGURE 9.1 Conceptual model with inheritance hierarchy.

# Table-per-Concrete Type Mapping

With table-per-concrete type mapping, each concrete class in the inheritance hierarchy gets its own table. The Employees and Customers tables in the database diagram shown in Figure 9.2 include columns for storing not only the concrete types, Employee and Customer, respectively, but also the abstract base type, User. Notice how both of these tables include the FirstName and LastName columns.

![](bbox=[0.1, 0.88, 0.55, 0.95])

FIGURE 9.2 Table-per-concrete type mapping.