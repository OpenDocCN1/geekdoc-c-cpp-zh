DAVID:      No, of course! I think this will demonstrate the functionality they want well enough.
            How about some tests?

DIANNE:   Oh, of course. Here they are.

The two unit tests from the RoomControllerTests class are shown in Listing 12-4.

# LISTING 12-4 Unit tests are added to enforce the validation rule on the room name and message text.

Click here to view code image

```
[Test]
[TestCase("Callooh! Callay! O frabjous day!")]
[TestCase("The frumious Bandersnatch!")]
[TestCase("A heffalump or woozle is very confusel...")]
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
[TestCase("A heffalump or woozle is very confusel...")]
public void PostAddMessageWithBlockedWordsCausesValidationError(string text)
{
    var controller = CreateController();

    var viewModel = new MessageViewModel { AuthorName = "David", Text = text};
    var context = new ValidationContext(viewModel, serviceProvider: null, items: null);
    var results = new List<ValidationResult>();

    var isValid = Validator.TryValidateObject(viewModel, context, results, true);

    Assert.That(isValid, Is.False);
}
```