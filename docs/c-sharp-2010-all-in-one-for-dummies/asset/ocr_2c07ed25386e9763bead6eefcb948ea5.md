The code looks like the delegate instantiations I describe, except that after the = sign, you see the delegate keyword, any parameters to the anonymous method in parentheses (or empty parentheses if none), and the method body. The code that used to be in a separate DoUpdate() method — the method that the delegate "points to" — has moved inside the anonymous method — no more pointing. And this method is utterly nameless.

You still need the UpdateProgressCallback delegate type definition, and you're still invoking a delegate instance, named anon in this example.

![](bbox=[0.03, 0.3, 0.14, 0.37])

Needless to say, this description doesn't cover everything there is to know about anonymous methods, but it's a start. Look up the term anonymous method in Help to see more anonymous method examples in the DelegateExamples program on the Web site. My parting advice is to keep your anonymous methods short.

# ## Stuff Happens — C# Events

One more application of delegates deserves discussion in this section: the C# event, which is implemented with delegates. An event is a variation on a callback but provides a simpler mechanism for alerting "interested observers" whenever an important event occurs. An event is especially useful when more than one anxious relative is waiting for a callback. Events are widely used in C#, especially for connecting the objects in the user interface to the code that makes them work. The buttons in the SimpleProgress example, presented earlier in this chapter, illustrate this use.

# ### The Observer design pattern

It's extremely common in programming for various objects in the running program — those anxious relatives I mentioned — to be "interested in" events that occur on other objects. For example, when the user clicks a button, the form that contains the button "wants" to know about it. Events provide the standard mechanism in C# and .NET for notifying any interested parties of important actions.

![](bbox=[0.03, 0.74, 0.14, 0.81])

The event pattern is so common that it has a name: the Observer design pattern. It's one of many common *design patterns* that people have published for anyone to use in their own code. To begin learning about other design *patterns*, you can consult *Design Patterns For Dummies*, by Steve Holzner.

The Observer pattern consists of an Observable object — the object with interesting events (sometimes called the Subject, though that confuses me) — and any number of Observer objects: those interested in a particular event. The observers register themselves with the Observable in some way