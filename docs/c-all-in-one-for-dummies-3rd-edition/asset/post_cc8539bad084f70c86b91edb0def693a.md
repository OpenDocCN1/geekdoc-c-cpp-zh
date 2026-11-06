
### Listing 3-1: Creating Temporary Instances with Functional Constructors

```cpp
#include <iostream>
#include <string>

using namespace std;

void WriteMe(string str)
{
    cout << "Here I am: " << str << endl;
}

int main()
{
    WriteMe(string("Sam"));
    return 0;
}
```

When you compile and run this, you see this output:

```text
Here I am: Sam
```

In main(), we created a temporary instance of the string class. (Remember, string is a class.) But as it turns out, an even shorter version of this is available. If we had called WriteMe(), we could have just done this:

```cpp
WriteMe("Sam");
```

This code works out well because you don't even feel like you're working with a class called string. The parameter just seems like a basic type, and you're passing a character array, Sam. However, the parameter is an instance of a class. Here's how the code works. Suppose you have a class like the one found in the Constructor06 example and a function to go with it:

```cpp
class MyNumber
{
public:
    int First;
    MyNumber(int TheFirst) : First(TheFirst) {}
};
```

```cpp
void WriteNumber(MyNumber num)
{
    cout << num.First << endl;
}
```

(WriteNumber() is *not* a member of MyNumber.) You can do any of the following calls to WriteNumber().

```cpp
MyNumber prime = 17;
WriteNumber(prime);
WriteNumber(MyNumber(23));
WriteNumber(29);
```

The first call uses a previously declared variable of type `MyNumber`. The second call creates a temporary instance, passing the value 23 into the constructor. The third one also creates a temporary instance, but it does so implicitly! The output from this example is

```text
17
23
29
```

You may wonder when your temporary variables get destroyed. For instance, if you call `WriteNumber(MyNumber(23));`, how long does the temporary `MyNumber` instance live on? The ANSI standard proudly proclaims that the instance will get deleted at the end of the *full expression*. In other words, after the line is done, the temporary instance will be done for.

![](img/6ba99460b0feb3585671a4612ff5fabb_505_0.png)

Be careful when using implicit temporary objects. Consider the following class and function found in the `Constructor07` example:

```cpp
class MyName
{
public:
    string First;
    MyName(string TheFirst) : First(TheFirst) {}
};

void WriteName(MyName name)
{
    cout << "Hi I am " << name.First << endl;
}
```

Seems straightforward. The `MyName` constructor takes a string, so it seems like we should be able to do this when we call the `WriteName()` function:

```cpp
WriteName("George");
```

Except we can’t. The compiler gives us an error message:

```text
In function 'int main()':
error: could not convert '(const char*)"George"' from 'const char*'
    to 'MyName'
```

Here’s the problem: The compiler got shortsighted. The compiler considers the type of the string constant a `const char *` (that is, a pointer to a const character, or really a constant character array). Although we don’t have any constructors that take a `const char *` parameter, we do have one that takes a string, and it has a constructor that takes a `const char *` parameter. Unfortunately, the compiler doesn’t fall for that, and it complains. So we have to adjust our function call just a tad, like so:

```cpp
WriteName(string("George"));
```

And this time it works. Now we *explicitly* create a temporary `string` instance. And by using that, we *implicitly* create a temporary instance of our own class, `MyName`. It would be nice if the compiler could wade through this and *implicitly* create the `string` instance for us, but it doesn't seem to want to. Oh well. Calling `WriteName(string("George"))`; works well enough for us.

## Calling one constructor from another

If you have some initialization code and you want several constructors to call it, you might try putting the code in one constructor and then having the other constructors call the constructor that has the initialization code.

Unfortunately, that won't work. Some things in life we just can't have, and this is one of them. If you have a constructor and write code to call another constructor, such as this

```cpp
CallOne::CallOne(int ax)
{
    y = 20;
    CallOne();
}
```

where `CallOne` is your class, then this will compile but won't behave the way you may expect. The line `CallOne();` is not calling a constructor for the same instance! The compiler treats this line as a *functional* constructor. Thus the line creates a *separate, temporary* instance. And then at the end of the line `CallOne()`, the application deletes the instance.

You can see this behavior with the following class:

```cpp
class CallOne
{
public:
    int x,y;
    CallOne();
    CallOne(int ax);
};

CallOne::CallOne()
{
    x = 10;
    y = 10;
}

CallOne::CallOne(int ax)
{
    y = 20;
    CallOne();
}
```

Book IV Chapter 3 Constructors, Destructors, and Exceptions

When you create an instance by using the second constructor like this, the value of the y member of the instance will be 20, not 10:

```cpp
CallOne Mine(10);
```

To people who don’t know any different, it may look like the y would first get set to 20 in the second constructor, and then the call to the default constructor would cause it to get changed to 10. But that’s not the case: The second constructor is not calling the default constructor for the same object; it’s creating a separate, temporary instance.

![](img/6ba99460b0feb3585671a4612ff5fabb_507_0.png)

If you have common initialization code that you want in multiple constructors, put the code in its own private or protected function (called, for example, `Init()`), and have each constructor call the `Init()` function. If you have one constructor call another constructor, it won’t work. The second constructor will be operating on a separate instance.

## Copying instances with copy constructors

One nice thing about C++ is that it lets you copy instances of classes. For example, if you have a class called Copyable, you can write code like this:

```cpp
Copyable first;
Copyable second = first;
```

This will create two instances, and second will be a duplicate of first. The application will accomplish this by simply copying all the member variables from first to second.

That works pretty well, except sometimes you want to customize the behavior just a bit. For example, you may have a member variable that contains a unique ID for each instance. In your constructor, you may have code that generates a unique ID. The problem is that the previous sample will not call your constructor: It will just make a duplicate of the object. Thus your two objects will have the same number for their supposedly “unique” IDs. So much for diversity.

So if you want to have control over the copying, you can create a copy constructor. A copy constructor is just a constructor that takes as a parameter a reference to another instance of the same class, as in this example:

```cpp
Copyable(const Copyable& source);
```

When you copy an instance, your application will call this constructor. The parameter to this constructor will be the instance you’re copying. Thus, in the case of Copyable second = first;, the source parameter will be first. And because it’s a reference (which is required for copy constructors), you can access its members by using the dot notation (.) rather than the pointer notation (->).

The Constructor08 example shown in Listing 3-2 is a complete application that demonstrates copy constructors.

### Listing 3-2: Customizing the Copying of Instances

```cpp
#include <iostream>

using namespace std;

class Copyable
{
protected:
    static int NextAvailableID;
    int UniqueID;
public:
    int SomeNumber;
    int GetID() { return UniqueID; }
    Copyable();
    Copyable(int x);
    Copyable(const Copyable& source);
};

Copyable::Copyable()
{
    UniqueID = NextAvailableID;
    NextAvailableID++;
}

Copyable::Copyable(int x)
{
    UniqueID = NextAvailableID;
    NextAvailableID++;
    SomeNumber = x;
}

Copyable::Copyable(const Copyable& source)
{
    UniqueID = NextAvailableID;
    NextAvailableID++;
    SomeNumber = source.SomeNumber;
}

int Copyable::NextAvailableID;

int main()
{
    Copyable take1 = 100;
    Copyable take2;
    take2.SomeNumber = 200;
    Copyable take3 = take1;

    cout << take1.GetID() << " "
         << take1.SomeNumber << endl;
}
```

_(continued)_
