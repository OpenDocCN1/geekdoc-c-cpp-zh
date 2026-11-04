![](bbox=[0.06, 0.06, 0.5, 0.33])

FIGURE 17.27 MulticastDelegate objects keep a list of Delegate objects inside.

If a Delegate object can refer to one method and a MulticastDelegate contains an array (known as the *invocation list*) of Delegate objects, it's clear that a MulticastDelegate can refer to multiple methods. Hence, the invocation of such a delegate multicasts the arguments passed in to all methods in the invocation list.

So far, we've always created delegates that point at one method at a time. For example, the following defines three Action<string> delegates based on a lambda expression:

```
```csharp
Action<string> sayHiEnglish = name => Console.WriteLine("Hello " + name);
Action<string> sayHiDutch   = name => Console.WriteLine("Hallo " + name);
Action<string> sayHiFrench  = name => Console.WriteLine("Allo " + name);
```
```

What if we're given a name and want to call all the above to greet the incoming user in a bunch of languages? Different approaches exist. Obviously, we could invoke all three delegates one by one:

```
```csharp
sayHiEnglish(name);
sayHiDutch(name);
sayHiFrench(name);
```
```

Code starts to get bloated if subsequently we're asked to add another language to the mix, requiring us to revisit the invocation site of those delegates. Furthermore, it might even be the case we provide a means for the users of our greeting system to plug in other delegates for different languages that we didn't anticipate. Now we can no longer have a fixed number of delegate invocations in our code.