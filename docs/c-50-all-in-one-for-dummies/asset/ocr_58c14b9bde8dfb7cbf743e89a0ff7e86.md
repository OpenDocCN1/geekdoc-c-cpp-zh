# Revising Generics

The generics model implemented in C# 2.0 was incomplete. Generics are fine for making the programmer’s life easier, but they did little in that version to make the analyst’s life easier. It used to be very hard to model an actual business model using Generics, and that changed in C# 4.0. Although parameters in C# 2.0 all allowed for variance in several directions, generics did not.

Variance has to do with types of parameters and return values. Covariance means that an instance of a subclass can be used when an instance of a parent class is expected, while Contravariance means that an instance of a superclass can be used when an instance of a subclass is expected. When neither is possible, it is called Invariance.

All fourth-generation languages support some kind of variance. In C# 3.0 and earlier versions, parameters are covariant, and return types are contravariant. So, this works because string and integer parameters are covariant to object parameters:

```
public static void MessageToYou(object theMessage)
{
    if (theMessage != null)
        Console.WriteLine(theMessage)
}
//then:
MessageToYou("It's a message, yay!");
MessageToYou(4+6.6);
```

And this works because object return types are contravariant to string and integer return types (for example):

```
object theMessage = MethodThatGetsTheMessage();
```

Generics are nonvariant in C# 2.0 and 3.0. This means that if Basket<apple> is of type Basket<fruit>, those Baskets are not interchangeable like strings and objects are in the preceding example.

# Variance

If you look at a method like the following one:

```
public static void WriteMessages()
{
    List<string> someMessages = new List<string>();
    someMessages.Add("The first message");
    someMessages.Add("The second message");
    MessagesToYou(someMessages);
}
```

and then you try to call that method like you did earlier in this chapter with a string type