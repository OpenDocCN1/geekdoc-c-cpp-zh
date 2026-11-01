By breaking down an object system in this way before going about assigning specifics, you can clearly see which situations should use abstract classes rather than interfaces, and vice versa. The result of this example couldn't be achieved using only interfaces or only abstract inheritance.

# STRUCT TYPES

Chapter 8 noted that structs and classes are very similar but that structs are value types and classes are reference types. What does this actually mean to you? Well, the easiest way of looking at this is with an example, such as the following Try It Out.

# TRY IT OUT Classes versus Structs: Ch09Ex03\Program.cs

+   1. Create a new console application project called Ch09Ex03 and save it in the directory C:\BegVCSharp\Chapter09.
+   2. Modify the code as follows:

```
```csharp
namespace Ch09Ex03
{
    class MyClass
    {
        public int val;
    }
    struct myStruct
    {
        public int val;
    }
    class Program
    {
        static void Main(string[] args)
        {
            MyClass objectA = new MyClass();
            MyClass objectB = objectA;
            objectA.val = 10;
            objectB.val = 20;
            myStruct structA = new myStruct();
            myStruct structB = structA;
            structA.val = 30;
            structB.val = 40;
            WriteLine("objectA.val = {objectA.val}");
            WriteLine("objectB.val = {objectB.val}");
            WriteLine("structA.val = {structA.val}");
            WriteLine("structB.val = {structB.val}");
            ReadKey();
        }
    }
}
```
```