
### Example B.47.

```csharp
public class Appendix_B {
    public static void Params(params string[] list) {
    }
    public static void Main() {
    }
}
```

## private, protected, and public

Private, protected, and public are class or structure members that allow for restricted or limited access based on user-defined methods written specifically for those values. These user-defined methods are declared as part of that class' internal structure (see Examples B.48–B.50).

### Example B.48.

```csharp
namespace Appendix_B {
    class BankAccount {
        private string first_name;
        private void ReadFiles(ref BankAccount acc) {}
        static void Main() {}
    }
}
```

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_484_0.png)

> Note: While private is the default setting, many programmers choose to explicitly restate that command to remove any ambiguity.

### Example B.49.

```csharp
namespace Appendix_B {
    class BankAccount {
        protected string first_name;
        protected void ReadFiles(ref BankAccount acc) {}
        static void Main() {}
    }
}
```

### Example B.50.

```
namespace Appendix_B {
    class BankAccount {
        public string first_name;
        public void ReadFiles(ref BankAccount acc) {}
        static void Main() {}
    }
}
```

## readonly

Readonly is a constant data type used as part of a class reference declared as a field. It is assignable at only one point in the program and then acts as a constant (see Example B.51).

### Example B.51.

```
class Appendix_B {
    public readonly double variable2 = 3.14159;
    static void Main() {}
}
```

## ref

The keyword ref is used to reflect a variable's control back to the original parameters, thereby allowing the method's, or function's, alterations to be known by the main or calling body (see Example B.52).

### Example B.52.

```
class Appendix_B {
    static void Main() {
        int iNumber1 = 0;
        TheRace(ref iNumber1);
    }
    static void TheRace(ref int Num) {}
}
```

## return

The keyword return is used to pass back a single value to that of the calling function. The value in question must be the qualified type, and in cases where the returning type is void, it can be omitted. Return statements are required with all nonvoid user-defined functions and methods (see Example B.53).

### Example B.53.

```csharp
using System;
class Appendix_B {
    static void Main() {
        RandomNumber();
    }

    static int RandomNumber() {
        return(0);
    }
}
```

## sbyte

The keyword sbyte is an 8-bit integer used to store values ranging from -128 to 127 (see Example B.54).

### Example B.54.

```csharp
class Appendix_B {
    static void Main() {
        sbyte Number1 = 1;
    }
}
```

## sealed

Once a class is sealed, it can no longer be inherited, hence it cannot be overridden or altered in any other way. For the same reason, we cannot use sealed with the abstract modifier (see Example B.55).

### Example B.55.

```csharp
sealed class Appendix_B {
    static void Main() { }
}
```

## short

The keyword short is a 16-bit integer data type used to store values ranging from -32,768 to 32,767 (see Example B.56).

### Example B.56.

```csharp
class Appendix_B {
    static void Main() {
        short Number1 = 1;
    }
}
```

## sizeof

The sizeof keyword is used to gather information pertaining to the size of our data types. Unfortunately, this also requires the use of a secondary command, unsafe, which is used to mark the unsafe nature of that code (see Example B.57).

### Example B.57.

```csharp
using System;
class Appendix_B {
    static unsafe void Main() {
        Console.WriteLine ("Byte = " + sizeof(byte));
    }
}
```

## stackalloc

The keyword stackalloc (stack allocating), is used to allocate blocks of memory referenced from a stack. The addresses of these blocks are stored as pointers and they are protected from garbage collection, thus they do not have to be fixed/pinned. Note: All blocks are lost when their methods are terminated (see Example B.58).

### Example B.58.

```csharp
class Appendix_B {
    public static unsafe void Main() {
        int* pointer1 = stackalloc int[3];
        pointer1[0] = 1;
    }
}
```

## static

The keyword static is used to modify constructors, fields, methods, operators, and properties. Static constructors, for example, are called automatically, and are used to initialize the rest of the class before any members are referenced. Static fields, then, are not part of a specific instance, and instead are referenced as a single memory address.

### Example B.59.

```
class Appendix_B {
    static void Main() {}
}
```

## string

A string is a reference data type that encompasses the more recently developed unicode characters. These characters can be transferred to string references using simple quotation marks, these expressions can also be made literal by first noting them with the @ symbol (see Example B.60).

### Example B.60.

```
class Appendix_B {
    static void Main() {
        string MyDog = "Brownie";
    }
}
```

## struct

Structures (struct) are user-defined data types that allow for groupings of similar or related data that do not have a single base data type. These groups can include all the basic value data-types as well as a list of methods used to manipulate those values. The data types declared inside a structure are referred to as the structure's members (or fields), while their declarations are referred to as its instances. The correlations between these internal values and structures are usually guided by some common theme or purpose. A structure is made up of the keyword struct, the structure's tag (or name); a list of the fields (written as declared members); and a list of possible methods used to manipulate that data. Structures are generally contained within a single block placed inside our referencing namespace, but as shown in Example B.61, they can also be used to invoke the main method.

Note that while the use of a C++ style terminating semicolon is allowed, it is not required when working with C#.

### Example B.61.

```
struct Appendix_B {
    static void Main() {}
}
```

## switch

The switch statement, like the if and else-if statements, is used to execute a statement or set of statements that equal the variable's value. However, unlike the if and else-if statements, the switch statement doesn't use comparison operators; instead, it simply reads the value of the variable and attempts to direct the program to the proper channel. A second keyword, case, is also used in this process. The keyword case is written and used multiple times from within the switch statement. Each case statement holds a numeric or character value for comparison. If the value held by a case statement matches the value read by the switch statement, then everything following that case statement will be executed.

### Example B.62.

```
class Appendix_B {
    static void Main() {
        int Grades = 1;
        switch (Grades) {
            case 1:
                break;
            default:
                break;
        }
    }
}
```

## this

The keyword this is a specialized reference signature used to indicate the referencing object of a passing class; in other words, it is a longhand version for the otherwise abbreviated member. While the this reference is implied, its definitions can become ambiguous and should be included to prevent this error (see Example B.63).

### Example B.63.

```csharp
class Appendix_B {
    protected short pin_number;
    private void ReadFiles() {
        this.pin_number = 1;
    }
    static void Main() {}
}
```

## throw

In addition to being able to catch both generalized and specific exceptions, we can also learn to throw a few of our own. This is not usually necessary for the context of this book, but the technique can serve to clarify the definitions of some otherwise confusing errors (see Example B.64).

### Example B.64.

```csharp
using System;
public class Appendix_B {
    static void Main() {
        int Y = 0;
        if (Y == 0) {
            throw new DivideByZeroException("\nProgram Error!");
        }
    }
}
```

## true

A user-defined Boolean type operator that returns the value true (see Example B.65).

### Example B.65.

```csharp
class Appendix_B {
    static void Main() {
        bool Variable1 = true;
    }
}
```

## try

When it comes to user input, we can never guarantee the results, therefore, we need to think ahead and plan for possible errors. The try block scenario is a test application that is used in
