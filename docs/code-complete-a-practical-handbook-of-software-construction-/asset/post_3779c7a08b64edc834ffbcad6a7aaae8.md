
- Streamline parameter passing
- Make central points of control
- Facilitate reusable code
- Plan for a family of programs
- Package related operations
- Accomplish a specific refactoring

## 6.5 Language-Specific Issues

Approaches to classes in different programming languages vary in interesting ways. Consider how you override a member routine to achieve polymorphism in a derived class. In Java, all routines are overridable by default and a routine must be declared *final* to prevent a derived class from overriding it. In C++, routines are not overridable by default. A routine must be declared *virtual* in the base class to be overridable. In Visual Basic, a routine must be declared *overridable* in the base class and the derived class should use the *overrides* keyword.

Here are some of the class-related areas that vary significantly depending on the language:

- Behavior of overridden constructors and destructors in an inheritance tree
- Behavior of constructors and destructors under exception-handling conditions
- Importance of default constructors (constructors with no arguments)
- Time at which a destructor or finalizer is called
- Wisdom of overriding the language’s built-in operators, including assignment and equality
- How memory is handled as objects are created and destroyed or as they are declared and go out of scope

Detailed discussions of these issues are beyond the scope of this book, but the “Additional Resources” section points to good language-specific resources.

## 6.6 Beyond Classes: Packages

**Cross-Reference** For more on the distinction between classes and packages, see “Levels of Design” in Section 5.2.

Classes are currently the best way for programmers to achieve modularity. But modularity is a big topic, and it extends beyond classes. Over the past several decades, software development has advanced in large part by increasing the granularity of the aggregations that we have to work with. The first aggregation we had was the statement, which

## Encapsulation

- Does the class minimize accessibility to its members?
- Does the class avoid exposing member data?
- Does the class hide its implementation details from other classes as much as the programming language permits?
- Does the class avoid making assumptions about its users, including its derived classes?
- Is the class independent of other classes? Is it loosely coupled?

## Inheritance

- Is inheritance used only to model “is a” relationships—that is, do derived classes adhere to the Liskov Substitution Principle?
- Does the class documentation describe the inheritance strategy?
- Do derived classes avoid “overriding” non-overridable routines?
- Are common interfaces, data, and behavior as high as possible in the inheritance tree?
- Are inheritance trees fairly shallow?
- Are all data members in the base class private rather than protected?

## Other Implementation Issues

- Does the class contain about seven data members or fewer?
- Does the class minimize direct and indirect routine calls to other classes?
- Does the class collaborate with other classes only to the extent absolutely necessary?
- Is all member data initialized in the constructor?
- Is the class designed to be used as deep copies rather than shallow copies unless there’s a measured reason to create shallow copies?

## Language-Specific Issues

- Have you investigated the language-specific issues for classes in your specific programming language?

## Additional Resources

## Classes in General

Meyer, Bertrand. *Object-Oriented Software Construction*, 2d ed. New York, NY: Prentice Hall PTR, 1997. This book contains an in-depth discussion of abstract data types and explains how they form the basis for classes. Chapters 14–16 discuss inheritance in depth. Meyer provides an argument in favor of multiple inheritance in Chapter 15.

Riel, Arthur J. *Object-Oriented Design Heuristics*. Reading, MA: Addison-Wesley, 1996. This book contains numerous suggestions for improving program design, mostly at the class level. I avoided the book for several years because it appeared to be too big–talk about people in glass houses! However, the body of the book is only about 200 pages long. Riel’s writing is accessible and enjoyable. The content is focused and practical.

## C++

Meyers, Scott. *Effective C++: 50 Specific Ways to Improve Your Programs and Designs*, 2d ed. Reading, MA: Addison-Wesley, 1998.

Meyers, Scott, 1996, *More Effective C++: 35 New Ways to Improve Your Programs and Designs*. Reading, MA: Addison-Wesley, 1996. Both of Meyers’ books are canonical references for C++ programmers. The books are entertaining and help to instill a language-lawyer’s appreciation for the nuances of C++.

## Java

Bloch, Joshua. *Effective Java Programming Language Guide*. Boston, MA: Addison-Wesley, 2001. Bloch’s book provides much good Java-specific advice as well as introducing more general, good object-oriented practices.

