```
string expectedText)
{
    message1.Text = markdownText;
    var markdownDecorator = new
RoomViewModelReaderMarkdownDecorator(mockRoomViewModelReader.Object,
markdown);

    var roomMessages = markdownDecorator.GetRoomMessages(12345);

    var actualMessage = roomMessages.FirstOrDefault();

    Assert.That(actualMessage, Is.Not.Null);

    Assert.That(actualMessage.Text, Is.EqualTo(expectedText));
}

[SetUp]
public void SetUp()
{
    markdown = new Markdown();
    message1 = new MessageViewModel
    {
        AuthorName = "Dianne",
        ID = 1,
        RoomID = 12345,
        Text = "Test!"
    };
    mockRoomViewModelReader = new Mock<IRoomViewModelReader>();
    var roomMessages = new MessageViewModel[]
    {
        message1
    };
    mockRoomViewModelReader.Setup(reader =>
        reader.GetRoomMessages(It.IsAny<int>())).Returns(roomMessages);
}

private MessageViewModel message1;
private Mock<IRoomViewModelReader> mockRoomViewModelReader;
private Markdown markdown;
}
```

STEVE:      Again, that’s great. Didn’t you say you had a second query?
DAVID:      Yeah—notice that the markdown class decorates the IRoomViewModelReader, but that class also has a GetAllRooms method. Is this a good candidate for interface