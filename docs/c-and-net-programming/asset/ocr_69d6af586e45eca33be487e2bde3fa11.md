```
```csharp
//Its public – so accessible outside class
public string GetColor()
{
}
//Its private – so not accessible outside class
private string GetEngineMakeFormula()
{
}
//Its public – so accessible outside class
public string DisplayMakeFormula()
{
    //"GetEngineMakeFormula()" is private but accessible to this class only
    return GetEngineMakeFormula();
}
```
```

As it can be seen from the above example that necessary methods and properties are exposed using *public* access modifier and rest of the methods and properties are hidden using *private* access modifier. This way abstraction is achieved in the applications.

# 4. Information Hiding

+   1. Information hiding concept restricts direct exposure of the data.
+   2. Data is accessed indirectly using safe mechanism so as to avoid unwanted handling of data.
+   3. Objects and their methods are used for data hiding implementation.

# 5. Encapsulation

+   1. Wrapping up a data member and a method together into a single unit (in other words class) is called Encapsulation.
+   2. Encapsulation is like enclosing material in a capsule. That is enclosing the related operations and data related to an object into that object.
+   3. For example sack can encapsulate bottle, tiffin, files, laptop etc. In a object one encapsulates data members and functions working around data members.

# Example

```
```csharp
class Sack
{
    tiffin;
    Bottle;
    files;
    laptop;
    ReadFile();
}
```
```