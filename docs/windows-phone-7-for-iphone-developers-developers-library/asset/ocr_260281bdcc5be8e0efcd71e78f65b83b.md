Now that we’ve modified the view model to save the list of books to isolated storage, we need to modify it to read from isolated storage when the view model is created by the view model locator. I’ve added a method called `LoadBooks()` to the `MainViewModel` class which reads books from isolated storage by way of the service provider, uses the static extensions to convert from model to view model domain, and then populates the view model accordingly. Because the view model is data bound, it will see this newly loaded data immediately.

```
```csharp
private void LoadBooks()
{
    Books.Clear();
    IEnumerable<Book> books = serviceProvider.LoadBooks().ToViewModel();
    foreach (Book b in books)
        Books.Add(b);
}
```
```

I strongly encourage you to go open up the Menmuse code sample for this chapter. Play around with navigating between the master view (books) and the details view (the pivot page with a character view model bound). Create books, delete books, exit the application, and return to the application. This will help you get a feel for how all the various parts of MVVM are coming together to help you build a more organized, clean, well-structured application.

As a user exercise, make the calls to service provider asynchronous and turn on an “indefinite” progress bar while calls to the service provider are happening. To do this, you can make use of the callback pattern (much like the delegate pattern or completion blocks for you iPhone developers) to call code when the service provider is finished, which will turn off the “busy” indicator. The busy indicator can be bound to a view model property, so all you really need to do is toggle the Boolean value of an `IsBusy` property to let your users know when data operations are in progress.

# Summary

Building “hello world” samples in any language, for any platform, for any device, is relatively easy. Taking the syntactical knowledge you’ve learned from building dozens of “hello world” applications and applying that to the construction of a well-organized application that will stand up to real-world development life cycles and withstand the rigor of multiperson development teams consisting of designers and developers alike is a daunting task.

This chapter provided you with an overview of the Model–View–View–Model pattern and how it differs from traditional and iOS MVC implementations. Using the MVVM Light toolkit for Windows Phone 7, you can build some pretty complex applications without creating complex, difficult to read and maintain code. By keeping your concerns