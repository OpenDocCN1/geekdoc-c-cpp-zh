
“object graph”) that represents the data for your application. In a sales application, example objects could be classes like Customer, SalesRegion, and SalesPerson.

## Business Layer (BL)

The BL is the implementation of the business rules for the application. This layer ensures that the data in the Model adheres to the law of the land.

## View

The View represents the pieces of the application that interact with the user. For WPF, this is the collection of Windows that compose the application.

The biggest gap with displaying an object graph (Model) in a View is that applications seldom display only one type of object at a time. If the Window allows for editing a customer, then it probably needs to display the sales regions, sales people, and so forth.

Combining multiple objects into a data object clouds the Model, and placing all that code into the view places too much knowledge in the View—not to mention a total inability to unit test the code. The compilation of the required parts of the object graph should not detract from any other part of the application.

The command objects are another consideration. There isn’t a tidy place in the traditional application layers to place the custom commands. The code contained in the commands is (typically) Business Logic, but the Window needs to bind to the commands and is therefore specific to the View.

## Introducing the ViewModel

The ViewModel fills that gap. It is designed to be a single class that pulls in all the necessary data points and commands into a one-stop shop for a particular view. Each view typically has its own ViewModel, but that is entirely dependent on your particular application.

As Chapter 3 discusses, WPF automatically monitors any class that implements either INotifyPropertyChanged (for items bound to a property of a class) and/or INotifyCollectionChanged (for items bound to a collection of items). These interfaces should be implemented in one of two camps — the ViewModel or the Model.

Implementing those two interfaces in the ViewModel is the more academic, textbook implementation. This is because it separates user interface code from the Model. It also requires a lot of additional work, because it entails recoding all the properties and collections of your Model to include raising the proper events.

Implementing in the Model reduces work, because it merely entails adding a few lines of code into properties already being implemented in the classes. A main argument against Model implementation revolves around code reuse. For example, if the Model is also used by an ASP.NET application, those events are still raised, but no one is listening. This could potentially present a performance issue. Of course, if you use the same model for WPF and non-WPF Views, then a simple flag passed into the constructor of the Model classes indicating whether the events should be raised or not resolves that issue.

Both ways are valid implementations. Your application and specific situation will most likely dictate where those interfaces are implemented.

In Chapter 3, you discover that if a control doesn’t have an explicit DataContext, it is inherited from the closest parent in the control tree that does have a DataContext explicitly assigned.

When developing WPF applications using the ViewModel pattern, the instantiated ViewModel becomes the Window’s (or user control’s) DataContext.

## Show me the code!

The full code for the ViewModel samples is in the project Chapter4ViewModelModels and Chapter4ViewModelModelsTests in the Chapter4 Solution.

## Just what are you building?

The Window (or View, to use “architecture speak”) is a simple customer maintenance form. The user can select a customer and edit his name and sales region. Clicking the Add Customer button adds a customer to the list. You’re right — not very realistic, but it demonstrates the ViewModel principles. Figure 4-6 shows the completed sample user interface.

![](img/80ff26f06fc9ab951e1cd4257b867366_662_0.png)

## The model

Okay, enough talk. For the sample ViewModel, you need to define a Model.

## Why “internal”?

The NotifyPropertyChanged method is marked with the internal access modifier instead of protected for one main reason — testing. Protected methods can be accessed only from derived classes, whereas internal methods can be accessed by any sibling class in the same assembly.

The assembly level attribute InternalsVisibleTo specifies what other assemblies have access to the internal methods and classes of the assembly decorated with the attribute. Adding this attribute to the Chapter4ViewModels project (usually placed in the assemblyinfo.cs class) and specifying the test project (Chapter4ViewModelsTests) grants access for your tests to the internals.

Listing 4-12 shows the base class from which all the Model classes will derive. The base class implements the INotifyPropertyChanged interface as well as the IsDirty property.

## Listing 4-12: ModelBase

```
public class ModelBase : INotifyPropertyChanged
{
    public bool IsDirty { get; private set; }
    public event PropertyChangedEventHandler PropertyChanged;
    internal void NotifyPropertyChanged(object sender, string propertyName)
    {
        if (PropertyChanged != null)
        {
            PropertyChanged(sender, new PropertyChangedEventArgs(propertyName));
        }
        IsDirty = true;
    }
}
```

Listings 4-13 and 4-14 show the Customer and SalesRegion classes that will populate the View. For each property in the class (except for the primary key and the collection properties), there is a check to see whether the value of the property is being set to a new value. If it is new, then the PropertyChanged event is raised. The NotifyPropertyChanged method also sets the IsDirty flag to True to indicate that the model has changes that need to be persisted.

## Listing 4-13: The Customer Model Class

```
public class Customer : ModelBase
{
    private string _name;
    private SalesRegion _region;
    public int ID { get; set; }
    public string Name
    {
        get { return _name; }
        set
        {
            if (value == _name)
            {
                return;
            }
            _name = value;
            NotifyPropertyChanged(this, "Name");
        }
    }
    public SalesRegion SalesRegion
    {
        get { return _region; }
        set
        {
            if (value == _region)
            {
                return;
            }
            _region = value;
            NotifyPropertyChanged(this, "SalesRegion");
        }
    }
}
```

## Listing 4-14: The SalesRegion Model Class

```
public class SalesRegion:ModelBase
{
    private string _name;
    public int ID {get; set;}
    public string Name
    {
        get { return _name; }
        set
        {
            if (value == _name)
            {
                return;
            }
            _name = value;
            NotifyPropertyChanged(this, "Name");
        }
    }
}
```

## Why “SUT”?

The variable name stands for System Under Test and is a common convention in unit testing. It clearly delineates what is being tested from other objects that are required for the test. Why don't the earlier examples use this? Ah, grasshopper — gradual introduction is in play so you aren't drinking from a fire hose!

## Model unit tests

There isn't much to test in the model. You don't typically write tests against the .NET Framework itself — one has to assume that it works! The only real logic in this sample is setting of the `IsDirty` flag and the raising of the `PropertyChanged` event when something changes.

The first test is to verify that the `IsDirty` flag gets set when a property changes, and it is very straightforward. You create a new `Customer`, assert that the `IsDirty` flag is `False`, make a change, and then assert that the `IsDirty` flag is `True`. This test is shown in Listing 4-15.

### Listing 4-15: Testing the IsDirty Flag

```csharp
[Test]
public void Should_Set_Is_Dirty_On_Property_Change()
{
    var sut = new Customer();
    Assert.IsFalse(sut.IsDirty);
    sut.Name="New Name";
    Assert.IsTrue(sut.IsDirty);
}
```

The second test is much more involved, because it tests the raising of the `PropertyChanged` event. You have to create a subscriber to listen for this event. Windows (and the WPF rendering engine) automatically attach to this event, but you don't want to re-create the rendering engine just to test one method. To test the event, create a subscriber, raise the event, and then assert that the handler of the event was executed.

Tests of this type are typically done with a mocking framework, such as RhinoMocks (the tool used in the samples). Mocking frameworks allow tests for behavior in addition to state, and because the test needs to validate that an event was raised, RhinoMocks is the perfect fit. A deep dive into mocking and behavior testing is beyond the scope of this book. Look at the code, digest it, and tinker with it. It's a great way to expand your testing knowledge!
