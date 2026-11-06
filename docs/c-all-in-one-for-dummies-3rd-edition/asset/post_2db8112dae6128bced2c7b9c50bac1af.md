
However, you can't go further than that. You can't take a pointer to a pointer to Creature. (*Remember:* When you say a "pointer to a pointer," the first pointer really means "the address of the second pointer variable." We need to phrase things like that, or our brains might explode in certain situations.)

So if you have a function such as this:

```cpp
void Feed(Creature *c)
{
    cout << "Feed me!" << endl;
}
```

you're free to pass the address of a Platypus object, as in the following:

```cpp
Platypus *plato = new Platypus;
Feed(plato);
```

with a function that takes the address of a pointer variable (note the two asterisks in the parameter), like this:

```cpp
void Eat(Creature **c)
{
    cout << "Feed me!" << endl;
}
```

You *cannot* pass the address of a pointer to a Platypus instance, as in this example:

```cpp
Platypus *plato = new Platypus;
Eat(&plato);
```

If you try to compile this code, you get a compiler error.

You don't always use polymorphism when you declare a variable. If you do, you would be declaring variables like this:

```cpp
Creature *plato = new Platypus;
```

The type plato is a pointer to Creature. But the object is a Platypus. You can do this because a pointer to a base class can point to an object of a derived class. But now the compiler thinks that plato is a pointer to a Creature instance, so you can't use plato to call a member function of Platypus — you can use plato to call only members of Creature. For example, if your two classes look like this:

```cpp
class Creature
{
public:
    void EatFood()
    {
        cout << "I'm eating!" << endl;
    }
};

class Platypus : public Creature
{
public:
    void SingLikeABird()
    {
        cout << "I'm siiiiiinging in the rain!" << endl;
    }
};
```

the following would not work:

```cpp
Creature *plato = new Platypus;
plato->SingLikeABird();
```

Although the first line would compile, the second wouldn’t. When the compiler gets to the second line, it thinks that `plato` is only an object of class type `Creature`. And `Creature` does not have a member called `SingLikeABird()`, so the compiler gets upset. You can fix the situation by casting like this:

```cpp
Creature *plato = new Platypus;
static_cast<Platypus *>(plato)->SingLikeABird();
```

If you want to save some work, start by declaring `plato` as type `Platypus` as shown here:

```cpp
Platypus *plato = new Platypus;
plato->SingLikeABird();
```

You may need to perform a cast at times. For example, you may have a variable that can hold an instance of an object or its derived object. Then you would have to use polymorphism, as in the following code:

```cpp
Creature *plato;
if (HasABeak == true)
{
    plato = new Platypus;
}
else
{
    plato = new Creature;
}
```

In this code, we have a pointer to `Creature`. In that pointer, we store the address of either a `Platypus` instance or a `Creature` instance, depending on what’s in the `HasABeak` variable.

But if you use an `if` statement like that, you shouldn't follow it with a call to `SingLikeABird()`, even if you cast it:

```cpp
static_cast<Platypus *>(plato)->SingLikeABird();
```

And now, when you use the Revealed class, the inherited member X is public (but X is still protected in the base class, Secret).

![](img/6ba99460b0feb3585671a4612ff5fabb_526_0.png)

If you want to make a protected member public in a derived class, don't just redeclare the member. If you do, you end up with two member variables of the same name within the class; and needless to say, that can be confusing! Take a look at the following two classes:

```cpp
class Secret
{
protected:
    int X;

public:
    void SetX()
    {
        X = 10;
    }

    void GetX()
    {
        cout << "Secret X is " << X << endl;
    }
};

class Revealed : public Secret
{
public:
    int X;
};
```

The Revealed class has two int X members! Suppose you try this code with it:

```cpp
Revealed me;
me.SetX();
me.X = 30;
me.GetX();
```

The first line declares the variable. The second line calls SetX(), which stores 10 in . . . which variable? The inherited X, because SetX() is part of the base class! The third line stores 30 in . . . which one? The new X declared in the derived class! So then GetX() is again part of the base class, but will it print 10 or 30? It will print 10!

