# Class Constructors and Destructors

At this point, you need to do more with the Stock class. There are certain standard functions, called *constructors* and *destructors*, that you should normally provide for a class. Let’s talk about why they are needed and how to write them.

One of C++’s aims is to make using class objects similar to using standard types. However, the code provided so far in this chapter doesn’t let you initialize a Stock object the way you can an ordinary int or struct. That is, the usual initialization syntax doesn’t carry over for the Stock type

```
int year = 2001;                                  // valid initialization
struct thing
{
    char * pn;
    int m;
};
thing amabob = {"widget", -23};                  // valid initialization
Stock hot = {"Sukie’s Autos, Inc.", 200, 50.25};  // NO! compile error
```

The reason you can’t initialize a Stock object this way is because the data parts have private access status, which means a program cannot access the data members directly. As you’ve seen, the only way a program can access the data members is through a member function. Therefore, you need to devise an appropriate member function if you’re to succeed in initializing an object. (You could initialize a class object as just shown if you made the data members public instead of private, but making the data public goes against one of the main justifications for using classes: data hiding.)

In general, it’s best that all objects be initialized when they are created. For example, consider the following code:

```
Stock gift;
gift.buy(10, 24.75);
```

With the current implementation of the Stock class, the gift object has no value for the company member. The class design assumes that the user calls acquire() before calling any other member functions, but there is no way to enforce that assumption. One way around this difficulty is to have objects initialized automatically when they are created. To accomplish this, C++ provides for special member functions, called *class constructors*, especially for constructing new objects and assigning values to their data members. More precisely, C++ provides a name for these member functions and a syntax for using them, and you provide the method definition. The name is the same as the class name. For example, a possible constructor for the Stock class is a member function called Stock(). The constructor prototype and header have an interesting property: Although the constructor has no return value, it’s not declared type void. In fact, a constructor has no declared type.