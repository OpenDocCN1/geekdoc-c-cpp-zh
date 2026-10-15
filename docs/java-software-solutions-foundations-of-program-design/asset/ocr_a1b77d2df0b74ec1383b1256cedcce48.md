We mentioned that an enumerated type is a special kind of class, and that the values of the enumerated type are objects. The values are, in fact, instances of its own enumerated type. For example, winter is an object of the Season class. Let’s explore this concept a bit further.

Suppose we declare a variable of the Season type as follows:

```
Season time;
```

KEY CONCEPT
The values of an enumerated type are static variables of that type.

Because an enumerated type is a special kind of class, the variable time is an object reference variable. Furthermore, as an enumerated type, it can be assigned only the values listed in the Season definition. These values (winter, spring, summer, and fall) are actually references to Season objects that are stored as public static variables within the Season class. Thus we can make an assignment such as the following:

```
time = Season.spring;
```

Now let’s take this idea a step further. In Listing 7.11 we redefine the Season type, giving it a more substantial definition. Note that we still use the enum reserved word to declare the enumerated type, and we still list all possible values of the type. In addition, in this definition we add a private String called span, a constructor for the Season class, and a method named getSpan. Each value in the list of values for the enumerated type invokes the constructor, passing it a character string that is then stored in the span variable of each value.

# LISTING 7.11

```
//****************************************************************
// Season.java      Author: Lewis/Loftus
//
// Enumerates the values for Season.
//****************************************************************

public enum Season
{
    winter ("December through February"),
    spring ("March through May"),
    summer ("June through August"),
    fall ("September through November");

    private String span;
```