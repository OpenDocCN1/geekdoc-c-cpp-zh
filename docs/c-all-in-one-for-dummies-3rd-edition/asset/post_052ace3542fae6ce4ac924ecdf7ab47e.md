
```cpp
cout << x << endl;
else
  cout << -x << endl;
}
```

The `WriteAbsoluteValue()` member function is a template. It's preceded by the word `template` and a `template` parameter in angle brackets. Then it has a return type, `void`, the function name, and the function parameter.

When you create an instance of the class, you can call the member function, providing a type as need be, as in the following:

```cpp
int main()
{
  MyMath inst = string("George");
  inst.WriteAbsoluteValue(-50.5);
  inst.WriteAbsoluteValue(-35);
  return 0;
}
```

In the first call, the function takes a double (because, by default, the C++ compiler considers `-50.5` a double). In the second call, the function takes an integer. The compiler then generates two different forms of the function, and they both become members of the class.

![](img/6ba99460b0feb3585671a4612ff5fabb_577_0.png)

Although you can use function templates as class members, you cannot make them virtual. The compiler will not allow it, and the ANSI standard forbids ("forbids," we say) you from doing it. In fact, we tried it with Code::Blocks just to see what friendly message we would get. Here it is:

> `'virtual' can only be specified for functions`

We guess by *functions* it means actual functions — not function templates.

## Chapter 6: Programming with the Standard Library

### In This Chapter

- **Architecting the Standard C++ Library**
- **Storing data in vector or map**
- **Containing data with a list or set**
- **Stacking and queuing**
- **Copying containers**
- **Using dynamic arrays**
- **Working with unordered data**

When you get around in the world of C++ programming (a fun world indeed!), you're going to encounter two different *libraries* that people use to make their lives easier. That, after all, the ultimate point of computers — to make our lives easier, right? These two libraries are

- Standard C++ Library
- Standard Template Library (STL)

Some people say, “We use STL.” Others say, “We use the Standard C++ Library.” In this case, *library* means a set of classes that you can use in your applications. These libraries include handy classes, such as `string` and `vector` (which is like an array in that it’s a list in which you can store objects).

The difference between the Standard C++ Library and STL is that STL came first. STL was used by so many developers that the American National Standards Institute (ANSI) decided to standardize it. The result is the similar Standard C++ Library that is part of the official ANSI standard and now part of most modern C++ compilers (including Code::Blocks, Microsoft Visual C++, Borland C++ Builder, MinGW, Cygwin, and Dev-C++). We use the Standard C++ Library in this chapter. Because we know that this is C++, we just call it the *Standard Library*.

The concepts that we present here apply to STL, so if you’re using STL, you can use this chapter.

### Architecting the Standard Library

When people start using the Standard Library, they often ask: Where’s the source code? We see the header files, but where are the .cpp files? This question has an easy answer: There are no .cpp files! ANSI architected the Standard Library for ease of use and reliability.

The classes contain their functions inside the class definitions; there are no forward declarations. You don’t add source files to your project or linking in compiled libraries. Just add an include line for the libraries you want.

### Containing Your Classes

Computers need a place to store things, so the Standard Library includes containers in which you can put things. The classes for containing things are called *container classes*. These classes are templates. When you create an instance of a container class, you specify what class it holds.

When you specify the class in a container, you are saying that the container will contain instances of your specified class or of classes derived from your specified class. You must decide whether the container will hold instances of the class, pointers to the instances, or references to the instances.

![](img/6ba99460b0feb3585671a4612ff5fabb_579_0.png)

### Storing in a vector

The vectors example shown in Listing 6-1 demonstrates how to use a container class. This particular container is a datatype called a *vector*, and it works much like an array.

