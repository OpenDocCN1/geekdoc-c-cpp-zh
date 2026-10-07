# Object Oriented programming using C#

Some tests for the ClientBook class are shown below...

```
[TestMethod]
public void AddClient_TestAddingClient_ShouldNotGenerateException()
{
    MessageManagerSystem.Clients.Client c = new
    MessageManagerSystem.Clients.Client("Simon",
    "Room 1234", "x200", 10);
    try
    {
        cb.AddClient(1, c);
    }
    catch
    {
        Assert.Fail("ClientAlreadyExists exception should not be
thrown for new client");
    }
}
```

```
[TestMethod]
public void AddClient_TestAddingClientTwice_ShouldGenerateException()
{
    MessageManagerSystem.Clients.Client c = new
    MessageManagerSystem.Clients.Client("Simon",
    "Room 1234", "x200", 10);
    try
    {
        cb.AddClient(1, c);
        cb.AddClient(1, c);
        Assert.Fail("ClientAlreadyExists exception should be thrown
if client added twice");
    }
    catch
    {
        MessageManagerSystem.Clients.ClientAlreadyExistsException()
    }
}
```

```
[TestMethod]
[ExpectedException(typeof(MessageManagerSystem.Clients.ClientAlreadyExistsException))]
public void AddClient_TestClientTwice_AlternativeVersion()
{
    MessageManagerSystem.Clients.Client c = new
    MessageManagerSystem.Clients.Client("Simon",
    "Room 1234", "x200", 10);
    cb.AddClient(1, c);
    cb.AddClient(1, c);
    Assert.Fail("ClientAlreadyExists exception should be thrown if
client added twice");
}
```

```
[TestMethod]
public void GetClient_TestGettingUnknownClient_ShouldGenerateException()
{
    try
    {
        cb.GetClient(1);
        Assert.Fail("UnknownClient exception should be thrown if
client does not exist");
    }
}
```