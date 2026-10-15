piece of code *in isolation* (for example, as a unit). We must assume that another suite of unit tests has already proved that each of the web services function as expected. As a result, we need to mock those clients so that nothing about our unit test ever leaves a logical area, least of all an entire application tier or layer.

What if we modified the constructor of our TaxHandler class so that instead of creating instances of concrete web service client proxies, it accepts instances of objects that implement contracts? These contracts can correspond to the functionality of the web services, but they’re just contracts. The implementation now is up to the client consuming the TaxHandler class. In our case, that’s either the real application or a suite of unit tests.

So, in C#, we might change the constructor to look like this:

```
public TaxHandler(ITaxService taxService, IStockService stockService)
{
    this.TaxService = taxService;
    this.StockService = stockService;
}
```

Now when the client code calls the ComputeTax method, the TaxHandler class will invoke methods on objects that implement a contract. There won’t be any tight coupling between the TaxHandler class and the physical implementation of the application tier that supports it.

Whether we use a Dependency Injection framework to automatically supply configuration-controlled instances of these objects or whether our test methods define their own implementations of these contracts, the end result is the same: We can now test just the ComputeTax method in isolation and verify that it does as we expect—it makes two web service calls and returns a result that is an aggregate of the results.

I’ll show you more test implementations later in this chapter and walk through more examples of refactoring tightly coupled classes so that their dependencies are pulled away, allowing us to test in isolation. This is especially useful when we want to test view model classes like the ones we created in the previous chapter.

# Unit Testing iOS Applications

Back in the early days of iPhone development, the unit testing framework that was bundled with Xcode for desktop Mac development, SenTest, didn’t work properly on the iPhone. With newer versions of the iOS SDK, however, unit testing capabilities are built right into Xcode for any of your iOS projects. Thankfully, you don’t have to install any additional software, nor do you have to do any extra configuration. As you’ll see later in the chapter, in the area of unit testing Microsoft suffers from a bit of “v1-itis” in that the first release of its tools are just not mature when it comes to built-in support for TDD and unit testing.