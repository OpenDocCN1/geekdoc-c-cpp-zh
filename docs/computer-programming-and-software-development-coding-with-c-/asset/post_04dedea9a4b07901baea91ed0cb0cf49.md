
// Act
var result = controller.UseRuntimeReader() as ViewResult;
class Microsoft.AspNetCore.Mvc.ViewResult
Represents an ActionResult that renders a view to the response.

Before going on, I'm going to do a little bit of a sanity check to make sure that the result is populated. So I'll say Assert.IsNotNull, and then we'll check this result variable. And if it is null for some reason, we'll add a message that says "Controller action failed". And this really means there's something that went wrong outside of what we're specifically testing for. So now that we have this result, let's get the model out of it. So I'll create a variable for the model, and we'll set it to result.model, and then I'll cast this to an IEnumerable of Person since I know that's the type that we're specifically dealing with.

// Act
var result = controller.UseRuntimeReader() as ViewResult;
Assert.IsNotNull(result, "Controller action failed");

// Assert
Assert.Inconclusive();
}

You'll notice some greens squiggles here, and that's because it's warning us that result may be null. Well, the assertion that we have on the line before this ensures that it is not null, so I can add the exclamation point to say, I know this is not null.

// Act
var result = controller.UseRuntimeReader() as ViewResult;
Assert.IsNotNull(result, "Controller action failed");
var model = result.Model as IEnumerable<Person>;

// Assert
Assert.Inconcl

(local variable) ViewResult? result
'result' may be null here.
CS8602: Dereference of a possibly null reference.
Show potential fixes (Alt+Enter or Ctrl+.)

TestMethod1

So now that we have our model, let's make sure that it's populated and has the things that we expect. So we'll check to make sure that it's not null, and if it is, we'll say 'Model property is not populated', and then we'll make sure that there are two items in it. So we'll Assert.AreEqual, the number 2, our expected value, and model.Count, which will tell us how many items are in our model. And again, I have a warning that model may be null. And since I just checked it, I'll say I know it's not null. So let's save this and run our tests. And for this, we'll go to the Test Explorer. If you don't already have it open, you can go to the Test menu and then choose Test Explorer, and it will open the window for you. I'll click on the Run All button, and this will recompile our project and run our unit tests.

// Arrange
IPersonReader reader = new FakeReader();
var controller = new PeopleController(reader);

// Act
var result = controller.UseRuntimeReader() as ViewResult;
Assert.IsNotNull(result, "Controller action failed");
var model = result!.Model as IEnumerable<Person>;

// Assert
Assert.IsNotNull(model, "Model property is not populated");
Assert.AreEqual(2, model!.Count());
}

And that shows us that we have one test that passed, the one we just did, and one that's been skipped. And the reason it's been skipped is because we have an Assert.Inconclusive inside of our test.

}
[TestMethod]
public void PeopleController_OnRuntimeReaderAction_ReaderTypeIsPopulated()
{
    Assert.Inconclusive();
}
}

So let's look at our second test,
PeopleController_OnRuntimeReaderAction_ReaderTypeIsPopulated. So in this case, I'm going to go through the same process, but I'm going to expect that the reader type is populated with the value for our fake reader. To get started, I'll copy some code from our previous test and then make some modifications. In this case, I'll take the entire Arrange section and the first two lines of our Act section.
We'll copy those to the clipboard and then put them into our test.

```csharp
[TestMethod]
public void PeopleController_OnRuntimeReaderAction_ReaderTypeIsPopulated()
{
    // Arrange
    IPersonReader reader = new FakeReader();
    var controller = new PeopleController(reader);
    var expectedType = "PeopleViewer.Test.FakeReader";

    // Act
    var result = controller.UseRuntimeReader() as ViewResult;
    Assert.IsNotNull(result, "Controller action failed");
}
```

And as a reminder, the Arrange section creates a fake data reader and passes it to our PeopleController constructor. And our Act section calls our UseRuntimeReader method, casts it to a ViewResult, and makes sure that the result is not null. In the Arrange section, I'm going to add one more line, and this is a variable for our expected value, and I'll name this expectedType, and we'll set it to PeopleViewer.Test.FakeReader, and that's the type name for our FakeReader class. Now in our Act section, I want to get the actual type from our controller. So we'll say var actualType, and we'll set that equal to result.ViewData, and then we'll pass in our ReaderType string. And as a reminder, if we go back to our PeopleController class, this is the value that we're looking for. As with our other tests, I do need to tell this result is not null, and now we can do our assertions. First, we can check to make sure that it's not null. And if it is, we'll have the error message, ReaderType is not populated.

// Act
var result = controller.UseRuntimeReader() as ViewResult;
Assert.IsNotNull(result, "Controller action failed");
var actualType = result!.ViewData["ReaderType"];

// Assert
Assert.IsNotNull(actualType, "ReaderType is not populated");
Assert.AreEqual(expectedType, actualType);
}

And for our second assertion, we'll make sure that our values are equal. So this compares the expectedType to the actualType. So let's go back to our Test Explorer and rerun our tests. And now we see both of them pass. What I like about these tests is that they're both fairly small and easy to read and write. When we have unit tests that are easy to read and write, we are more likely to use them. And interfaces are a great tool to help us get there. In summary we saw a couple of scenarios where interfaces are very useful, first, by changing a data reader in an internal application using configuration and then by creating a dynamic factory that makes it easier to support multiple clients with different data storage needs. We are relying on interfaces to supply the important functionality. In our case, it is getting people from our data source. But in this process, we remove the details of interacting with any particular data source. Our application can work with any data reader as long as it implements our interface. We also saw how we can change the behavior of our application without recompiling. Based on configuration, we can pull a data reader out of an assembly on the filesystem. This works great for our scenario of having multiple clients because we can change the data reader without recompiling

the application. This gives us easier maintenance because we can keep the bulk of our application unchanged. And if a client switches to a different data source, we do not have to redeploy the entire application, just the parts that are relevant to the new data source. And we saw how interfaces can make unit testing easier. They allow us to isolate our code from a real data reader. Instead, we can supply our own fake data reader, and that provides us with consistent test data. Next up, we will look at what it means to explicitly implement an interface. This is a rather obscure feature, but we will see that the concepts help us when we look at default interface implementation in the last chapter.

## Chapter 8 Implementing Explicit Interfaces

Explicit interface implementation is a topic that I get asked about quite a bit, usually because of the Visual Studio popup that offers to implement all members explicitly. You will probably not come across explicit implementation very often, but there is at least one use case where we must use it, and it also helps us understand another feature of interfaces that we will see in the next chapter. We will take a look at what explicit implementation is and why we might need to use it. We will see that explicit implementation limits how interface members are used by forcing us to reference the interface. We will also see how explicit implementation resolves the problem of implementing interfaces with conflicting methods, such as two methods with the same name, but different return types. This is particularly useful when we have interface inheritance. We will see this by looking at the IEnumerable and IEnumerable interfaces. We will build our own implementation of IEnumerable and see how explicit implementation is necessary to resolve conflicting methods. And this is also preparation for default interface implementation. The restrictions on explicitly implemented members also apply to members with default implementation. Before looking at explicit implementation, let's review standard interface implementation. In this case, we have an ISaveable interface with one method, Save, and we have a Catalog class that implements the ISaveable interface.
