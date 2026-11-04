in line 41 returns the string "value" and the expression `nameof(Hour)` in line 42 returns the string "Hour".

# Good Programming Practice 10.1

*When you need to include an identifier in a string literal, use the nameof operator rather than hard coding the identifier's name in the string. If you right click an identifier in Visual Studio then use the Rename... option to change the identifier's name throughout your code, the string that nameof returns will be updated automatically with the identifier's new name.*

# Notes Regarding Class Time2's Methods, Properties and Constructors

Time2's properties are accessed throughout the class's body---SetTime assigns values to Hour, Minute and Second in lines 25-27, and ToUniversalString and ToString use properties Hour, Minute and Second in line 89 and lines 93-94, respectively. These methods could access the class's private data directly. However, consider changing the time's representation from three int values (requiring 12 bytes of memory) to one int value representing the total number of elapsed seconds since midnight (requiring only four bytes of memory). If we make this change, only code that accesses the private data directly would need to change---for class Time2, the bodies of properties Hour, Minute and Second. There would be no need to modify SetTime, ToUniversalString or ToString, because they access the private data indirectly through Hour, Minute and Second. Designing a class in this manner reduces the likelihood of programming errors when altering the class's implementation.

Similarly, each constructor could include a copy of the appropriate statements from method SetTime. Doing so may be slightly more efficient, because the extra constructor call and the call to SetTime are eliminated. However, duplicating statements in multiple methods or constructors makes changing the class's internal data representation more difficult and error-prone. Having one constructor call the other or even call SetTime directly allows any changes to SetTime's implementation to be made only once.

# Software Engineering Observation 10.7

*When implementing a method of a class, using the class's properties to access the class's private data simplifies code maintenance and reduces the likelihood of errors.*

# 10.5.2 Using Class Time2's Overloaded Constructors

Class Time2Test (Fig. 10.6) creates six Time2 objects (lines 9-13 and 41) to invoke the overloaded Time2 constructors.

```
```csharp
1 // Fig. 10.6: Time2Test.cs
2 // Overloaded constructors used to initialize Time2 objects.
3 using System;
4
5 public class Time2Test
6 {
```
```

Fig. 10.6 | Overloaded constructors used to initialize Time2 objects. (Part 1 of 3.)