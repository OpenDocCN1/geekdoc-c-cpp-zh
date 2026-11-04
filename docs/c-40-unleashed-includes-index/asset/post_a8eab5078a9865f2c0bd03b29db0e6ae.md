
Because you need the reference to handlers to refer to its OnShutDown method, this can be done only as long as a reference to handlers exists. The line that removes the event handler creates a new delegate instance referring to OnShutDown on handlers, which is located in the multicast delegate's invocation list by the Delegate.Remove method. In short, don't forget to unhook your event handlers.

If all this scares you to death, don't worry too much. Although this problem exists (as our example proves), it's not all that common. The crux of the sketched problem is that we're handling the events on a separate object that does not own the objects that raise the events. In our case, we're even using a static event to construct a bad scenario. Why does "ownership" of event sources matter? Well, consider the case of a Windows Forms form shown here:

```csharp
class LoginForm : Form {
    private Button login;

    public LoginForm() {
        login = new Button { Text = "Log in" };
        login.Click += login_Click;
    }

    private void login_Click(object sender, EventArgs e) { /* TODO */ }
}
```

Here, the form instance owns the login button object. The form attaches an event handler for the button's Click event, with the handler located on the form instance itself. In fact, the third line of the constructor could be read as follows:

```csharp
login.Click += this.login_Click;
```

So the "event sink" with the event handlers (the form) is the same as the owner of the event source (the button). As soon as the form object becomes unreachable, so do all of its controls and their event handlers. As shown in Figure 18.12, this makes it possible to reclaim the form and its controls. On the other hand, the earlier example (shown at the bottom of Figure 18.12) poses a problem, as explained earlier.

## USING SOS TO TRACE LEAKS

The .NET Framework comes with a low-level debugger extension called SOS (for "Son of Strike") that can be loaded inside Visual Studio for advanced debugging. One of the many things it can help with is locating the source of memory leaks.

A sample session debugging our memory leak is shown in Figure 18.13. On the first line, the SOS extension is loaded from the folder where the .NET Framework lives.

Assuming we somehow already know that a Handlers instance is being leaked, we issue the command !dumpheap to search the managed heap for objects of the specified type. We find exactly one instance of the type and wonder what keeps it alive. Given its reported address, !GCRoot does the trick.

The GCRoot command traces the path of references that keeps the object alive (that is, proves how it can still be reached by code). For our suspect Handlers object, traces look like System.Action -> Handlers. (Read the arrow as "references.")

From this, we clearly see that an Action delegate still refers to the Handlers object. In some cases, this is enough of a clue to start looking for places where the event handlers should be removed but aren't. If more information is needed, you could dump the Action delegate to see what its target method is and so forth.

Search the Web for terms GCRoot, SOS, and event to learn more about the use of SOS to debug object leaks like the one shown here.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_885_0.png)

## FIGURE 18.12 Ownership of event source objects can help a lot for event handler use.

Because this problem has been known as one of the main sources of memory issues in .NET applications, WPF added the pattern of “weak events.” We won’t elaborate on this right here, but when using WPF you may want to research this in more depth on MSDN.

Unhooking event handlers looks like a pretty straightforward business, simply using the -= operator. Although this is true, a caveat exists due to the introduction of anonymous function expressions in C# 2.0 and lambda expressions in C# 3.0. Earlier on, we’ve seen code like this:

![](img/a16f85e62ce9bdc527f4b09dbfe26092_886_0.png)

## FIGURE 18.13 Analyzing a memory leak with SOS.

```csharp
var countDown = new CountDown(5);

// Hook up event handlers, using lambda expressions
countDown.Tick += currentSecond => Console.WriteLine(currentSecond);
countDown.Finished += () => Console.Beep();

countDown.Start();
```

In the light of our discussion about event handlers, we might want to unhook the Tick and Finished event handlers as a matter of following best practices. The first question to ask is when it's appropriate to do so. Clearly, we shouldn't unhook while the events can still be raised, but we know not to expect further events after the Finished event has been raised (though such a “protocol” should really be documented by the provider of the CountDown type). This makes the code inside the Finished event handler a good place to unhook the Tick event handler as well as itself. Now the more pressing question is how to accomplish this.

To answer this accurately, let's first take a step back. Because we know that events are nothing but multicast delegates in disguise, we can use a plain multicast delegate as a petri dish for some experimentation. Take a look at the following fragment of code, where we use handy lambda expression syntax to make things concise:

```
Action evt = null;
evt += () => Console.WriteLine("Hello");
if (evt != null)
    evt();
evt -= () => Console.WriteLine("Hello");
if (evt != null)
    evt();
```

Pop quiz: How many times does it print Hello? If you say once, think twice; the answer is two times. Although it looks like we're adding and removing the same event handler on lines two and four, those are not the same object. Recall what anonymous functions compile into under the hood: compiler-generated methods containing the code specified in the anonymous function expression:

```
Action evt = null;
evt += new Action(__AnonymousMethod1);
if (evt != null)
    evt();
evt -= new Action(__AnonymousMethod2);
if (evt != null)
    evt();
```

Two anonymous function expressions result in two distinct methods being cooked up by the compiler, even though they have the same code inside them. The compiler could be smarter about this, detecting “semantically identical” anonymous function expressions and sharing the same object for them. However, this is a pretty tricky thing to implement, and the compiler writers thought there were more important matters to tackle.

Because we have two distinct methods used when adding and removing delegates, the += and -= operations do not cancel each other out. The way to fix this issue is to use an intermediate variable:

```
Action evt = null;
Action handler = () => Console.WriteLine("Hello");
evt += handler;
if (evt != null)
    evt();
evt -= handler;
if (evt != null)
    evt();
```

To be able to unhook our CountDown event handlers, we have to lift them into a local variable, as just shown:

```csharp
var countDown = new CountDown(5);

// Hook up event handlers
Action<uint> tickHandler = currentSecond => Console.WriteLine(currentSecond);
Action finishedHandler = () => {
    Console.Beep();

    // Finished has been called: we can unhook both Tick and Finished now.
    countDown.Tick -= tickHandler;
    countDown.Finished -= finishedHandler;
};

countDown.Tick += tickHandler;
countDown.Finished += finishedHandler;

countDown.Start();
```

The preceding code is almost right; it just doesn't compile yet. Conceptually, everything looks right, though: We create handler delegates of type Action first and hook them up using regular += syntax later. Inside the event handler for Finished, we can unhook those again based on our knowledge of the event protocol of CountDown.

The remaining issue (that prevents us from compiling the preceding code) is rather subtle. Take a closer look at the finishedHandler lambda expression. While we're defining it, we're using it inside its own body on the last line. In more technical terms, we're defining a recursive lambda expression, which is something the language doesn't permit in this syntactical form, as illustrated in Figure 18.14.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_888_0.png)

## FIGURE 18.14 Recursive lambda expressions make the compiler unhappy.
