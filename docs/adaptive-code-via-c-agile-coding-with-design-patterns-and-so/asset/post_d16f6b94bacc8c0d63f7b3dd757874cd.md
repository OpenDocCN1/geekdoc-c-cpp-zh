
DAVID: No, of course! I think this will demonstrate the functionality they want well enough. How about some tests?

DIANNE: Oh, of course. Here they are.

The two unit tests from the RoomControllerTests class are shown in Listing 12-4.

## LISTING 12-4 Unit tests are added to enforce the validation rule on the room name and message text.

Click here to view code image

```csharp
[Test]
[TestCase("Callooh! Callay! O frabjous day!")]
[TestCase("The frumious Bandersnatch!")]
[TestCase("A heffalump or woozle is very confused...")]
public void PostCreateNewRoomWithBlockedWordsCausesValidationError(string roomName)
{
    var controller = CreateController();

    var viewModel = new RoomViewModel { Name = roomName };
    var context = new ValidationContext(viewModel, serviceProvider: null, items: null);
    var results = new List<ValidationResult>();

    var isValid = Validator.TryValidateObject(viewModel, context, results, true);

    Assert.That(isValid, Is.False);
}
//...
[Test]
[TestCase("Callooh! Callay! O frabjous day!")]
[TestCase("The frumious Bandersnatch!")]
[TestCase("A heffalump or woozle is very confused...")]
public void PostAddMessageWithBlockedWordsCausesValidationError(string text)
{
    var controller = CreateController();

    var viewModel = new MessageViewModel { AuthorName = "David", Text = text };
    var context = new ValidationContext(viewModel, serviceProvider: null, items: null);
    var results = new List<ValidationResult>();

    var isValid = Validator.TryValidateObject(viewModel, context, results, true);

    Assert.That(isValid, Is.False);
}
```

DAVID: With the two properties on the view models marked with the ContentFiltered attribute, these tests will pass quite nicely.

DIANNE: Absolutely. Still, there are a few things that I’m not happy about with this design at the moment.

DAVID: What?

DIANNE: Obviously, the hardcoding of the blocked word list. I would consider this to be prudent technical debt, but I would still like to request the blocked word list from a provider interface. This way, I could create an implementing class that returns a static, hardcoded list and provide a more data-driven implementation in future.

DAVID: Yes, that would nicely split the data for the blocked word list from the algorithm of validating the property. Could you use dependency injection?

DIANNE: Unfortunately not. These custom attributes are not very flexible and will not be constructed through the controller or any other extension point exposed by MVC.

DAVID: That’s a shame. How about the service locator pattern?

DIANNE: I usually refer to service locator as an anti-pattern, but in this case it might be the best choice available to us.

DAVID: Shall we leave this as is for now and accept that there is some more technical debt associated with this attribute? That way, we get to make progress and revisit this code if necessary.

DIANNE: I agree. I think that this is likely to change quite drastically in the future, so there is no point in guessing which direction it will take at this point.

## “I want to serve hundreds of users concurrently.”

The final story of the sprint involves Dianne and Steve increasing the scalability of the application. The client has requested that the application support scaling horizontally, rather than vertically. Horizontal scaling means that the application should be able to support more concurrent users through the addition of extra machines. In comparison, vertical scaling is the ability to support more concurrent users through the addition of extra resources to a single machine.

Dianne and Steve understand that the limiting factor to horizontal scaling is the presence in the architecture of a relational database management system (RDBMS), such as Microsoft SQL Server. In comparison to solutions with purpose-built distributed storage that is intended to scale horizontally, it is difficult to add a new instance of SQL Server to a cluster of machines.

Because of this, Dianne investigates the team’s options for replacing the SQL Server database with document storage. She presents MongoDB to the team as a solid and popular alternative that will allow the team to scale the application by adding new machines to a cluster. The only problem standing in the way is current reliance of the application on SQL Server to store and retrieve room and message data.

Luckily, the team has already prepared for this eventuality by programming to interfaces.

DIANNE: All we need to do is create new implementations for the repository interfaces: IRoomRepository and IMessageRepository.

STEVE: We certainly could do that, but I think we could cut out the mapping from record data to view model data and, instead, just serialize and deserialize our view models directly.

DIANNE: That sounds interesting! That way we would just need to create new implementations of the IRoomViewModelReader and IRoomViewModelWriter interfaces that delegate down to MongoDB.

STEVE: Exactly.

The pair sets to work implementing the MongoRoomViewModelStorage class, as shown in Listing 12-5.

## LISTING 12-5 The implementation of the data persistence layer for MongoDB.

Click here to view code image

```csharp
public class MongoRoomViewModelStorage : IRoomViewModelReader,
IRoomViewModelWriter
{
    public MongoRoomViewModelStorage(IApplicationSettings applicationSettings)
    {
        this.applicationSettings = applicationSettings;
    }

    public IEnumerable<RoomViewModel> GetAllRooms()
    {
        var roomsCollection = GetRoomsCollection();
        return roomsCollection.FindAll();
    }

    public void CreateRoom(RoomViewModel roomViewModel)
    {
        var roomsCollection = GetRoomsCollection();
        roomsCollection.Save(roomViewModel);
    }

    public IEnumerable<MessageViewModel> GetRoomMessages(int roomID)
    {
        var messageQuery = Query<MessageViewModel>
            .EQ(viewModel => viewModel.RoomID, roomID);
        var messagesCollection = GetMessagesCollection();
        return messagesCollection.Find(messageQuery);
    }

    public void AddMessage(MessageViewModel messageViewModel)
    {
        var messagesCollection = GetMessagesCollection();
        messagesCollection.Save(messageViewModel);
    }

    private MongoCollection<MessageViewModel> GetMessagesCollection()
    {
        var database = GetDatabase();
        var messagesCollection = database.
            GetCollection<MessageViewModel>(MessagesCollection);
        return messagesCollection;
    }

    private MongoCollection<RoomViewModel> GetRoomsCollection()
    {
        var database = GetDatabase();
        var roomsCollection = database.GetCollection<RoomViewModel>(RoomsCollection);
        return roomsCollection;
    }

    private MongoDatabase GetDatabase()
    {
        var connectionString = applicationSettings.GetValue(MongoConnectionString);
        var client = new MongoClient(connectionString);
        var server = client.GetServer();
        return server.GetDatabase(ProsewareDatabase);
    }

    private readonly IApplicationSettings applicationSettings;
    private static string MongoConnectionString = "MongoConnectionString";
    private static string ProsewareDatabase = "Proseware";
    private static string MessagesCollection = "messages";
    private static string RoomsCollection = "rooms";
}
```

With this implementation in place, the team is able to unleash the potential of horizontal scalability for the Proseware application and the client.

## Sprint demo

At the end of the second sprint, the team prepares to give another demonstration to the client. All of the stories completed in this sprint are collated and their functionality is shown. One of the key actions taken from the sprint retrospective meeting for sprint 1 was to improve the preparation of the demonstration. The team follows up on this diligently, meeting ahead of schedule to run through each story’s functionality without the client present. This helps to mitigate any problems due to differences in the development and demonstration environments. The rehearsal proceeds without a problem, so the team is ready to demonstrate its progress to the client.
