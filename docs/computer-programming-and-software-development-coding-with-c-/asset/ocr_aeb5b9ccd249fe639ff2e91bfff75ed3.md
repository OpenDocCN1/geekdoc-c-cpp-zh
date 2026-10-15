```
```csharp
using ...

namespace PeopleViewer.Controllers
{
    public class PeopleController : Controller
    {
        private ReaderFactory readerFactory;

        public PeopleController(IConfiguration configuration)
        {
            readerFactory = new ReaderFactory(configuration);
        }

        public IActionResult UseRuntimeReader()
        {
            IPersonReader reader = readerFactory.GetReader();
            IEnumerable<Person> people = reader.GetPeople();

            ViewData["Title"] = "Using a Runtime Reader";
            ViewData["ReaderType"] = reader.GetType().ToString();
            return View("Index", people);
        }
    }
}
```
```

We will no longer use the ReaderFactory to get the data reader ourselves. Instead, we will rely on someone else to provide us with a data reader that's ready to use. As we will see, the dependency injection container can handle most of these details for us. The first thing I'll do is remove references to the ReaderFactory. So we'll remove the private field, the body of the constructor, and also the line where we call the GetReader method. Now we do still need a data reader, so I'll add a private field for that, IPersonReader which will call reader. And now we'll update our constructor to require that. So we'll create a parameter for an IPersonReader, and we'll call this dataReader.