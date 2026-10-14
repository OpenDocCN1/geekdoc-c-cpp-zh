
```csharp
allRooms.Add(mapper.MapRoomRecordToRoomViewModel(roomRecord));
}
return allRooms;
}

public void CreateRoom(string roomName)
{
    repository.CreateRoom(roomName);
}
}
```

**DAVID:** I decided to implement both interfaces in one class, because they both shared a dependency on the IRoomRepository. However, I think this resembles the original controller class—what have we gained with this refactor?

**DIANNE:** The main benefit is that the controller is now more focused on its main responsibilities. Instead of being responsible for orchestrating the mapping from records to viewmodels, it can now focus on responding to validation. The fact that the controller no longer has knowledge of the RoomRecord class is compelling enough.

**DAVID:** Yes, I suppose it was starting to do too much, wasn’t it?

**DIANNE:** It didn’t really obey the single responsibility principle. If we weren’t using a repository, we wouldn’t need a mapper. This would be a change lower down in the architectural layers. Controllers should not be concerned with such changes.

David and Dianne agree that this story is now ready to be committed.

## “I want to view the messages that have been sent to a room.”

Dianne works on the next story in tandem with David, by using pair programming. While Dianne writes the code, David looks on and offers suggestions.

![](img/65c1bad7a6b3cffae8cbb79664f0708b_383_0.png)

### Note

> *Pair programming* is a common practice in Agile software development that originated with the Extreme Programming (XP) methodology: two programmers work together on a particular functionality. While one of the pair types, the other is able to consider the best way of implementing a method, class, or unit test.

**DIANNE:** Shall we start with the controller?

**DAVID:** Yes, that seems like a good place to begin.

**DIANNE:** We’re going to need a new HttpGet handler for viewing room messages. What shall we call this?

**DAVID:** Something like GetMessages?

**DIANNE:** That would be good, but ASP.NET MVC uses the controller name and method name to form the URL for the request.

**DAVID:** Of course, I forgot. How about just calling it Messages? It is part of the RoomController, so the URL will be /Room/Messages.

**DIANNE:** Okay, that makes sense. We’ll also need a parameter for identifying which room’s messages we want to see.

**DAVID:** We’ve got the room ID, which uniquely identifies a room. Could we use that?

**DIANNE:** Is it an integer or a long?

**DAVID:** I thought an integer would suffice.

**DIANNE:** We’ll also need a new viewmodel for this view. Following the naming convention you’ve used so far, this should be MessageListViewModel, right?

**DAVID:** Yes. We can just pass an instance of it to the View method on the controller and return the resulting ViewResult.

**DIANNE:** The IRoomViewModelReader will need a new method for querying the messages in a room.

**DAVID:** I suppose that should be called GetRoomMessages, and it should also accept the room ID as a parameter.

**DIANNE:** I’ll define it on the interface and create a stub on any implementing classes so that we can determine how the controller changes might work.

Dianne creates the method shown in Listing 11-12.

### LISTING 11-12 The Messages method retrieves all messages associated with a room, by ID.

```csharp
[HttpGet]
public ActionResult Messages(int roomID)
{
    var messageListViewModel = new MessageListViewModel(reader.GetRoomMessages(roomID));

    return View(messageListViewModel);
}
```

**DIANNE:** This looks good. Let’s fill in the implementation of the IRoomViewModelReader.GetRoomMessages method.

**DAVID:** Okay, the only implementation so far makes use of an IRoomRepository interface. I think we’ll need a new IMessageRepository interface so that we can retrieve messages.

**DIANNE:** Agreed. We should inject it in just like the other dependencies.

**DAVID:** When we have that repository available in the class, we need to request from it the messages for a given room ID and pass them to the mapper.

**DIANNE:** So the mapper is responsible for converting records from the repository to viewmodels that the controller can use, right? It looks like there’s only an `IRoomViewModelMapper` available. It feels a little too much to create a new `IMessageViewModelMapper`. Can we rename this interface to something more generic?

**DAVID:** How about `IViewModelMapper`? That way it becomes useful for mapping all records to viewmodels.

**DIANNE:** How does this look?

Dianne shows David the code in Listing 11-13.

### LISTING 11-13 The class that maps records to viewmodels now contains a method for retrieving room messages.

