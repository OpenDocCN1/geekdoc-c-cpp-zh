```
public class Robozilla  // Doesn't implement IPet!
{
    public void ClimbStairs();                 // Safe
    public void PetTheRobodog();               // Safe? Might break it.
    public void Charge();                      // Maybe not safe
    public void SearchAndDestroy();            // Dangerous
    public void LaunchGlobalThermonuclearWar(); // Catastrophic
}
```

You want to expose only the two safer methods while hiding the last three dangerous ones. Here’s how you can do that by using a C# interface:

+   1. Design a C# interface that exposes only the safe methods:

```
public interface IRobozillaSafe
{
    void ClimbStairs();
    void PetTheRobodog();
}
```

+   2. Modify the Robozilla class to implement the interface. Because it already has implementations for the required methods, all you need is the : IRobozillaSafe notation on the class heading:

```
public class Robozilla : IRobozillaSafe ...
```

Now you can just keep Robozilla itself a secret from, say, everybody except Gandhi, Martin Luther King, and Mother Theresa and give most users the IRobozillaSafe interface. Give your clients a way to instantiate a new Robozilla, but return to them a reference to the interface (in this example, by using a static factory method added to class Robozilla):

```
// Creates a Robozilla but returns only an interface reference to it.
public static IRobozillaSafe CreateRobozilla(<parameter list>)
{
    return (IRobozillaSafe)new Robozilla(<parameter list>);
}
```

Clients then use Robozilla like this:

```
IRobozillaSafe myZilla = Robozilla.CreateRobozilla(...);
myZilla.ClimbStairs();
myZilla.PetTheRobodog();
```

It’s that simple. Using the interface, they can call the Robozilla methods that it specifies — but not any other Robozilla methods.

Programmers (I think I can guess which ones) can defeat my little ploy with a simple cast:

```
Robozilla myKillaZilla = (Robozilla)myZilla;
```

![](bbox=[0.13, 0.79, 0.22, 0.9])