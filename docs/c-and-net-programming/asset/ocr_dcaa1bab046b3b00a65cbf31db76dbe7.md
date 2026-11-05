```
{
if(System.Text.RegularExpressions.Regex.IsMatch(s,"Python"))
{
Console.WriteLine("Match found");
}
}
```

The above example searches for "Python" against the set of inputs from the languages array. It uses Regex.IsMatch which returns true in case if the pattern is found in the input. The pattern can be any regular expression representing the input that we want to match.

# Q.4 What are Events ?

Ans.: Events are user actions that generate notifications to the application to which it must respond. The user actions can be mouse movements, keypress and so on.

Programmatically, a class that raises an event is called a publisher and a class which responds/receives the event is called a subscriber. Event should have at least one subscriber else that event is never raised.

Delegates are used to declare Events.

```
Public delegate void PrintNumbers();
Event PrintNumbers myEvent;
```

# Q.5 What are the different types of Delegates ?

Ans.: Different types of Delegates are :

Single Delegate : A delegate that can call a single method.

Multicast Delegate : A delegate that can call multiple methods. + and - operators are used to subscribe and unsubscribe respectively.

Generic Delegate : It does not require an instance of the delegate to be defined. It is of three types, Action, Funcs and Predicate.

Action : In the above example of delegates and events, we can replace the definition of delegate and event using Action keyword. The Action delegate defines a method that can be called on arguments but does not return a result

```
Public delegate void deathInfo();
Public event deathInfo deathDate;
//Replacing with Action//
Public event Action deathDate;
```