# The MetaModel Class

The MetaModel class serves as a root access point for Dynamic Data components to find information about the tables. In particular, the dynamic URL routing functionality relies on the MetaModel to determine if the incoming request is valid and route it to the appropriate page template. Although multiple instances are supported, a typical Dynamic Data application contains a single MetaModel, created and initialized in the Global.asax as shown in the following example:

```
public class Global : HttpApplication
{
    public static readonly MetaModel DefaultModel = new MetaModel();
    void Application_Start(object sender, EventArgs e)
    {
        DefaultModel.RegisterContext(typeof(NorthwindEntities));
    }
}
```

# Data Model Registration

The MetaModel instance is initially empty and requires a call to one of the RegisterContext methods to populate it with MetaTable objects:

```
public void RegisterContext(Type contextType);
public void RegisterContext(Func<object> contextFactory);
public void RegisterContext(DataModelProvider dataModelProvider);
```

In the simplest case, you can initialize the MetaModel by calling the RegisterContext method that takes a type object such as typeof(NorthwindEntities) in the example just shown. MetaModel has built-in support for Entity Framework and LINQ to SQL and expects a type derived from ObjectContext or DataContext, respectively. Using this type, Dynamic Data creates a new instance of the context class whenever a context is required at run time. Any context class registered this way must have a default constructor.

If your context class doesn't have a default constructor or if you need to perform additional initialization steps, you can use the RegisterContext method that takes a context factory delegate as a parameter:

```
public static readonly MetaModel DefaultModel = new MetaModel();
void Application_Start(object sender, EventArgs e)
{
    DefaultModel.RegisterContext(this.CreateContext);
}

private object CreateContext()
{
    NorthwindEntities context = new NorthwindEntities();
```