```csharp
public class RepositoryRoomViewModelService : IRoomViewModelReader, IRoomViewModelWriter
{
    private readonly IRoomRepository roomRepository;
    private readonly IMessageRepository messageRepository;
    private readonly IViewModelMapper mapper;

    public RepositoryRoomViewModelService(IRoomRepository roomRepository,
        IMessageRepository messageRepository, IViewModelMapper mapper)
    {
        Contract.Requires<ArgumentNullException>(roomRepository != null);
        Contract.Requires<ArgumentNullException>(messageRepository != null);
        Contract.Requires<ArgumentNullException>(mapper != null);

        this.roomRepository = roomRepository;
        this.messageRepository = messageRepository;
        this.mapper = mapper;
    }

    public IEnumerable<MessageViewModel> GetRoomMessages(int roomID)
    {
        var roomMessages = new List<MessageViewModel>();
        var roomMessageRecords = messageRepository.GetMessagesForRoomID(roomID);

        foreach (var messageRecord in roomMessageRecords)
        {
            roomMessages.Add(mapper.MapMessageRecordToMessageViewModel(messageRecord));
        }

        return roomMessages;
    }
}
```

**DAVID:** That looks good to me.

David and Dianne continue to implement the repository method `IMessageRepository.GetMessagesForRoomID()`, which loads the message from the Microsoft SQL Server database. After this method is implemented, they move on to the next user story.

## “I want to send plain text messages to other room members.”

David swaps places with Dianne to implement the final story of the sprint.

**DAVID:** This should be really easy now that we have a pattern in place for reading and writing data.

**DIANNE:** Sort of, yes. But remember, one of the requirements of this story is that the request will be made asynchronously.

**DAVID:** Oh. So it won’t be a full-page postback?

**DIANNE:** No, the user interface will send the data via an AJAX request.

> **Note**
> 
> Some definitions: AJAX stands for Asynchronous JavaScript and XML. XML stands for Extensible Markup Language. AJAJ stands for Asynchronous JavaScript and JSON. JSON stands for JavaScript Object Notation.

**DAVID:** Hold on. You mean AJAJ, don’t you?

**DIANNE:** I suppose I do!

**DAVID:** What makes this controller action different, then?

**DIANNE:** Two things, really. When the ModelState.IsValid property is true, we should use the IRoomViewModelWriter to save the message. But we should then return the viewmodel as a JsonResult.

**DAVID:** And what do we do when the model state is not valid?

**DIANNE:** In that case, return an HttpStatusCodeResult with an HTTP 400 error.

**DAVID:** That’s a client error response code, isn’t it?

**DIANNE:** Yes. Specifically, it’s a Bad Request response.

David shows Dianne the code in Listing 11-14.

### LISTING 11-14 The AddMessage method on the RoomController class.

```csharp
[HttpPost]
public ActionResult AddMessage(MessageViewModel messageViewModel)
{
    ActionResult result;

    if (ModelState.IsValid)
    {
        writer.AddMessage(messageViewModel);

        result = Json(messageViewModel);
    }
    else
    {
        result = new HttpStatusCodeResult(400);
    }

    return result;
}
```

**DAVID:** What about the AddMessage method on the IRoomViewModelWriter?

**DIANNE:** I think we can use the same pattern as before. This part of the code does not care whether it is called synchronously or asynchronously, so it will not change the pattern that we’ve established so far.

David proceeds to follow the same pattern that the IRoomViewModelWriter.CreateRoom method uses, which results in the AddMessage method shown in Listing 11-15.

### LISTING 11-15 The AddMessage method on the RoomViewModelWriter class.

```csharp
public void AddMessage(MessageViewModel messageViewModel)
{
    var messageRecord = mapper.MapMessageViewModelToMessageRecord(messageViewModel);
    messageRepository.AddMessageToRoom(messageRecord.RoomID,
        messageRecord.AuthorName,
        messageRecord.Text);
}
```

With this change, and the creation of a further repository method to retain the message record in Microsoft SQL Server via ADO.NET, the story is complete.

David and Dianne have now finished the stories that were assigned to the sprint, just in time for the sprint demo.

## Sprint demo

At the end of the week, the team arranges to meet the client and demonstrate its progress thus far. The stories to be completed are assembled, and the functionality of each one is shown. The client is invited to provide feedback and alter the direction in which to take the product from here.

The sprint demo has many benefits. First, it allows the team to ensure that it is always aligned with
