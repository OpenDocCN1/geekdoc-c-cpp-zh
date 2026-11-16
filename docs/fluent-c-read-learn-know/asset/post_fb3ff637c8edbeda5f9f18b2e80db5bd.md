
## THE LOGICAL OBSERVER

Some design patterns, like the Strategy pattern we've been exploring, do seem to imply a canonical structure. The Observer, on the other hand, is a pattern that's more about the way objects interact than about the way they're structured, and there are several ways to implement it.

Let's start by looking at the interactions the Observer pattern represents:

Basically, the Observer pattern is quite simple. One class, called the Observer, wants to know about changes in another class, the Subject, just as our restaurant customer wants to know about a change in the kitchen (the food's ready).

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_480_0.png)

This actually requires three different processes:

- 1. REGISTRATION
  The Observer tells the Subject that it's interested in the changes.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_480_1.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_480_2.png)

- 2. NOTIFICATION
  The Subject notifies all the Observers that the change has occurred.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_480_3.png)

- 3. UNREGISTRATION
  The Observer tells the Subject that it's no longer interested.

### 1

The Observer notifies the Subject of its interest.

Observer

Register

Subject

The Subject stores a reference to the Observer.

Store Reference

Container

### 2

Observer

Notify

Subject

The Subject retrieves the references to its Observers.

The Subject notifies its Observers.

Retrieve References

Container

### 3

The Observer notifies the Subject that it is no longer interested.

Observer

Unregister

Subject

The Subject removes the reference to the Observer

Remove Reference

Container

## OBSERVER OPTIONS

There are three standard ways to implement the Observer pattern. Don't worry about how they're implemented; .NET has a built-in solution, which we'll look at in a page or two.

### THE OBVIOUS SOLUTION

The most obvious way to solve the problem is to store a collection of observers in the subject.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_482_0.png)

### THE CLASSIC SOLUTION

The classic solution described by the Gang of Four de-couples the subject from the observer by using an interface and having all subjects derive from a base class.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_482_1.png)

### THE MODIFIED SOLUTION

The Modified Observer pattern is most often used in languages (like C#) that only support single inheritance.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_483_0.png)

### PUT ON YOUR THINKING HAT

Each of these solutions has some problems. Can you figure out what they are?

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_484_0.png)

### HOW'D YOU DO?

This was a hard one. Don't feel bad if you missed some of the problems. I probably missed some, too.

### THE OBVIOUS SOLUTION

The basic problem here is that the classes are too tightly coupled.

- Only instances of ObviousObserver can be notified.
- Any instance that cares about one change will be notified of all changes.
- It isn't possible to reuse one class without including the other.

### THE CLASSIC SOLUTION

The classic solution solves the problem of requiring that the observer be of a specific type, but it has problems of its own.

- All subjects need to descend from ClassicSubjectBase. That complicates the class hierarchy when only single inheritance is supported.
- Any instance that cares about one change will be notified of all changes.
- The code to implement this solution is complicated, and it's rarely obvious how it works. That makes the classes hard to understand (and therefore, to maintain.)

### THE MODIFIED SOLUTION

The Modified Observer pattern is most often used in languages (like C#) that only support single inheritance. It solves most of the problems in the obvious solution, but some remain.

- The pattern has moved from the two simple classes in the obvious solution to three classes and two interfaces. That's a lot of complexity.
- The code is still fairly complicated and hard to understand, and there's more of it (although the interfaces and SubjectHelper class only need to be written once.)

## THE .NET SOLUTION

The Modified Observer pattern solves the major problems posed by the Observer, but it's complicated and can be tricky to implement. Fortunately, .NET (along with some other development platforms) implements some constructs that make implementation quite straightforward. Let's see how the .NET solution maps to our original example:

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_485_0.png)

The events declared by classes are like the menu items offered by our restaurant.

A delegate acts as the intermediary between the subject and observer, just like the waiter in our example.

In .NET, any class can be an observer, and unlike our restaurant example, shoes and shirts aren't required.

```
NetSubject
Class
Events
SomeEvent: NetDelegate
```

```
NetDelegate
Class
```

```
NetObserver
Class
Methods
SomeEventHandler(): NetDelegate
```

A .NET event corresponds to the SubjectHelper class in the Modified Observer pattern, but there's no code to write!

A delegate is very different from the IObserver interface in the Modified Observer pattern, but it fulfills the same role—it defines the type that can respond to an event. The major functional difference is that a delegate works on a method-by-method basis, while the interface works on a class-by-class basis.

Because a delegate defines only a method signature, any class that exposes a method with the correct signature can respond to an event.

## EVENT OBJECTS

Defining an event is a whole lot easier than implementing any of the Observer patterns directly, but it does require four things.

### AN ARGUMENT CLASS

The second argument passed to an event handler is an instance of System.EventArgs or a class that descends from it. EventArgs itself doesn't pass any information, but the Framework defines dozens of classes that derive from it (everything from AccessKeyEventArgs to XsltMessageEncounteredEventArgs), so if you want to pass some information, you might be able to use one of them, or you can define your own class that inherits System.EventArgs. By convention, the argument class should be named <EventName>EventArgs.

### AN EVENT DELEGATE

If you're using an EventArgs class that's defined by the Framework, there will be a delegate defined for it as well. The handler will be named <EventNameHandler>, and you should follow the same convention when you create a delegate for a new argument type.

The delegate defines the signature of methods that can respond to the event. All delegates have the same basic pattern: they are declared as public, return void, and have two arguments. The first argument is an Object named sender, and represents the instance that is raising the event. The second argument is named e, and represents an instance of the appropriate event argument class.

### AN EVENT DECLARATION

Of course, you need to declare the event so the CLR knows about it. The syntax is simple:

```
. public event <DelegateType> <EventName>;
```

### A METHOD TO RAISE THE EVENT

Finally, you need a method that will actually raise the event. In C#, the syntax to raise an event looks like a method call, and by convention the event-raising method is named On<EventName>, is protected, and takes the event arguments as a parameter, so the basic pattern looks like this:

```
protected void On<EventName>(<EventName>Args e)
{
. <EventName>(this, e);
}
```

## HANDLING EVENTS

We've written quite a few event handlers in this book, but we've always used the WPF Designer to declare them. So here's what you need to do to handle a standard CLR event in C#:

### CREATE THE HANDLER METHOD

The method must have the same signature as the delegate for the event, and by convention use the name <EventName>Handler:

```
public void <EventName>Handler
{
    //do something
}
```

### CREATE AN INSTANCE OF THE EVENT DELEGATE

The constructor for a delegate takes the method name as its only parameter. The delegate can be named anything you like, of course it's just a variable:

```
<DelegateType> <myDelegate> = new <DelegateType>(<HandlerMethod>);
```

That's a lot of placeholders, isn't it? Here's a concrete example:

```
EventHandler myDelegate = new EventHandler(MyEventHandler);
```

### REGISTER THE DELEGATE WITH AN INSTANCE OF THE CLASS

You can use the C# += operator to do this. Here's a concrete example:

```
MyClass myInstance = new MyClass();
myInstance.MyEvent += myDelegate;
```

### PUT ON YOUR THINKING HAT

You wouldn't ordinarily handle an event in the same class that raises it, but let's do it just to get some experience writing events and handlers. You can declare the event (use the base EventArgs argument type) and the handler (have it display a MessageBox) in the MainWindow class, and then call the event-raising method from inside a Button_Click event handler.
