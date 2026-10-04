**Important** Without doubt, it doesn't take much for programmers to start abusing C#'s lambda expression feature. When I first started using lambdas, it instinctively took me some time to get used to them. After all, the code you write in a method is not actually inside that method, and this can also make debugging and single-stepping through the code a bit more challenging. In fact, I'm amazed at how well the Microsoft Studio debugger actually handles stepping through lambda expressions in my source code.

I set up a rule for myself: If I need my callback method to contain more than three lines of code, I will not use a lambda expression; instead, I'll write the method manually and sign it a name of my own. But, used judiciously, lambda expressions can greatly increase programmer productivity as well as the maintainability of your code. The following is some code in using lambda expressions feels very natural. Without it, the code would be tedious, harder to read, and harder to maintain.

```
// Create and initialize a String array
String[] names = { "Jeff", "Kristin", "Aidan", "Grant" };

// Get the names that have a lowercase 'a' in them
charToFind = 'a';
names = Array.FindAll(names, name => name.IndexOf(charToFind) >= 0);

// Convert each string's characters to uppercase
names = Array.ConvertAll(names, name => name.ToUpper());

// Display the results
Array.ForEach(names, Console.WriteLine());
```

# Delegates and Reflection

So far in this chapter, the use of delegates has required the developer to know up front the prototype of the method that is to be called. For example, if fb is a variable that references a Feedback delegate (see this first program listing), to invoke the delegate, the code would look like the following.

```
fb(item); // item is defined as Int32
```

As you can see, the developer must know when coding how many parameters the callback method requires and the types of those parameters. Fortunately, the developer almost always has this information, so writing like the preceding code isn't a problem.

In rare circumstances, however, the developer doesn't have this information at compile time. I showed an example of this in Chapter 11, "Events," when I discussed the HashSet. In this example, a dictionary maintained a set of different delegate types. At runtime, to raise an event, one of the delegates was looked up in the dictionary and invoked. At compile time, it wasn't possible to know exactly which delegate would be called and which parameters were necessary to pass to the delegate's callback method.