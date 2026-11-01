
```cpp
gsl::owner<int*> i = new int;  // You're the owner
    return i;                // Passing ownership out of the function
}
```

```cpp
void consume(gsl::owner<int*> i) // Taking on ownership
{
    delete i;                // It's yours, you can destroy it
}
```

```cpp
void p_and_c()
{
    auto i = produce();      // create...
    consume(i);              // ...and destroy
}
```

As you can see, enclosing the pointer with owner<> signals that ownership is being established. Let’s change things a little:

Click here to view code image

```cpp
int* produce()                // Just a raw pointer
{
    gsl::owner<int*> i = new int;
    return i;
}
```

What happens now?

You might be forgiven for thinking that the compiler will warn you that you are passing to an unowned pointer from an object signaling ownership. Unfortunately, this is not the case. The definition of owner is:

Click here to view code image

```cpp
template <class T,
    class =
std::enable_if_t<std::is_pointer<T>::value>>
using owner = T;
```

As you can see, there is no magic here. The definition of gsl::owner is very simple: if T is a pointer type, then gsl::owner<T> is an alias to T, otherwise it is undefined.

The purpose of this type is not to enforce ownership, but rather to hint to the user that there is a change in ownership going on. Rather than embedding this information in the function name, it is embedded in the type. While it is quite possible to create a type named owner that does all the required enforcement to correctly track and maintain ownership, there is no need: std::shared_ptr and std::unique_ptr do this job entirely adequately. The gsl::owner type is merely syntactic sugar that can be dropped into an existing codebase with no impact to the code, the ABI, or the execution, but with a large impact on readability and comprehension, as well as a contribution to the efficacy of static analyzers and code reviews.

As the GSL becomes more widely used we might expect IDEs to learn about its types and warn about abuses of ownership through signals in the editor, such as red underlining or floating lightbulb hints. Until then, do not use gsl::owner as an enforcement type, but rather as a documentation type. Ultimately, treat gsl::owner as a last resort when you are truly unable to use higher-level ownership abstractions.

## Summary

In summary:

- Owning something means being responsible for something.
- C++ has smart pointers for unambiguously signaling ownership.
- Use smart pointers to signal ownership, or `gsl::owner<T>`.
- Do not assume ownership from a raw pointer or a reference.

## Chapter 3.2

### I.3: Avoid singletons

### Global objects are bad

Global objects are bad, m’kay? You will hear this all the time, from programmers young and old, recited as an article of faith. Let’s look into why this is.

A global object lives in the global namespace. There is only one of these, hence the name “global.” The global namespace is the outermost declarative region of a translation unit. A name with global namespace scope is said to be a global name. Any object with a global name is a global object.

A global object is not necessarily visible to every translation unit of a program; the one-definition rule means that it can only be defined in one translation unit. However, a declaration can be repeated in any number of translation units.

Global objects have no access restrictions. If you can see it, you can interact with it. Global objects have no owner other than the program itself, which means no single entity is responsible for it. Global objects have static storage duration, so they are initialized at startup (or static initialization) and destroyed at shutdown (or static deinitialization).

This is problematic. Ownership is fundamental to reasoning about objects. Since nothing owns a global object, how can you reason about its state at any time? You might be calling functions on that object and then, suddenly and without warning, another entity may call other functions on that object without your knowledge.

Worse still, since nothing owns global objects, their construction sequence is not determined by the standard. You have no idea in which order global objects will be constructed, which leads to a rather frustrating category of bug that we shall cover later.

### Singleton Design Pattern

Having convinced you of the harm that global objects cause to your codebase, let us turn our attention to singletons. I first encountered this term in 1994 when the book Design Patterns¹ was published. This venerable tome was a tremendously exciting read at the time and is still a very useful book to have on your shelf or your e-reader. It describes patterns that recur in software engineering, in much the same way that patterns recur in conventional architecture, such as cupola, portico, or cloister. What was so welcome about this book was that it identified common patterns in programming and gave them names. Naming is hard, and having someone do the naming for us was a great boon.

1. Gamma, E, Helm, R, Johnson, R, and Vlissides, J, 1994. Design Patterns. Reading, MA: Addison-Wesley.

The book categorizes the patterns in three ways, as creational, structural, or behavioral patterns. It is within the creational division that we find the singleton, which restricts object creation for a class to only one instance. Of course, with such a fabulous text outlining such a well-used pattern, it was taken for granted that using a singleton was A Good Thing. After all, we had all been using something like singletons for years, we just had not yet given them a name that we could all agree on.

A popular example of a singleton is the main window. The main window is where all the action happens, collecting user input and displaying results. You should only create one main window, so it might make sense to prevent the creation of another. Another example is the manager class. This is characterized by including the name “manager” in the identifier. This is a strong sign that in fact a singleton has been created, and that there are problems deciding about ownership of whatever is being managed.

### Static initialization order fiasco

Singletons are prone to the static initialization order fiasco.² This term was coined by Marshall Cline in his C++ FAQ and characterizes the problem of dependent objects being constructed out of order. Consider two global objects, A and B, where the constructor of B uses some functionality provided by A and so A must be constructed first. At link time, the linker identifies the set of objects with static storage duration, sets aside an area of the memory for them to exist in, and creates a list of constructors to be called before main is called. At runtime, this is called static initialization.

2. “Fiasco” is possibly an unfair characterization. Static initialization was never supposed to offer a topological ordering of initialization. That was infeasible with separate compilation, incremental linking, and linkers from the 1980s. C++ had to live with the existing operating systems. This was a time when systems programmers were used to living with sharp tools.

Now, although you can identify that B depends on A and so A must be constructed first, there is no standard way to signal to the linker that this is the case. Indeed, how could you do that? You would need to find some way of exposing the dependency in the translation unit, but the compiler only knows about the translation unit it is compiling.

We can hear your brow furrowing. “Well, what if I told the linker what order to create them in? Could the linker be modified to accommodate that?” In fact, this has been tried. Long ago I used an IDE called Code Warrior, by Metrowerks. The edition I was using exposed a property that allowed me to dictate the order of construction of static objects. It worked fine, for a while, until I unwittingly created a subtle circular dependency that took me the better part of twenty hours to track down.

> By keeping your object dependencies in a single translation unit, you avoid all of these problems while maintaining clarity of purpose and separation of concerns.

You aren’t convinced. “Circular dependencies are part and parcel of engineering development. The fact that you managed to create one because you got your relationships wrong shouldn’t preclude the option to dictate the creation order at static initialization.” Indeed, I did actually resolve the problem and carried on, but then I needed to port the codebase to another