## Visual Basic

The following books are good references on classes in Visual Basic:

Foxall, James. *Practical Standards for Microsoft Visual Basic .NET*. Redmond, WA: Microsoft Press, 2003.

Cornell, Gary, and Jonathan Morrison. *Programming VB .NET: A Guide for Experienced Programmers*. Berkeley, CA: Apress, 2002.

Barwell, Fred, et al. *Professional VB.NET*, 2d ed. Wrox, 2002.

## Chapter 7

## High-Quality Routines

## Contents

- 7.1 Valid Reasons to Create a Routine: page 164
- 7.2 Design at the Routine Level: page 168
- 7.3 Good Routine Names: page 171
- 7.4 How Long Can a Routine Be?: page 173
- 7.5 How to Use Routine Parameters: page 174
- 7.6 Special Considerations in the Use of Functions: page 181
- 7.7 Macro Routines and Inline Routines: page 182

## Related Topics

- Steps in routine construction: Section 9.3
- Working classes: Chapter 6
- General design techniques: Chapter 5
- Software architecture: Section 3.5

Chapter 6 described the details of creating classes. This chapter zooms in on routines, on the characteristics that make the difference between a good routine and a bad one. If you’d rather read about issues that affect the design of routines before wading into the nitty-gritty details, be sure to read Chapter 5, “Design in Construction,” first and come back to this chapter later. Some important attributes of high-quality routines are also discussed in Chapter 8, “Defensive Programming.” If you’re more interested in reading about steps to create routines and classes, Chapter 9, “The Pseudocode Programming Process,” might be a better place to start.

Before jumping into the details of high-quality routines, it will be useful to nail down two basic terms. What is a “routine”? A routine is an individual method or procedure invocable for a single purpose. Examples include a function in C++, a method in Java, a function or sub procedure in Microsoft Visual Basic. For some uses, macros in C and C++ can also be thought of as routines. You can apply many of the techniques for creating a high-quality routine to these variants.

What is a high-quality routine? That’s a harder question. Perhaps the easiest answer is to show what a high-quality routine is not. Here’s an example of a low-quality routine:

```
```cpp
void HandleStuff( CORP_DATA & inputRec, int crntQtr, EMP_DATA empRec,
    double & estimRevenue, double ytdRevenue, int screenX, int screenY,
    COLOR_TYPE & newColor, COLOR_TYPE & prevColor, StatusType & status,
    int expenseType )
{
int i;
for ( i = 0; i < 100; i++ ) {
    inputRec.revenue[i] = 0;
    inputRec.expense[i] = corpExpense[ crntQtr ][ i ];
}
UpdateCorpDatabase( empRec );
estimRevenue = ytdRevenue * 4.0 / (double) crntQtr;
newColor = prevColor;
status = SUCCESS;
if ( expenseType == 1 ) {
    for ( i = 0; i < 12; i++ )
        profit[i] = revenue[i] - expense.type1[i];
}
else if ( expenseType == 2 ) {
    profit[i] = revenue[i] - expense.type2[i];
}
else if ( expenseType == 3 ) {
    profit[i] = revenue[i] - expense.type3[i];
}
```
```

What’s wrong with this routine? Here’s a hint: you should be able to find at least 10 different problems with it. Once you’ve come up with your own list, look at the following list:

- The routine has a bad name. *HandleStuff()* tells you nothing about what the routine does.
- The routine isn’t documented. (The subject of documentation extends beyond the boundaries of individual routines and is discussed in Chapter 32, “Self-Documenting Code.”)
- The routine has a bad layout. The physical organization of the code on the page gives few hints about its logical organization. Layout strategies are used haphazardly, with different styles in different parts of the routine. Compare the styles where *expenseType == 2* and *expenseType == 3*. (Layout is discussed in Chapter 31, “Layout and Style.”)
- The routine’s input variable, *inputRec*, is changed. If it’s an input variable, its value should not be modified (and in C++ it should be declared *const*). If the value of the variable is supposed to be modified, the variable should not be called *inputRec*.
- The routine reads and writes global variables—it reads from *corpExpense* and writes to *profit*. It should communicate with other routines more directly than by reading and writing global variables.
