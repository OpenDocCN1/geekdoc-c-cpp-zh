introduction of Language Integrated Query (LINQ). The core idea is to provide syntax for query expressions right inside the language, which compile down to API calls that can be targeted at various data sources. The high-level overview is shown in Figure 19.3.

![](bbox=[0.07, 0.18, 0.92, 0.52])

FIGURE 19.3 LINQ general overview.

# LINQ by Example

Before we start investigating LINQ from a language and framework point of view, let's revisit our running example by reformulating the query in terms of LINQ for each of the three data domains. You'll see how the same syntactical language surface for query expressions can be used against different domains, abstracting away the technicalities we had to deal with manually before.

# In-Memory Data

Starting from the same in-memory collection of products, we want to get rid of our imperative code that obfuscated the meaning of our query before. Here, we're using the LINQ to Objects implementation, which implements the query pattern for objects that implement IEnumerable<T>. Given the following data source, we want to express a query that will give us back only the products with a price less than $25:

```
var products = new List<Product> {
    new Product { Name = "Chai", Price = 18.00m },
    new Product { Name = "Chang", Price = 19.00m },
    new Product { Name = "Aniseed Syrup", Price = 10.00m },
    new Product { Name = "Chef Anton's Cajun Seasoning", Price = 22.00m },
    new Product { Name = "Chef Anton's Gumbo Mix", Price = 21.35m },
    new Product { Name = "Grandma's Boysenberry Spread", Price = 25.00m },
    new Product { Name = "Uncle Bob's Organic Dried Pears", Price = 30.00m },
}
```