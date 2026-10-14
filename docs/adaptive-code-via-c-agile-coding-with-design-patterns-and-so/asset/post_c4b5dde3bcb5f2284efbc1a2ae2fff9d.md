
David scrolls down through the tests file and finds the code shown in Listing 11-3.

### LISTING 11-3 Unit tests for the GET request of the Create action.

```
[Test]
public void GetCreateRendersView()
{
    var controller = CreateController();

    var result = controller.Create();

    Assert.That(result, Is.InstanceOf<ViewResult>());
}

[Test]
public void GetCreateSetsViewModel()
{
    var controller = CreateController();

    var viewResult = controller.Create() as ViewResult;

    Assert.That(viewResult.Model, Is.InstanceOf<CreateRoomViewModel>());
}
```

**DAVID:** We need to know two things: that the request gives a ViewResult instance, and that the Model property is of the expected type, CreateRoomViewModel.

**DIANNE:** Could you unify these into one unit test with two assertions?

**DAVID:** I suppose I could, but then it wouldn’t be immediately clear from the name of the unit test which assertion had failed. I prefer to write quite fine-grained tests with as few assertions as make sense. When a unit test fails, it is then easy to identify the errant behavior.

**DIANNE:** That’s fine. What about the POST request side of the Create action, the one that delegates to the service?

**DAVID:** Here it is.

David scrolls down further and shows Dianne the unit tests of Listing 11-4.

### LISTING 11-4 Unit tests for the POST request of the Create action.

```
[Test]
[TestCase(null)]
[TestCase("")]
[TestCase("  ")]
public void PostCreateNewRoomWithInvalidRoomNameCausesValidationError(string roomName)
{
    var controller = CreateController();

    var viewModel = new CreateRoomViewModel { NewRoomName = roomName };

    var context = new ValidationContext(viewModel, serviceProvider: null, items: null);
    var results = new List<ValidationResult>();

    var isValid = Validator.TryValidateObject(viewModel, context, results);

    Assert.That(isValid, Is.False);
}

[Test]
[TestCase(null)]
[TestCase("")]
[TestCase("  ")]
public void PostCreateNewRoomWithInvalidRoomNameShowsCreateView(string roomName)
{
    var controller = CreateController();

    var viewModel = new CreateRoomViewModel { NewRoomName = roomName };
    controller.ViewData.ModelState.AddModelError("Room Name", "Room name is required");
    var result = controller.Create(viewModel);

    Assert.That(result, Is.InstanceOf<ViewResult>());

    var viewResult = result as ViewResult;
    Assert.That(viewResult.View, Is.Null);
    Assert.That(viewResult.Model, Is.EqualTo(viewModel));
}

[Test]
public void PostCreateNewRoomRedirectsToViewResult()
{
    var controller = CreateController();

    var viewModel = new CreateRoomViewModel { NewRoomName = "Test Room" };
    var result = controller.Create(viewModel);

    Assert.That(result, Is.InstanceOf<RedirectToRouteResult>());

    var redirectResult = result as RedirectToRouteResult;
    Assert.That(redirectResult.RouteValues["Action"], Is.EqualTo("List"));
}

[Test]
public void PostCreateNewRoomDelegatesToRoomRepository()
{
    var controller = CreateController();

    var viewModel = new CreateRoomViewModel { NewRoomName = "Test Room" };
    controller.Create(viewModel);

    mockRoomRepository.Verify(repository => repository.CreateRoom("Test Room"));
}
```

**DAVID:** The first two tests assert that the room name is a required field—it cannot be omitted—and that a validation error drops the user back at the room creation form.

**DIANNE:** I like your use of the TestCase attribute to provide the unit test with some erroneous room names.

**DAVID:** Thanks. I thought it would allow me to write fewer tests.

**DIANNE:** So far, so good. What’s next?

## The room repository

David is unsure of his implementation for the room repository. He opens the file shown in Listing 11-5 so that Dianne can offer her opinion.

**DAVID:** I’ve created an implementation of the IRoomRepository interface for ADO.NET. Here it is.

### LISTING 11-5 The AdoNetRoomRepository allows Room data to be stored in any ADO.NET-compatible database.

```
public class AdoNetRoomRepository : IRoomRepository
{
    public AdoNetRoomRepository(IConnectionIsolationFactory factory)
    {
        this.factory = factory;
    }

    public void CreateRoom(string name)
    {
        factory.With(connection =>
        {
            using (var transaction = connection.BeginTransaction())
            {
                var command = connection.CreateCommand();
                command.CommandText = "dbo.create_room";
                command.CommandType = CommandType.StoredProcedure;
                command.Transaction = transaction;
                var parameter = command.CreateParameter();
                parameter.DbType = DbType.String;
                parameter.ParameterName = "name";
                parameter.Value = name;
                command.Parameters.Add(parameter);

                command.ExecuteNonQuery();
            }
        });
    }

    private readonly IConnectionIsolationFactory factory;
}
```

