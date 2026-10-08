```
{
var context = TempData["context"] as AcmeLibraryDataEntities;
var book = TempData["book"] as Book;
if (context != null && book != null) {
    UpdateModel(book, collection.ToValueProvider());
    context.SaveChanges();
    context.Dispose();
}
return RedirectToAction("Index");
}
catch {
    return View();
}
```

The UpdateModel method has several overloads. The one used in the example updates the book variable (representing the model) from the controller's value provider. The FormCollection instance passed to the method can be converted to a value provider with the ToValueProvider method. All the mechanic work is done by this simple method — like parsing the string of properties, and converting them to the appropriate types (such as handling the DateTime value of the Published property).

With binding, you can go even further. Let's see the original implementation of the Create actions in the controller:

```
public ActionResult Create() {
    var context = new AcmeLibraryDataEntities();
    var book = new Book {
        Author = "*Author*",
        Title = "*Title*",
        ISBN = "*ISBN*"
    };
    context.AddToBooks(book);
    TempData["context"] = context;
    TempData["book"] = book;
    return View(book);
}
```

```
[HttpPost]
public ActionResult Create(FormCollection collection) {
    return Edit(-1, collection);
}
```

The first Create method instantiated AcmeLibraryDataEntities so that the Create method can simply call the Edit action. This context is not really required by the time the View is displayed, because it will have an active role only in the second Create method.