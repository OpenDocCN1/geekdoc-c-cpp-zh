# # HANDLING EVENTS

We've written quite a few event handlers in this book, but we've always used the WPF Designer to declare them. So here's what you need to do to handle a standard CLR event in C#:

# ## CREATE THE HANDLER METHOD

The method must have the same signature as the delegate for the event, and by convention use the name <EventName>Handler:

```
public void <EventName>Handler
{
    //do something
}
```

# ## CREATE AN INSTANCE OF THE EVENT DELEGATE

The constructor for a delegate takes the method name as its only parameter. The delegate can be named anything you like, of course it's just a variable:

```
<DelegateType> <myDelegate> = new <DelegateType>(<HandlerMethod>);
```

That's a lot of placeholders, isn't it? Here's a concrete example:

```
EventHandler myDelegate = new EventHandler(MyEventHandler);
```

# ## REGISTER THE DELEGATE WITH AN INSTANCE OF THE CLASS

You can use the C# += operator to do this. Here's a concrete example:

```
MyClass myInstance = new MyClass();
myInstance.MyEvent += myDelegate;
```

# ### PUT ON YOUR THINKING HAT

You wouldn't ordinarily handle an event in the same class that raises it, but let's do it just to get some experience writing events and handlers. You can declare the event (use the base EventArgs argument type) and the handler (have it display a MessageBox) in the MainWindow class, and then call the event-raising method from inside a Button_Click event handler.