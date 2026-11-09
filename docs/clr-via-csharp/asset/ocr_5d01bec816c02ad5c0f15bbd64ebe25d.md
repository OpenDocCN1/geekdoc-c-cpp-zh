Because the C# compiler has built-in support for events, the compiler translates the use of the `+=` operator into the following line of code to add the object's interest in the event:

```
```csharp
mm.add_NewMail(new EventHandler<NewMailEventArgs>(this.FaxMsg));
```
```

As you can see, the C# compiler is generating code that will construct an `EventHandler<NewMailEventArgs>` delegate object that wraps the `Fax` class's `FaxMsg` method. Then, the C# compiler calls the `MailManager`'s `add_NewMail` method, passing it the new delegate. Of course, you can verify all of this by compiling the code and looking at the IL with a tool such as `ILDasm.exe`.

Even if you're using a programming language that doesn't directly support events, you can still register a delegate with the event by calling the `add` accessor method explicitly. The effect is identical; the source code will just not look as pretty. It's the `add` method that registers the delegate with the event by adding it to the event's list of delegates.

When the `MailManager` object raises the event, the `Fax` object's `FaxMsg` method gets called. The method is passed a reference to the `MailManager` object as the first parameter, `sender`. Most of the time, this parameter is ignored, but it can be used if the `Fax` object wants to access members of the `MailManager` object in response to the event notification. The second parameter is a reference to a `NewMailEventArgs` object. This object contains any additional information the designer of `MailManager` and `NewMailEventArgs` thought would be useful to the event receivers.

From the `NewMailEventArgs` object, the `FaxMsg` method has easy access to the message's sender, the message's recipient, and the message's subject. In a real `Fax` object, this information would be faxed somewhere. In this example, the information is simply displayed in the console window.

When an object is no longer interested in receiving event notifications, it should unregister its interest. For example, the `Fax` object would unregister its interest in the `NewMail` event if the user no longer wanted his or her e-mail forwarded to a fax. As long as an object has registered one of its methods with an event, the object can't be garbage collected. If your type implements `IDisposable`'s `Dispose` method, the implementation should cause it to unregister interest in all events. (See Chapter 21, "Automatic Memory Management (Garbage Collection)," for more information about `IDisposable`.)

Code that demonstrates how to unregister for an event is shown in `Fax`'s `Unregister` method. This method is practically identical to the code shown in the `Fax` constructor. The only difference is that this code uses `-=` instead of `+=`. When the C# compiler sees code using the `-=` operator to unregister a delegate with an event, the compiler emits a call to the event's `remove` method:

```
```csharp
mm.remove_NewMail(new EventHandler<NewMailEventArgs>(FaxMsg));
```
```