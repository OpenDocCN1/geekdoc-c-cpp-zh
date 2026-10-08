{

```
public class BookController : Controller
{
    public ActionResult Index()
    {
        var context = new AcmeLibraryDataEntities();
        var books = context.Books;
        return View(books);
    }

    public ActionResult Details(int id)
    {
        var context = new AcmeLibraryDataEntities();
        var book = context.Books.First(b => b.Id == id);
        return View(book);
    }

    public ActionResult Create()
    {
        var book = new Book
        {
            Author = "Author",
            Title = "Title",
            ISBN = "ISBN"
        };
        return View(book);
    }

[HttpPost]
public ActionResult Create(Book newbook)
{
    try
    {
        using (var context = new AcmeLibraryDataEntities())
        {
            context.AddToBooks(newbook);
            context.SaveChanges();
        }
        return RedirectToToAction("Index");
    }
    catch
    {
        return View(newbook);
    }
}

    public ActionResult Edit(int id)
{
    using (var context = new AcmeLibraryDataEntities())
    {
        var book = context.Books.First(b => b.Id == id);
        context.Detach(book);
    }

```

continues