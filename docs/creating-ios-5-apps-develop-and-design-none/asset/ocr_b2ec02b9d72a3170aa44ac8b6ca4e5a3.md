applications, the model might be implemented directly in the controllers. For the most part, though, we want to keep these areas as cleanly separated as possible.

Cocoa Touch uses UIView subclasses for the view, and UIViewController subclasses for the controller. Communication between the model and the view generally uses target/action connections.

On the model side, we can implement our models using a number of different techniques: custom classes, SQLite, or Core Data. In many cases, models and controllers communicate directly with each other—though we can create more loosely bound connections using notifications and delegates (see the data sources discussion in the next section for more information).

# ## DELEGATES

Delegates allow you to extend or modify an object’s behavior without having to subclass the object. You can even change the object’s behavior at runtime by swapping delegates—though in practice, this is somewhat rare.

We have already seen delegates in action. For example, instead of subclassing the UIApplication class within each project, we use a generic UIApplication and implement a custom UIApplicationDelegate. The application delegate protocol defines more than 20 optional methods that we can override to both monitor and alter the application’s behavior.

Any class that uses a delegate usually has a property named (not surprisingly) delegate. By convention, delegate properties should always use weak references. This helps avoid retain loops. However, we need to make sure we have a strong reference to our delegate object somewhere else in our application—otherwise ARC will deallocate it.

```
`@property (nonatomic, weak) IBOutlet id<DelegateProtocol> delegate;`
```

As this example shows, we typically declare a protocol that our delegate must implement. This defines the interface between the delegating class and our delegate. Note that the delegating class is the active partner in this relationship. It calls these methods on the delegate. Some of them pass information to the delegate; others query the delegate. In this way, we pass information back and forth between the two objects.