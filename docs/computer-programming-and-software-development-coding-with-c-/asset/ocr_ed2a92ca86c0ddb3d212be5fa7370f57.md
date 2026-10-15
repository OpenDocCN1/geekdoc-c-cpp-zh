```
namespace PeopleViewer.Controllers
{
    public class PeopleController : Controller
    {
        private IPersonReader reader;

        public PeopleController(IPersonReader dataReader)
        {
            reader = dataReader;
        }

        public IActionResult UseRuntimeReader()
        {
            IEnumerable<Person> people = reader.GetPeople();

            ViewData["Title"] = "Using a Runtime Reader";
            ViewData["ReaderType"] = reader.GetType().ToString();
            return View("Index", people);
        }
    }
}
```

And then inside the body of the constructor, we can set our private field. Now our PeopleController class expects that it will be provided with a data reader. The data reader is provided by passing it as an argument to the constructor, and this is known as constructor injection. The next step is to add the data reader to the dependency injection container at startup. Then it will automatically get passed to the constructor. To configure the dependency injection container, we'll go to the startup file of our project and then look at the ConfigureServices method. So let's add our ReaderFactory. For this, we'll say services.AddSingleton, and we'll use the generic type parameter ReaderFactory. And don't forget to bring in a using statement if it's not already there. So what this does is it adds a reference to the ReaderFactory in our dependency injection container. So if our code needs a ReaderFactory, the dependency injection container will take care of newing that up for us. AddSingleton means that we only want to create the ReaderFactory one time. If