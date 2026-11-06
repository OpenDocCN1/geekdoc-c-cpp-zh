
![](img/6ba99460b0feb3585671a4612ff5fabb_273_0.png)

The cash amount, therefore, would be a *private* or *protected* member variable. It would be hidden from the other functions and classes. As for which it would be, private or protected, that depends on whether we expect to derive new classes from the cash register class and whether we want these new classes to have access to the members. In the situation of a cash register, we would probably not want other parts of the application to access the cash register if we’re worried about security. But on the other hand, if we think that we’ll be creating derived classes that have added features involving the cash (such as automatically sending the money to a bank via an electronic transaction), we would want the members to be protected. (In general, we choose protected, rather than private, because they have been bitten too many times by using classes that have a gazillion private members. In those cases, we’re unable to derive useful classes because everything is private!)

Encapsulation, then, is this: You combine the methods and member variables into a single entity, hiding some of them and making some accessible. The accessible ones together make up the *interface* of the object. And finally (this is important!), when you create an object, you create one that can perform on its own. In other words, the users of the class tell it what to do (such as perform a sales transaction) by calling its member functions and supplying parameters, and the object does the work. The *calling function* doesn’t care how the object does its thing, just that it can do it. For example, a cash register class knows how to perform a sales transaction. As the designer of the class, don’t force users to first call Sale and then call separate functions to manually modify the amount of cash in the register and modify the running total. Rather, the Sale function does all the hard work, and users of the class don’t have to worry about how that work takes place.

And now the fundamental question: Why do you need to know the word encapsulation? Because it’s a common term that computer scientists like to throw around. If they use it, however, they are likely to use it as a verb: “Look at me! I am going to encapsulate this information into an object!”

But the process matters more than the word itself. When you design objects and classes, you encapsulate your information into individual objects. If you keep the process in mind, you will be better off. Here are the things you need to do every time you design a class:

- **Encapsulate the information.** Combine the information into a single entity that becomes the class. This single entity has member variables representing its characteristics and member functions representing its capabilities.
- **Clearly define the public interface of the class.** Provide a set of functions that are public (and, possibly, member variables that are public, although it’s best to keep them protected or private), and make the rest of the members either protected or private.
- **Write the class so that it knows how to do its own work.** The class’s users should need only to call the functions in the public interface, and these public functions should be simple to use.

Note that the Weight member is protected and SetWeight() is public. Thus, the users of the class can’t modify the Weight member directly; they can only call SetWeight() to set it, which provides built-in checking. Now, this works all fine and dandy, except when the users of the class need to find Fido’s weight to make sure that he’s not rapidly shrinking. The only problem is that Weight is protected, so the user can’t read it. So you need to add a function that retrieves the value of Weight, as in the following:

```cpp
int Dog::GetWeight()
{
    return Weight;
}
```

You must modify the class to accommodate this function:

```cpp
class Dog
{
protected:
    int Weight;

public:
    void SetWeight(int NewWeight);
    int GetWeight();
};
```

Now when you use this class, instead of accessing the Weight variable directly, you use the access methods, as in the following sample lines:

```cpp
int main()
{
    Dog fido;
    fido.SetWeight(10);
    cout << fido.GetWeight() << endl;
    fido.SetWeight(-5);
    cout << fido.GetWeight() << endl;
    return 0;
}
```

To set the weight, you call SetWeight(). Note that in the first call to SetWeight(), we’re passing a legitimate value, 10. And when the next line runs, we see the number 10 appear on the console. But in the second call to SetWeight(), we’re passing an invalid weight, -5. The SetWeight() function rejects this value and doesn’t change the weight. So the second time we write the weight by calling GetWeight(), we still see 10. The number did not change. The -5 value was rejected, and the weight remained the same.

When you use access functions, you can do much more than just guard against invalid values and return the current value. The set() function, for example, can process the value and make calculations or modify it. For example, the Dog class might have a maximum weight. If the user passes a larger weight to the SetWeight() function, the function could change it to the maximum weight. For example, the following function limits the weight to an upper level of 100 and a lower level of 1:

```cpp
void Dog::SetWeight(int NewWeight)
{
    if (NewWeight < 0)
    {
        Weight = 0;
    }
    else if (NewWeight > 100)
    {
        Weight = 100;
    }
    else
    {
        Weight = NewWeight;
    }
}
```

You can use a Get() function to send a modified form of a member variable. For example, if you have a SalesTransaction class that contains a CreditCardNumber variable, which is a string containing the digits and the spaces, you may want to reveal only the last four digits instead of the entire number. A Get() function, then, might retrieve the CreditCardNumber, extract only the final four digits, and build a string of the form “XXXX XXXX XXXX 1234.” It would then return that string rather than the actual CreditCardNumber value.

![](img/6ba99460b0feb3585671a4612ff5fabb_276_0.png)

## Access methods versus properties

Many modern languages support a third aspect to classes, called properties, in addition to the usual member methods and member variables. C++ doesn't support a named entity called properties, but it does support the equivalent methodology. In your programming career, you're likely to move between lots of different languages. And so we want to take a moment to introduce you to properties, which are found in languages such as C#, VB.NET, and Object Pascal. Properties are essentially a combination of member variables and methods. Think of a public member variable in C++. Anyone using an object can freely modify a member variable. But sometimes when you're creating a class, you want to place restrictions on what people can do with the member variables. For example, you might want to limit the access to reading the member variable but not changing it. Or you might want to restrict what values the variable can take on, such as limiting the variable to integers between 1 and 100 and not allowing it to contain any other integers.

In C++, the way to impose such limitations is to make the member variable private and then write two member methods: one for reading the value of the variable and one for setting the value. The method that sets the value would impose the limits; if the caller tries to set the value to 101, for example, the method might automatically knock the value down to 100, if that's the limit you're imposing. And similarly, if you want people to be able to read the value but not change it, you might provide only a method that returns the value, and not a method for modifying the variable.

These two methods — one for setting a member variable and one for “getting” (that is, reading) a member variable — are accessor methods. Some languages other than C++ let you combine these member methods into what

Book II Chapter 1 Planning and Building Objects
