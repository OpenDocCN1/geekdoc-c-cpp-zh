“Enumerating collections.” It doesn’t matter what structure you use (an array, a HashSet<T>, a Queue<T>, or any other collection type, or even one that you define yourself) as long as it is enumerable. However, to keep things straightforward, the examples in this chapter assume that the customer and address information is held in the customers and addresses arrays shown in the following code example.

# Note

In a real-world application, you would populate these arrays by reading the data from a file or a database.

Click here to view code image

```
var customers = new[] {\n    new { CustomerID = 1, FirstName = "Kim", LastName = "Abercromie",
        CompanyName = "Alpine Sky House" },
    new { CustomerID = 2, FirstName = "Jeff", LastName = "Hay",
        CompanyName = "Coho Winery" },
    new { CustomerID = 3, FirstName = "Charlie", LastName = "Herb",
        CompanyName = "Alpine Sky House" },
    new { CustomerID = 4, FirstName = "Chris", LastName = "Preston",
        CompanyName = "Trey Research" },
    new { CustomerID = 5, FirstName = "Dave", LastName = "Barnett",
        CompanyName = "Wingtip Toys" },
    new { CustomerID = 6, FirstName = "Ann", LastName = "Beebee",
        CompanyName = "Coho Winery" },
    new { CustomerID = 7, FirstName = "John", LastName = "Kane",
        CompanyName = "Wingtip Toys" },
    new { CustomerID = 8, FirstName = "David", LastName = "Simpson",
        CompanyName = "Trey Research" },
    new { CustomerID = 9, FirstName = "Greg", LastName = "Chapman",
        CompanyName = "Wingtip Toys" },
    new { CustomerID = 10, FirstName = "Tim", LastName = 
```