```
typeof(TestBookRepository);

[TestMethod]
public void InsertValidBooksOk()
{
    for (int i = 1; i <= 10; i++)
    {
        var book = new Book
        {
            Author = "Author" + i,
            Title = "Title" + i,
            ISBN = "012345678902",
            Published = new DateTime(1998, 1, 1),
            Published = "Wrox"
        }
    }
    var bc = new BookController();
    var result = bc.Create(book) as RedirectToRouteResult;
    Assert.IsNotNull(result);
    Assert.AreEqual(result.Values["action"], "Index");
}

var list = new BookController().Index() as ViewResult;
Assert.IsNotNull(list);
var model = list.View.Model as IEnumerable<IBook>;
Assert.AreEqual(model.Count(), 10);

```

> Code file [BookControllerTest.cs] available for download at Wrox.

MyClassNameInitialize injects the TestRepository class into BookController, so when you instantiate a BookController, the test repository is used.

The InsertValidBooksOk test method evaluates the insertion of ten books. After each insertion, it checks whether the result of the action is a RedirectToRouteResult, forwarding the user to the "Index"—is the sign of proper operation. When all books are inserted, it checks that the list contains ten elements.

The test project contains another test case (not listed here) to check what happens when a book with a wrong publishing date is about to be inserted.

With the Run All Tests in Solution command, you can run all AcmeLibrary unit tests. The checkmarks (as shown in Figure 18-28) indicate successful test cases.

![](bbox=[0.513, 0.698, 0.927, 0.843])

FIGURE 18-28: Successful test cases