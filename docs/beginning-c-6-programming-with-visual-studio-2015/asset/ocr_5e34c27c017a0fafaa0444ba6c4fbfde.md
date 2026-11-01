![](bbox=[0.15, 0.14, 0.78, 0.34])

FIGURE 21-15

This adds a Migrations class to your project, shown in Figure 21-16.

![](bbox=[0.15, 0.48, 0.42, 0.66])

FIGURE 21-16

The Entity Framework will compare the timestamp of the database to your program and advise you when the database is out of sync with your classes. To update the database, simply enter this command in the Package Manager Console at the PM> prompt:

```
Update-Database
```

# CREATING AND QUERYING XML FROM AN EXISTING DATABASE

For the last example you will combine all you have learned about LINQ, databases, and XML.

XML is often used to communicate data between client and server machines or between “tiers” in a multitier application. It is quite common to query for some data in a database and then produce an XML document or fragment from that data to pass to another tier.

In the following Try It Out, you create a query to find some data in the previous example database, use LINQ to Entities to query the data, and then use LINQ to XML classes to convert the data to XML. This is an example of Database First as opposed to Code First programming where you take an existing database and generate C# objects from it.