Personally, having two member variables of the same name is downright confusing. (Fortunately, our brains didn't quite explode because we're still here, writing away.) We think that it would be best if the compiler didn't allow you to have two variables of the same name. But even though the compiler allows it, that doesn't mean you should do it; having two variables of the same name is a perfect way to increase the chances of bugs creeping into your application.

Now think about this: Suppose you have a class that has several public members, and when you derive a new class, you want all the public members to become *protected*, except for one. You can do this task in a couple of ways. You could adjust the access of all the members except for the one you want left public. Or if you have lots of members, you can take the opposite approach. Look at this code:

![](img/6ba99460b0feb3585671a4612ff5fabb_527_0.png)

```cpp
class Secret
{
public:
    int Code, Number, SkeletonKey, System, Magic;
};

class AddedSecurity : protected Secret
{
public:
    using Secret::Magic;
};
```

Notice what we did: We derived the class as protected, as you can see in the header line for the *AddedSecurity* class. That means all the inherited public members of *Secret* will be protected in the derived class. But then we promoted *Magic* back to public by adjusting its member access. Thus, after all is said and done, *Magic* is the only public member of *AddedSecurity*. All the rest are protected.

If you have a member that is private and you try to adjust its access to protected or public in a derived class, you quickly discover that the compiler won't let you do it. The reason is that the derived class *doesn't even know about the member* because the member is private. And because the derived class *doesn't know about the member*, you can't adjust its access.

![](img/6ba99460b0feb3585671a4612ff5fabb_527_1.png)

### Returning something different, virtually speaking

Two words that sound similar and have similar meanings but are, nevertheless, different are *overload* and *override*. Although both words appear in movies (“Danger, danger! The system is overloaded, so we need to override the built-in security”), they’re less glamorous in computer programming. But the real danger that results in an overloading of your brain is in confusing the two words where one meaning overrides the other. Whew!

So first, let us clarify: To *override* means to take an existing function in a base class and give the function new code in a derived class. The function in the derived class has the same prototype as the base class: It takes the same parameters and returns the same type.

To *overload* means to take a function and write another function of the same name that takes a different set of parameters. An overloaded function can optionally return a different type, but the parameters must be different, whether in number or type or both. The overloaded function can live in the same class or in a derived class. The idea here is to create what appears to be a single function that can take several types of parameters. For example, you may have a function called Append() that works on strings. By using Append(), you would be able to append a string to the end of the string represented by the instance, or you could append a single character to the end of the string represented by the instance. Now, although it feels like one function called Append(), really you would implement it as two separate functions: one that takes a string parameter and one that takes a character parameter.

In this section, we talk about one particular issue dealing with overriding functions (that is, replacing a function in a derived class). We said something a few paragraphs back that many others have said: We mentioned that the function must have the same parameter types and must return the same type.

![](img/6ba99460b0feb3585671a4612ff5fabb_528_0.png)

A situation exists under which you can violate this rule, although only slightly. You can violate the rule of an overridden function returning the same type as the original function if all three of the following are true:

- The overridden function returns an instance of a class derived from the type returned by the original function.
- You return either a pointer or a reference, not an object.
- If you return a pointer, the pointer doesn't refer to yet another pointer.

![](img/6ba99460b0feb3585671a4612ff5fabb_528_1.png)

Typically, you want to use this approach when you have a container class that holds multiple instances of another class. For example, you may have a class called Peripheral. You may also have a container class called PeripheralList, which holds instances of Peripheral. You may later derive a new class from Peripheral, called Printer, and a new class from PeripheralList, called PrinterList. If PeripheralList has a function that returns an instance of Peripheral, you would override that function in PrinterList. But instead of having it return an instance of Peripheral, you would have it return an instance of Printer. The OverridingDerived example shown in Listing 4-1 shows how to perform this task.

### Listing 4-1: Overriding and Returning a Derived Class

```cpp
#include <iostream>
#include <string>
#include <map>

using namespace std;

class Peripheral {
public:
    string Name;
    int Price;
    int SerialNumber;
```
