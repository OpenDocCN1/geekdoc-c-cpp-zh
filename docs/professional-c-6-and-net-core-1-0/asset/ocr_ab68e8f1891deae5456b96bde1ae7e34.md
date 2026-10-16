> **NOTE** With the service, you can also restrict the query options by setting the `AllowedQueryOptions` of the `EnableQuery` attribute. You can also restrict logical and arithmetic operators with the properties `AllowedLogicalOperators` and `AllowedArithmeticOperators`.

# Summary

This chapter described the features of the ASP.NET Web API that is now part of ASP.NET MVC. This technology offers an easy way to create services that can be called from any client—be it JavaScript or a .NET client—with the help of the `HttpClient` class. Either JSON or XML can be returned.

Dependency injection was already used in several chapters of this book, particularly in Chapter 31, “Patterns with XAML Apps.” In this chapter you’ve seen how easy it is to replace a memory-based repository using a dictionary with a repository by making use of the Entity Framework.

This chapter also introduced you to OData with which it’s easy to reference data in a tree using resource identifiers.

The next chapter continues with web technologies and gives information on publish and subscribe technologies such as WebHooks and SignalR.