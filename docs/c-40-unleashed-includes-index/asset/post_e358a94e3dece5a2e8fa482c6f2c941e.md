
However, sometimes one needs to synthesize a special "default value" for a type parameter without knowing the type of the parameter until runtime. All that matters to set the scene is that we are defining a generic type with a type parameter T. In the definition of that type, we don’t know anything about T. It could be an int, a string, a Customer, whatever. The generic type can use T anywhere as if it were a known type:

```
class Sample<T>
{
    private T _data;

    // ...

    public void Reset()
    {
        // How can we set _data to the default value for type T?
    }
}
```

For example, in this case we’re defining a field of type T. All is good and well, our code is very generic as we intended it to be. But what if we need to check that _data against a default value? (For example, if T were a reference type, that would be a null check?) Or say you need to reinitialize the field to go back to its default value? Clearly, we need something here to express "default value of T," for whatever T may be. That’s where the default value expression comes in:

```
class Sample<T>
{
    private T _data;

    // ...

    public void Reset()
    {
        _data = default(T);
    }
}
```

Talking about generic parameters gives us a good opportunity to take a little look behind the scenes and get a feel for how generics work. The essential idea is simple: Open generic types are types with holes in them. Every type parameter creates such a hole whose size is unknown. For example, if it’s set to an Int32, 4 bytes of storage will be required, but for a DateTime more space will be needed. Think of the act of defining a generic type roughly as operating a perforator that leaves holes for every occurrence of a type parameter. This analogy is depicted in Figure 6.10.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_352_0.png)

FIGURE 6.11 A generic type with a field of type T gives rise to a “hole.”

Notice the default value expression doesn’t just work with type parameters; it can be used with any type. For reference types, default will produce a null reference; for value types, it will produce the default value (everything “zeroed out” essentially):

```
int zero = default(int);
string nothing = default(string);
DateTime longAgo = default(DateTime); // 01/01/0001 12:00:00 AM
```

## Creating Objects with the new Operator

We already know a couple of ways to create instances of types: the use of literals and default value expressions. And because expressions evaluate to produce something of a certain type, they can be used in all places where objects are expected.

However, so far we’ve yet to discuss one of the most common ways of creating object instances: the use of constructors. Constructors are nothing but regular methods that are defined on a type but are known to serve a special goal: They return an instance of the containing type. Every type can have different constructors that take in different arguments, as a matter of friendliness toward the consumer of the type. This is facilitated by means of method overloading, discussed in Chapter 10, “Methods.”

Because we are deferring the discussion of defining our own types with constructors until later, let’s take a look at an existing type from the BCL: System.TimeSpan, the representation of a difference between two times. To inspect the type while being able to peek under the hood, we can use .NET Reflector. You can find a type by using the search option or by drilling down through the tree view on the left (in this case, by following mscorlib, CommonLanguageRuntime, System, TimeSpan). Figure 6.12 highlights the constructors of TimeSpan as seen through .NET Reflector.

The most familiar way for a C# developer to spot the constructors is to look at the right side where the decompiled C# code is shown. Constructors look like methods but don’t have a return type and are named after the type itself. In this particular case, four overloads have been defined:

```
    public TimeSpan(long ticks);
    public TimeSpan(int hours, int minutes, int seconds);
    public TimeSpan(int days, int hours, int minutes, int seconds);
    public TimeSpan(int days, int hours, int minutes, int seconds,
                    int milliseconds);
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_353_0.png)

FIGURE 6.12 Looking at the constructors for System.TimeSpan.

On the left side, in the tree view, the internal representation is shown. In reality, constructors are defined as methods with the name .ctor. Because of their special status as creators for object instances, they deserve special syntactical treatment in the language. That’s what the new operator is about.

To create an instance of the TimeSpan type, you use the new operator followed by the type name and a (possibly empty) set of parameters:

```
    var oneHourAndAHalf = new TimeSpan(1, 30, 0);
```

Because the type already appears on the right side of the assignment, it’s perfectly fine to omit the type on the left side and use type inference by means of the var keyword.

### CONCRETE OR NOT?

Constructors can be called only for concrete types, but what does that mean? Let’s go the opposite direction: Something concrete is not abstract. Abstract types are types that lack parts of their implementation.

Interfaces are an example of this: They just describe what an object is capable of doing (for example, IEnumerable says an object can be enumerated over, for example to retrieve elements in a collection), rather than saying how it is done. So it doesn’t make sense to create an instance of just IEnumerable; we need something that implements the interface instead (like ArrayList).

![](img/a16f85e62ce9bdc527f4b09dbfe26092_355_0.png)

FIGURE 6.14 How a constructor initializes a value type object.

First, the memory address of the local variable is retrieved using the ldloca instruction, which stands for “load a local’s address.” In addition to the address being pushed on the stack, the arguments to the constructor are pushed, too. For our example, there are three: 1 for hours, 30 for minutes, and 0 for seconds. Finally, a call is made to the constructor method. The address where the data being initialized lives can be seen as an implicit parameter to the runtime to call the constructor method.

With reference types, things go a little differently. Room for the data contained in a reference type is allocated dynamically in another portion of memory (called the heap). In-depth coverage of memory allocation in the CLR would lead us astray at this point, so let’s ignore the nitty-gritty details for now. Just recall reference types consist of a reference to data that lives elsewhere. Aliasing can occur, causing multiple references to exist to the same piece of data.

The prototypical example of a reference type is System.String, which has a few constructors defined that allow us to illustrate how instances of reference types are created:

```
var tenStars = new string('*', 10);
```

This constructor takes in a char parameter and an integer one, producing a string that consists of the repetition of the specified character as many times as specified by the integer parameter. In the preceding example, 10 asterisks result.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_357_0.png)

FIGURE 6.16 How a constructor creates a reference type object.

## Object Initializers

Calling constructors is an essential mechanism for creating new instances of objects, but sometimes it doesn't suffice. A common problem with constructors is the number of overloads they have to accommodate for various scenarios. For example, the TimeSpan type has no fewer than four constructor overloads for developer convenience. Internally, a TimeSpan simply consists of a tick count, but as you've seen, more handy overloads exist that allow us to supply hours, minutes, and seconds (for example).

It turns out TimeSpan is a type that leads to a good developer experience: The most useful overloads are available, so while browsing the list of overloads, you'll most certainly want something that's close enough to what you want. In our previous example, we had to express 1.5 hours, for which we used the overload taking in hours, minutes, and seconds. Although seconds are of no interest to us, it doesn't hurt much to have to specify a zero value for that parameter.

Unfortunately, lots of other types exist that lack convenient constructors that suit everyone's needs. This problem ultimately boils down to an explosion of possible combinations of the discrete pieces of data to be initialized. Assume you have a Person type that contains 20 fields for name, date of birth, address, and so on. Maybe a few fields are required, but others aren't. So how many constructors do you provide to make everyone happy? Not only would you go nuts trying to come up with all combinations, think of the poor API user browsing the list of overloads in search of the right constructor. Figure 6.17 pinpoints this issue by looking at constructor overloads in the code editor.
