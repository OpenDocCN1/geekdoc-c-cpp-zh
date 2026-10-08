# # Why "SUT"?

The variable name stands for "System Under Test" and is a common convention in unit testing. It clearly delineates what is being tested from other objects that are required for the test Why don't the earlier examples use this? Ah, grasshopper — gradual introduction is in play so you aren't drinking from a fire hose

The second test is much more involved, because it tests the raising of the PropertyChanged event. We have to create a subscriber to listen for this event. Windows (and the WPF rendering engine) automatically attach to this event, and we don't want to re-create the rendering engine just to test one method. To test the event, create a subscriber, raise the event, and then assert that the handler of the event was executed.

Tests of this type are typically done with a mocking framework, such as Mocks (the tool used in the samples). Mocking frameworks allow tests for behavior in addition to state, and since the test need to validate that an event was raised, RhinoMocks is the perfect fit. A deep dive into mocking and behavior testing is beyond the scope of this book. Look at the code, digest, and tinker with it. It's a great way to expand your testing knowledge!

Mocking frameworks create proxy objects based on interfaces. For the single event, create an interface (shown in Listing 4-16) that has the required signature for the handler — in this case, the PropertyChanged event.

# ### Listing 4-16: The Event Subscriber

```
public interface IPropertyChangedSubscriber
{
    void Handler(object sender, PropertyChangedEventArgs e);
}
```

The test starts off by creating a mock of the subscriber and registering the PropertyChanged event with the handler. The test acts on the Customer object by changing the name and asserts that the handler was called. The Arg<object>.Is.Any syntax tells Mocks not to test the arguments for equality. Again, the test is just verifying that the event is raised when a property on the Customer object is updated. See the code in Listing 4-17.