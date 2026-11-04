
In conjunction with several catch responses. The information in question is placed between the try block’s parameters and is given only one chance to succeed (see Example B.66).

## Example B.66.
```csharp
public class Appendix_B {
    static void Main() {
        try{}
        catch{}
        finally{}
    }
}
```

## typeof
The typeof operator is used to determine an object’s type, fields, methods, properties (see Example B.67)

### Example B.67.
```csharp
using System;
namespace Appendix_B {
    public class Class1 {
        public static void Main() {
            Type Ob = typeof(Class1);
            Console.WriteLine(Ob.GetFields());
            Console.WriteLine(Ob.GetMethods());
        }
    }
}
```

## uint
The keyword uint is an unsigned 32-bit integral type used to store values ranging from 0 to 4,294,967,295 (see Example B.68).

### Example B.68.
```csharp
class Appendix_B {
    static void Main() {
        uint Number1 = 1;
    }
}
```

## ulong
The keyword ulong denotes an unsigned 64-bit integral type used to store values ranging from 0 to 18,446,744,073,709,551,615 (see Example B.69).

### Example B.69.
```csharp
class Appendix_B {
    static void Main() {
        ulong Number1 = 1;
    }
}
```

## unchecked
The keyword unchecked is used to block the Solution Explorer\Configuration Properties\Build\Check for an arithmetic overflow/underflow true statement. This statement is false by default, but if we were to change this default and then attempt to break the barriers of our designated type, we could block the error with the unchecked statement (see Example B.70).

### Example B.70.
```csharp
class Appendix_B {
    static void Main () {
        byte Max255 = 255;
        unchecked {Max255 += 1 ;}
    }
}
```

## unsafe
The keyword unsafe denotes a change in settings to unsafe mode. The unsafe feature was developed to aid in bridging the gap between C++ and C# programming, allowing us to use time tested techniques that are not officially permitted under C#'s safe mode (see Example B.72). In addition to including the keyword unsafe to our coding, we must also change the compiler's settings in Configuration Manager (see Chapter 1—Sizeof and Unsafe Coding for details).

### Example B.71.
```csharp
class Class1 {
    static unsafe void Main() {}
}
```

## ushort
The keyword ushort denotes a 16-bit integral data type used to store values ranging from 0 to 65,535 (see Example B.72).

### Example B.72.
```csharp
class Appendix_B {
    static void Main() {
        ushort Number1 = 1;
    }
}
```

## using
The using directive allows us to include a host of system and user-defined namespaces including a namespace is not equivalent to including a file, as was done in C++. Here, we'll only be notifying the compiler of where to find the references written in shorthand. User-defined namespaces are accessed in exactly the same manner as the system type (see Example B.73).

### Example B.73.
```csharp
using System;
class Appendix_B {
    static void Main() {}
}
```

## virtual
The keyword virtual denotes a modifier that sets a method of a base class so that it can be overridden in a derived class. When a virtual function is referenced, it searches for an overriding method.

### Example B.74.
```csharp
namespace Appendix_B {
    public class Area {
        public Area() {}
        public virtual void CalculateArea() {}
    }
    public class Parallelogram : Area {
        public Parallelogram() {}
        override public void CalculateArea() {}
    }
    static void Main() {}
}
```

## void
Void is a data type that holds no data, thus, serves the purpose of telling the compiler that no data will be required by this variable or returning function. This is logical, since the ending of the main function is also the ending of the program and there would be no program to which information could be sent. Void is also most commonly associated with user-defined functions that use reference-variables (explained in Chapter 2) and generalized pointers-variables (explained in Chapter 4). Unlike the other data types, Void does not take a position in memory, therefore, we won't need to measure its size in bytes.

### Example B.75.
```csharp
class Appendix_B {
    static void Main(){}
}
```

## volatile
The keyword volatile is used to denote a variable that cannot be optimized, which is usually due to some unpredictable change or reference made to it, frequently from an outside source such as the operating system or hardware device (see Example B.76).

### Example B.76.
```csharp
class Appendix_B {
    public volatile char variable3 = 'A';
    static void Main(){}
}
```

## while
The while loop can be set up to repeat and/or terminate in several different ways. The most common include using a predetermined count (as in to repeat an iteration five times then end) according to the user's input (end by request), and a termination command (a command that short-circuits or breaks the loop—see Example B.77).

### Example B.77.
```csharp
class Appendix_B {
    static void Main() {
        while(true){}
    }
}
```

## Appendix C: Accessors

### get & set
The get and set accessors aren't officially keywords, rather, they are parameterless methods named to match certain fields and used in classes and interfaces that hold a body of executable data pertaining to the storage and retrieval of those fields. Their executable statements may include calculations, conversions, and a large host of other tasks, but their underlying purpose must include reading or recording to those properties. The body of an accessor is considered equivalent to a method although they do not include identity signatures. The get accessor returns a value and may be set to throw a value when needed; in contrast, the set accessor is always set to void. The keyword value is also used as an implicit parameter with setting fields, thus it takes on the value of any passed variables. The get and set accessors always share the same user-defined name, thus they cannot exist in the same base class. It is then considered natural to place the set accessor in the base class with the get accessor listed in the next derived class. It is also important to remember that the value retrieved by the get property is for reference only, while the value recorded in the set property is write only (see Example C.1).

### Example C.1.
```csharp
namespace Appendix_C {
    public class BaseClass {
        public short width;
        protected BaseClass() {}
        public short Width {set{width = value;}}
    }
    public class DerivedClass : BaseClass {
        protected DerivedClass() {}
        public new short Width {get{return(width);}}
        static void Main() {}
    }
}
```

### value
value types are implicit fields declared as part of a methods signature, and are referenced as if they were actual fields. They have the same limitations and abilities associated with a field of their declared type and should be treated as such (see Example C.2).

### Example C.2.
```csharp
namespace Appendix_C {
    public class Objects {
        int Number;
        public Objects(int value) {
            this.Number = value;
        }
        static void Main() {}
    }
}
```

## Appendix D: Order of Precedence

| Symbol(s) | Description |
|---|---|
| `.` | Dot operator |
| `[]` | Array indexing |
| `()` | Function call |
| `++` | Postfix increment operator (placed after the variable) |
| `--` | Postfix decrement operator (placed after the variable) |
| `new, typeof` |  |
| `checked, unchecked` |  |
| `++` | Prefix increment operator (placed before the variable) |
| `--` | Prefix decrement operator (placed before the variable) |
| `!` | Not |
| `-` | Unary minus |
| `+` | Unary Plus |
| `~` | Unary |
| `(T)x` |  |
| `*` | Multiply |
| `/` | Divide |
| `%` | Remainder |
| `+` | Addition |
| `-` | Subtraction |
| `<<` | Shift |
| `>>` | Shift |
| `<` | Less than |
| `>` | Greater than |
| `<=` | Less than or equal to |
| `>=` | Greater than or equal to |
| `as, is` |  |
| `==` | Equal to |
| `!=` | Not equal to |
| `&` | Logical AND |
| `^` | Logical XOR |
| `|` | Logical OR |
| `&&` | And |
| `||` | Or |
| `?:` | If |
| `= += -= *= /= %=` | Assignment, add, subtract, multiply, divide, remainder... |
| `/= %= <<= >>= ` |  |
| `|= &= ^=` |  |
