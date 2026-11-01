```
// utility method to see if cards are in a run
// (same suit assumed)
private bool IsSequential(Cards cards)
{
    int maxVal, minVal;
    GetLimits(cards, out maxVal, out minVal);
    if ((maxVal - minVal) == (cards.Count - 1))
    {
        return true;
    }
    else
    {
        return false;
    }
}
```

# Exercise 3

In order to use an object initializer with a class, you must include a default, parameter-less constructor. You could either add one to this class or remove the nondefault constructor that is there already. Once you have done this, you can use the following code to instantiate and initialize this class in one step:

```
Giraffe myPetGiraffe = new Giraffe
{
    NeckLength = "3.14",
    Name = "Gerald"
};
```

# Exercise 4

False. When you use the var keyword to declare a variable, the variable is still strongly typed; the compiler determines the type of the variable.

# Exercise 5

You can use the Equals() method that is implemented for you. Note that you cannot use the == operator to do this, as this compares variables to determine if they both refer to the same object.

# Exercise 6

The extension method must be static:

```
public static string ToAcronym(this string inputString)
```

# Exercise 7

You must include the extension method in a static class that is accessible from the namespace that contains your client code. You could do this either by including the code in the same namespace or by importing the namespace containing the class.