**DAVID:** I’ve used the Factory Isolation pattern here, and I’m delegating down to a factory interface to control the lifetime of the database connection object. The body of the CreateRoom method is pretty standard ADO.NET code aside from that.

**DIANNE:** Hmm, I’m not so sure that the Factory Isolation pattern is warranted here. Let me just ask Steve.

## Factory Isolation pattern misapplied

Dianne beckons Steve over to get a second opinion on David’s use of the Factory Isolation pattern.

**STEVE:** How can I help?

**DIANNE:** Well, look at this class. David’s used the Factory Isolation pattern here, but I’m just not sure it’s appropriate.

**STEVE:** Hmm, indeed. I think I understand the problem here. You’re using ADO.NET here, right? Let’s have a look at the implementation of the factory.

David opens the file and shows Dianne and Steve the code in Listing 11-6.

### LISTING 11-6 The isolation factory aims to manage the lifetime of a database connection.

```
public class AdoNetConnectionIsolationFactory : IConnectionIsolationFactory
{
    private readonly IApplicationSettings applicationSettings;
    private readonly DbProviderFactory dbProviderFactory;

    public AdoNetConnectionIsolationFactory(IApplicationSettings applicationSettings)
    {
        this.applicationSettings = applicationSettings;
        this.dbProviderFactory = DbProviderFactories
            .GetFactory(applicationSettings.GetValue("DatabaseProviderName"));
    }

    public void With(Action<IDbConnection> action)
    {
        using (var connection = dbProviderFactory.CreateConnection())
        {
            connection.ConnectionString = applicationSettings
                .GetValue("ProsewareConnectionString");
            connection.Open();

            action(connection);
        }
    }
}
```

**STEVE:** The DbProviderFactory.CreateConnection method returns an IDbConnection.

**DAVID:** Yes, that’s right.

**DIANNE:** I understand the problem now. The Factory Isolation pattern is only applicable when the product of the factory may or may not implement IDisposable. The IDbConnection interface inherits from IDisposable, so it effectively forces all implementations to provide a public Dispose method.

**STEVE:** Exactly. So you don’t need to use factory isolation because...

**DAVID:** Because I can just add in a using block, instead.

**DIANNE:** That’s right.

**DAVID:** Okay, so should this just be a normal factory, instead?

**DIANNE:** I would say no. If you look at what’s happening in this class, it’s effectively hiding the DbProviderFactory from clients. I think the factory is needless indirection in this case.

**STEVE:** I agree.

**DAVID:** But that means I’ll have to call DbProviderFactory directly from the room repository implementation. Isn’t that inflexible, especially because DbProviderFactory is a static class?

**STEVE:** That’s true—it would be nice if DbProviderFactory wasn’t a static class. But the room repository implementation depends on ADO.NET, so it isn’t really pollution. The introduction of the factory has made public something that is a concern only internally to the repository’s implementation.

**DAVID:** Okay, that makes sense. And we can ignore this static class call because it is generic enough as it is, right?

**DIANNE:** Yes. Consider what meaningful decoration or adaptation you might make to a DbProviderFactory if it was an interface. Any alternative behavior is more likely to be injected at a higher level—around the IRoomRepository interface.

**DAVID:** I’ve got it. Let me make these changes, and I’ll get back to you.

## Refactoring

David sets to work on refactoring the room repository, resulting in the code shown in Listing 11-7. He calls Dianne and Steve over to assess the changes.

### LISTING 11-7 The refactored room repository uses the DbProviderFactory directly.

```
public class AdoNetRoomRepository : IRoomRepository
{
    private readonly IApplicationSettings applicationSettings;
    private readonly DbProviderFactory databaseFactory;

    public AdoNetRoomRepository(IApplicationSettings applicationSettings,
DbProviderFactory databaseFactory)
    {
        Contract.Requires<ArgumentNullException>(applicationSettings != null);
        Contract.Requires<ArgumentNullException>(databaseFactory != null);

        this.applicationSettings = applicationSettings;
        this.databaseFactory = databaseFactory;
    }

    public void CreateRoom(string name)
    {
        using (var connection = databaseFactory.CreateConnection())
        {
            connection.ConnectionString =
                applicationSettings.GetValue("ProsewareConnectionString");
            connection.Open();

            using (var transaction = connection.BeginTransaction())
            {
                var command = connection.CreateCommand();
                command.CommandText = "dbo.create_room";
                command.CommandType = CommandType.StoredProcedure;
                command.Transaction = transaction;
```
