```
BroadCast(killer.Name + " killed " + target.Name +
"! OH NOEZ!!1ONE");
}

static void BroadCast(string msg)
{
    // ordinarily there would be network code here
    // to broadcast to the entire game

    Debug.WriteLine("[Game]: " + msg);
}

public static event OnGameStartedDelegate OnGameStarted;
public static event OnGameFinishedDelegate OnGameFinished;
public static event OnGamePausedDelegate OnGamePaused;
public static event Action<DateTime> OnGameResumed;
}
}
```

At this point, the code in Listing 4.3 should look pretty straightforward. There are new methods on the game engine that will trigger various events such as Start, Stop, Pause, and Resume. At the end of the listing you can see where I’ve declared the four new events.

If you have been looking closely, you’ll notice something a little different about the way I’ve declared the OnGameResumed event. I didn’t use a strongly typed delegate that was declared at the top of the namespace like I did in previous listings. Instead I made use of a few shorthand features in C# like Generics and the generic type called Action<T>.

Generics allow classes to be associated with a particular type by the code creating the instance, rather than by the class itself. For example, rather than creating a list of objects that can be any type by using an instance of the List class, I can create a list of combatants by creating an instance of List<Combatant>. Generics allow me to supply one or more type parameters to a class when instantiating it. If you want to know more about Generics and other low-level details of the C# language itself, you might want to pick up a copy of C# 4.0 Unleashed, by Bart De Smet.

The second change to the last event declaration is the use of Action<DateTime>. The Action<T> class is a generic class that provides a kind of shorthand for delegates that have a void return type. As you can see, writing Action<DateTime> once before the event declaration is much easier to read than creating a custom delegate type and then using that to declare the event. Anytime you see Action<T> you can translate that in your mind to “a void-returning delegate that takes a parameter of type T.” There are also variants of Action that take multiple parameters to accommodate more parameters in the event handler.