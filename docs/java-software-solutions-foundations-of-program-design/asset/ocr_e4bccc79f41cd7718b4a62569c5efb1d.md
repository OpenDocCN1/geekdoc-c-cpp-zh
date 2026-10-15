# LISTING 9.7 continued
OUTPUT

```
I feel like I'm diagonally parked in a parallel universe.

Warning: Dates in calendar are closer than they appear.

I feel like I'm diagonally parked in a parallel universe.
```

Both the Thought class (see Listing 9.8) and the Advice class (see Listing 9.9) contain a definition for a method called message. The version of message defined in the Thought class is inherited by Advice, but Advice overrides it with an alternative version. The new version of the method prints out an entirely different message and then invokes the parent’s version of the message method using the super reference.

The object that is used to invoke a method determines which version of the method is actually executed. When message is invoked using the parked object in

# LISTING 9.8

```
//****************************************************************
// Thought.java      Author: Lewis/Loftus
//
// Represents a stray thought. Used as the parent of a derived
// class to demonstrate the use of an overridden method.
//****************************************************************

public class Thought
{
    //-------------------------------------------------------------
    // Prints a message.
    //-------------------------------------------------------------
    public void message()
    {
        System.out.println ("I feel like I'm diagonally parked in a " +
                            "parallel universe.");

        System.out.println();
    }
}
```