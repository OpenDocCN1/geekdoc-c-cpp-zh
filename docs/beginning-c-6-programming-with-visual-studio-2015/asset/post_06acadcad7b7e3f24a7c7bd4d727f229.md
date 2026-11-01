
![](img/cf72ea860016d2d680fc085fc06f265a_268_0.png)

**FIGURE 10-8**

You can find the code generated for these two enumerations in the code files, Suit.cs and Rank.cs. First, you can find the full code for this example in Ch10CardLib folder/Suit.cs:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace Ch10CardLib
{
    public enum Suit
    {
        Club,
        Diamond,
        Heart,
        Spade,
    }
}
```

And you can find the full code for this example in Ch10CardLib folder/Rank.cs:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace Ch10CardLib
{
    public enum Rank
    {
        Ace = 1,
        Deuce,
        Three,
        Four,
        Five,
        Six,
        Seven,
        Eight,
        Nine,
        Ten,
        Jack,
        Queen,
        King,
    }
}
```

Alternatively, you can add this code manually by adding Suit.cs and Rank.cs code files and then entering the code. Note that the extra commas added by the code generator after the last enumeration member do not prevent compilation and do not result in an additional "empty" member being created — although they are a little messy.

### Adding the Card Class

To add the Card class, you'll use a mix of the class designer and code editor. Adding a class in the class designer is much like adding an enumeration — you drag the appropriate entry from the Toolbox into the diagram. In this case, you drag a Class into the diagram and name the new class Card.

Use the Class Details window to add the fields rank and suit, and then use the Properties window to set the Constant Kind of the field to readonly. You also need to add two constructors — a private default constructor, and a public constructor that takes two parameters, newSuit and newRank, of types Suit and Rank, respectively. Finally, you override ToString(), which requires you to change the Inheritance Modifier in the Properties window to override.

Figure 10-9 shows the Class Details window and the Card class with all the information entered. (You can find this code in Ch10CardLib\Card.cs.)

![](img/cf72ea860016d2d680fc085fc06f265a_269_0.png)

**FIGURE 10-9**

Next, modify the code for the class in Card.cs as follows (or add the code shown to a new class called Card in the Ch10CardLib namespace):

```csharp
assigned[destCard] = true;
newDeck[destCard] = cards[i];
}
newDeck.CopyTo(cards, 0);
}
}
```

The last line of this method uses the CopyTo() method of the System.Array class (used whenever you create an array) to copy each of the cards in newDeck back into cards. This means you are using the same set of Card objects in the same cards object, rather than creating any new instances. If you had instead used cards = newDeck, then you would be replacing the object instance referred to by cards with another. This could cause problems if code elsewhere were retaining a reference to the original cards instance — which wouldn’t be shuffled!

That completes the class library code.

### A Client Application for the Class Library

To keep things simple, you can add a client console application to the solution containing the class library. To do so, simply right-click on the solution in Solution Explorer and select Add ▸ New Project. The new project is called Ch10CardClient.

To use the class library you have created from this new console application project, add a reference to your Ch10CardLib class library project. You can do that through the Projects tab of the Reference Manager dialog box, as shown in Figure 10-12.

![](img/cf72ea860016d2d680fc085fc06f265a_273_0.png)

**FIGURE 10-12**

Select the project and click OK to add the reference.

Because this new project is the second one you've created, you also need to specify that it is the startup project for the solution, meaning the one that is executed when you click Run. To do so, simply right-click on the project name in the Solution Explorer window and select the Set as StartUp Project menu option.

Next, add the code that uses your new classes. That doesn't require anything particularly special, so the following code will do (you can find this code in Ch10CardClient\Program.cs):

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using static System.Console;
using Ch10CardLib;
namespace Ch10CardClient
{
    class Program
    {
        static void Main(string[] args)
        {
            Deck myDeck = new Deck();
            myDeck.Shuffle();
            for (int i = 0; i < 52; i++)
            {
                Card tempCard = myDeck.GetCard(i);
                Write(tempCard.ToString());
                if (i != 51)
                    Write(", ");
                else
                    WriteLine();
            }
            ReadKey();
        }
    }
}
```

Figure 10-13 shows the result you'll get if you run this application.

![](img/cf72ea860016d2d680fc085fc06f265a_274_0.png)

**FIGURE 10-13**

This is a random arrangement of the 52 playing cards in the deck. You'll continue to develop and use this class library in later chapters.

## WHAT YOU LEARNED IN THIS CHAPTER

| TOPIC | KEY CONCEPTS |
|---|---|
| Member definitions | You can define field, method, and property members in a class. Fields are defined with an accessibility, name, and type. Methods are defined with an accessibility, return type, name, and parameters. Properties are defined with an accessibility, name, and a get and/or set accessor. Individual property accessors can have their own accessibility, which must be less accessible than the property as a whole. |
| Member hiding and overrides | Properties and methods can be defined as `abstract` or `virtual` in base classes to define inheritance. Derived classes must implement abstract members, and can override virtual members, with the `override` keyword. They can also provide new implementations with the `new` keyword, and prevent further overrides of `virtual` members with the `sealed` keyword. Base implementations can be called with the `base` keyword. |
| Interface implementation | A class that implements an interface must implement all of the members defined by that interface as public. You can implement interfaces implicitly or explicitly, where explicit implementations are only available through an interface reference. |
| Partial definitions | You can split class definitions across multiple code files with the `partial` keyword. You can also create partial methods with the `partial` keyword. Partial methods have certain restrictions, including no return value or `out` parameters, and are not compiled if no implementation is provided. |

## 11 Collections, Comparisons, and Conversions

### WHAT YOU WILL LEARN IN THIS CHAPTER

- Defining and using collections
- Learning the types of collections that are available
- Comparing types and using the is operator
- Comparing values and overloading operators
- Defining and using conversions
- Using the as operator

### WROX.COM CODE DOWNLOADS FOR THIS CHAPTER

You can find the wrox.com code downloads for this chapter at www.wrox.com/go/beginning-visual-csharp-2015-programming on the Download Code tab. The code is in the Chapter 11 download and individually named according to the names throughout the chapter.

You’ve covered all the basic OOP techniques in C# now, but there are some more advanced techniques that are worth becoming familiar with. These techniques relate to certain problems that you must solve regularly when you are writing code. Learning about them will make it much easier to progress and allow you to concentrate on other, potentially more important aspects of your applications. In this chapter, you look at the following:

- **Collections** — Collections enable you to maintain groups of objects. Unlike arrays, which you’ve used in earlier chapters, collections can include more advanced functionality, such as controlling access to the objects they contain, searching and sorting, and