**Listing 6-1: Using Vectors as Examples of Container Classes**

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main()
{
    vector<string> names;

    names.push_back("Tom");
    names.push_back("Dick");
    names.push_back("Harry");
    names.push_back("April");
    names.push_back("May");
    names.push_back("June");
}
```

**Listing 6-2: Containing the Type You Specify in Classes**

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Employee
{
public:
    string Name;
    string FireDate;
    int GoofoffDays;

    Employee(string aname, string afiredate,
        int agoofdays) : Name(aname), FireDate(afiredate),
        GoofoffDays(agoofdays) {}

};

int main()
{
    // A vector that holds strings
    vector<string> MyAliases;
    MyAliases.push_back(string("Bud The Sailor"));
    MyAliases.push_back(string("Rick Fixit"));
    MyAliases.push_back(string("Bobalou Billow"));
    cout << MyAliases[0] << endl;
    cout << MyAliases[1] << endl;
    cout << MyAliases[2] << endl;

    // A vector that holds integers
    vector<int> LuckyNumbers;
    LuckyNumbers.push_back(13);
    LuckyNumbers.push_back(26);
    LuckyNumbers.push_back(52);
    cout << LuckyNumbers[0] << endl;
    cout << LuckyNumbers[1] << endl;
    cout << LuckyNumbers[2] << endl;

    // A vector that holds Employee instances
    vector<Employee> GreatWorkers;
    GreatWorkers.push_back(Employee("George Washington", "123100", 50));
    GreatWorkers.push_back(Employee("Thomas Jefferson", "052002", 40));
    cout << GreatWorkers[0].Name << endl;
    cout << GreatWorkers[1].Name << endl;

    return 0;
}
```

After you compile and run this application, you see the following output from the cout statements:

```
Bud The Sailor
Rick Fixit
Bobalou Billow
13
26
52
George Washington
Thomas Jefferson
```

### Mapping your data

The Maps example shown in Listing 6-3 demonstrates a type of container called a map. A map works much like a vector, except for one main difference: You look up items in vector by putting a number inside brackets as in this

```cpp
cout << names[0] << endl;
```

but with a map, you can use any class or type you want for the index, not just numbers. This feature lets you associate objects. Take a gander at Listing 6-3 to see where we're coming from.

**Listing 6-3: Associating Objects with map**

```cpp
#include <iostream>
#include <map>

using namespace std;

int main()
{
    map<string, string> marriages;

    marriages["Tom"] = "Suzy";
    marriages["Harry"] = "Harriet";

    cout << marriages["Tom"] << endl;
    cout << marriages["Harry"] << endl;

    return 0;
}
```

First, you can see that to use map, we declare a variable of class map, supplying to the template the types of first the keys (a kind of index into the map) and then the values:

```cpp
map<string, string> marriages;
```

Then we store something in map by putting a key inside brackets and setting it equal to a value:

```cpp
marriages["Tom"] = "Suzy";
```

And to retrieve that particular item, we grab it, basing our choice of it on the key:

```cpp
cout << marriages["Tom"] << endl;
```

And voilà! We get back the item stored in `map` for that particular key. Think of `map` like an array, except the keys can be any object, not just a string. When you run this example, you see the following two strings as output:

```
Suzy
Harriet
```

![](img/6ba99460b0feb3585671a4612ff5fabb_583_0.png)

Even though the keys can be any type or class, you must specify the type or class you’re using when you set up `map`. And after you do that, you can use only that type for the particular `map`. Thus, if you say the keys will be strings, you cannot then use an integer for a key, as in `marriages[3] = "Suzy";`.

### Containing instances, pointers, or references

One of the most common discussions you encounter when people start talking about how to use the container templates is whether to put instances in the containers, pointers, or references. For example, which of these should you type:

```
vector<MyClass>
vector<MyClass *>
vector<MyClass &>
```

In other words, do you want your container to store the actual instance (whatever that might mean), a reference to the actual instance, or a pointer to the instance?

To explore this idea, have a look at the Maps2 example in Listing 6-4. Here we’re trying out the different ways of storing things in `map`: instances, pointers, and references.

**Listing 6-4: Making Decisions: Oh, What to Store?**

```cpp
#include <iostream>
#include <map>

using namespace std;

class StoreMe
{
public:
    int Item;
};

bool operator < (const StoreMe & first,
                 const StoreMe & second)
{
    return first.Item < second.Item;
}

int main()
{
```
