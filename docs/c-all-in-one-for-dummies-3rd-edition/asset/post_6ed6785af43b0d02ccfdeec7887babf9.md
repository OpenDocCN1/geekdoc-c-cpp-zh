
## Chapter 5: Modeling Your Applications with UML

### In This Chapter

- Using some UML extras, such as packages, notes, and tags
- Taking advantage of the freedom UML gives you
- Creating C++ enumerations in UML
- Using static members in UML
- Notating templates with UML

In this chapter, we list some miscellaneous details about using UML. After you understand how to use the diagrams and you have a feel for a methodology or process, read this chapter for interesting details about UML. For example, you can use several symbols in any of your diagrams to make them more descriptive; we discuss them here. We also talk about how to show various C++ features in UML.

### Using UML Goodies

The UML specification is huge. We’re talking *big*. You can see the currently released versions at http://www.omg.org/spec/UML/ or the UML 2.5 specification at http://www.omg.org/spec/UML/2.5/. In this section, we give you some additional information that you can use when creating UML diagrams.

### Packaging your symbols

In computer programming, a common term is *namespace*. When you have functions and classes and variables, you can put them into their own namespace, which is nothing more than a grouping. When you do so, the names of the functions, classes, and variables must be unique within the namespace. But if you create another namespace, you can reuse any of the names from the other namespace. In technical terms, *identifiers* must be unique *within a namespace*.

To make this concept clear, let us show you a C++ example. In C++, you can create a namespace by using none other than the namespace keyword. Have a gander at the Namespace01 example, shown in Listing 5-1 — and bear in mind the `using namespace std;` line you see in each of these applications, too.

**Listing 5-1:** Using the Namespace Keyword to Create a Namespace in C++

```cpp
#include <iostream>

using namespace std;

namespace Work
{
    int FavoriteNumber;

    class Info
    {
    public:
        string CompanyName;
        string Position;
    };

    void DoStuff()
    {
        cout << "Doing some work!" << endl;
    }
}

namespace Play
{
    int FavoriteNumber;

    class Info
    {
    public:
        string FullName;
        string Hobby;
    };

    void DoStuff()
    {
        cout << "Having fun!" << endl;
    }
}

int main()
{
    // Work stuff
    Work::FavoriteNumber = 7;
    Work::Info WorkInformation;
    WorkInformation.CompanyName = "Spaceley Sprockets";
    WorkInformation.Position = "Worker";
    Work::DoStuff();

    // Play stuff
    Play::FavoriteNumber = 13;
    Play::Info PlayInformation;
    PlayInformation.FullName = "George Jetson";
    PlayInformation.Hobby = "Playing with the dog";
    Play::DoStuff();

    return 0;
}
```

In Listing 5-1, we created two different namespaces — one called Work and one called Play. Just to prove the point, we created a global variable, a class name, and a function inside each namespace, and they are each named the same as in the other namespace. To make use of these items, down in main we precede them with the namespace name and two colons. So you can see that we have two separate global variables:

```cpp
Work::FavoriteNumber = 7;
Play::FavoriteNumber = 13;
```

and that we created instances of two separate classes:

```cpp
Work::Info WorkInformation;
Play::Info PlayInformation;
```

These are completely separate classes and variables; they just happen to have the same name. But they’re inside their own namespaces, so this is perfectly legal. And you can see that we also called the function in each namespace. Again, we put the namespace name, two colons, and then the function name. As before, these are each separate functions; they just happen to share the same name.

![](img/6ba99460b0feb3585671a4612ff5fabb_350_0.png)

Think of a namespace as a grouping mechanism. You can group related items, and it frees you from having to worry about whether the name you came up with is unique.

![](img/6ba99460b0feb3585671a4612ff5fabb_350_1.png)

To keep everything neat and tidy, the designers of C++ have put all their own features, such as cout, in their own namespace. This namespace is called std, which is short for *standard*. To make use of cout and other standard features, you need to use the std namespace. This means you would normally type `std::cout` to access cout. However, having a lot of cout entries in your code can be cumbersome. To simplify access to the std namespace, then, you can just put `using namespace std;` near the start of your code. Then every time the compiler comes across an identifier it doesn’t recognize, it follows up by checking the std namespace. Thus, you can have cout without the `std::cout` before it. The compiler at first won’t recognize cout, but then the compiler will check the std namespace, thus locating cout.

And now, on to UML. In UML, you can show namespaces in your diagrams by using packages. In UML, a package is equivalent to a namespace in C++ and other languages. A package looks like a file folder (not the kind in your computer, but the kind in those wondrous and archaic things that past generations of the late 20th century called *file cabinets*).

Figure 5-1 shows an example of a package. You can see that it’s a file-folder-looking thing, and the classes are inside it. We put two packages in this diagram — one called *Work* and one called *Play* — to match the classes in Listing 5-1.

![](img/6ba99460b0feb3585671a4612ff5fabb_351_0.png)

![](img/6ba99460b0feb3585671a4612ff5fabb_351_1.png)

Different Computer-Aided Software Engineering (CASE) tools and diagramming software do packages differently. If you are using Microsoft Visio to create diagrams, for example, its built-in UML tool does not let you draw your classes inside the package symbol. Instead, when you create a package symbol, you get a new, blank page on which to put your symbols.

Fortunately, there are a number of free CASE tools listed at `http://sourceforge.net/directory/development/case-tools/freshness:recently-updated/` that you can try in order to find a tool that meets your needs. Based on what you might see online, there doesn’t appear to be a Code::Blocks CASE plugin as of this writing — please write me at John@JohnMuellerBooks.com if you find one.

![](img/6ba99460b0feb3585671a4612ff5fabb_351_2.png)

In UML, by default, a namespace already exists. It’s called topLevel. If you don’t explicitly put your data inside a namespace, it automatically goes in the topLevel package.

### Notating your diagrams

UML has a handy little symbol called a *note* whose only purpose is to provide comments on a UML diagram. A note is much like a comment in C++ code: It has no bearing on the actual diagrams but is there for the benefit of us humans and other creatures with highly evolved brains to read.

### Free to Be UML

One of the great things about UML is that it gives you a great deal of freedom. For example, if you find a diagram that you don't care to use, you don't have to use it; you can still move through an entire software development process or methodology. For example, some people prefer to use sequence diagrams while staying away from collaboration diagrams. And some people don't use state diagrams and activity diagrams. Now some purists might complain about this, but as a software engineer, you need to do what works best for you and your team.

Further, UML is not intended to be used only for software engineering. The creators of UML designed it to be a general-purpose language for modeling, and it can be used for all sorts of projects. For example, in one book, every chapter started out with a UML activity diagram showing the flow of sections in the book.

Of course, most people will use UML for software engineering, primarily because many people outside the software field have simply never heard of UML.

Another area where UML allows freedom is in the methodology you choose. Although this book focuses on the Rational Unified Process (RUP), UML contains a rich set of diagrams and symbols that work with nearly any methodology.

Thanks to stereotypes (a method of creating a new symbol), you can even add symbols to UML; so if you're using a methodology with its own symbols, you are not trapped with those built into UML. Normally, you take an existing symbol and from it derive a new symbol that has similar, but more specialized features. You put the name in the funny-looking angle brackets, as in <<MyStereotype>>. However, there's an alternative: Rather than put the name inside those brackets (called guillemets), you can use your own, custom icon. In Figure 5-4, for example, we used the scroll symbol.

**Figure 5-4:** You can use custom icons for stereotypes.

![](img/6ba99460b0feb3585671a4612ff5fabb_353_0.png)
