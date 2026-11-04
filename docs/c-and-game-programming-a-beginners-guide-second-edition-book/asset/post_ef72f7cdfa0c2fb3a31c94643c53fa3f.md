
### Example 5.44. User-defined exceptions.

```csharp
using System;

namespace Chapter5 {
    public class MyException : System.ApplicationException {
        public MyException(string Comment) : base(Comment) {}
    }

    public class Errors {
        static void Main() {
            Errors Er = new Errors();
            Er.TryMethod();
        }

        public void TryMethod() {
            string Input;
            int X, Y;

            Console.WriteLine("Let's divide some numbers...");

            while(true) {
                Console.Write("Enter your numerator now: ");
                Input = Console.ReadLine();

                if (char.IsNumber(Input, 0)) {
                    X = int.Parse(Input);
                } else {
                    throw new IndexOutOfRangeException("\nCharacter " +
                        "Detected where Integer Value was Expected!");
                }

                Console.Write("Enter your denominator now: ");
                Input = Console.ReadLine();

                if (char.IsNumber(Input, 0)) {
                    Y = int.Parse(Input);
                } else {
                    throw new IndexOutOfRangeException("\nCharacter " +
                        "Detected where Integer Value was Expected!");
                }

                try {
                    Console.WriteLine(X / Y);
                } catch (DivideByZeroException) {
                    Console.WriteLine("Division by Zero attempted!\n");
                }
            }
        }
    }
}
```

```csharp
Console.Write("Please enter a new denominator now: ");
Y = char.Parse(Console.ReadLine());

try {
    Console.WriteLine(X / Y);
} catch {
    Console.WriteLine("Error!");
    break;
}
} catch {
    Console.WriteLine("Error Detected");
}
}
}
}
}
```

## Nested Exceptions

In addition to creating simple try block structures, catches, and class based exceptions, we can nest those exceptions to provide an even greater level of protection. Placing a second try-catch block inside of a secondary catch exception allows us to add a third catchall block, which will execute if the error was still not contained (see Examples 5.45a and 5.45b).

### Example 5.45a. Nested exceptions.

```csharp
namespace Chapter5 {
    class Mathematics {
        public static void Division(ref int X, ref int Y) {
            if (X == 0 && Y == 0) {
                X = Y = 1;
                throw new Exception("ZeroByZeroException");
            } else
                Console.WriteLine(X/Y);
        }

        public static void Main() {
            string Input;
            int X, Y;

            Console.WriteLine("Let's divide some numbers...");

            while (true) {
                Console.Write("Enter your numerator now: ");
                Input = Console.ReadLine();
                X = int.Parse(Input);

                Console.Write("Enter your denominator now: ");
                Input = Console.ReadLine();
                Y = int.Parse(Input);

                try {
                    Division(ref X, ref Y);
                } catch (DivideByZeroException) {
                    Console.WriteLine("Attempting to divide by zero!");
                } catch (System.Exception e) {
                    Console.WriteLine(e.Message);
                    try {
                        Division(ref X, ref Y);
                    } catch {
                        Console.WriteLine("Error Detected");
                    }
                }
            }
        }
    }
}
```

### Example 5.45b. Applied exceptions.

```csharp
namespace Chapter5 {
    class Mathematics {
        public static void Division(ref int X, ref int Y) {
            if (X == 0 && Y == 0) {
                X = Y = 1;
                throw new Exception("ZeroByZeroException");
            } else
                Console.WriteLine(X/Y);
        }

        public static void Main() {
            string Input;
            int X, Y;

            Console.WriteLine("Let's divide some numbers...");

            while (true) {
                Console.Write("Enter your numerator now: ");
                Input = Console.ReadLine();

                try {
                    X = int.Parse(Input);
                } catch (System.FormatException) {
                    Console.WriteLine("\nInvalid Input Detected!");
                    continue;
                }

                Console.WriteLine("Enter your denominator now: ");
                Input = Console.ReadLine();

                try {
                    Y = int.Parse(Input);
                } catch (System.FormatException) {
                    Console.WriteLine("Invalid Input Detected - " +
                        "Calculation Terminated!\n");
                    continue;
                }

                try {
                    Division(ref X, ref Y);
                } catch (DivideByZeroException) {
                    Console.WriteLine("Attempting to divide by zero!");
                } catch (System.Exception e) {
                    Console.WriteLine(e.Message);
                    try {
                        Division(ref X, ref Y);
                    } catch {
                        Console.WriteLine("Unrecoverable Error Detected");
                    }
                }
            }
        }
    }
}
```

## The Binary Operator as

The binary operator as allows for conversion of an expression to a data type. This operator is considered a more elegant data type, since its expressions can return null data and do not call exceptions. As expressions also require reference types and are used to express a reference type or object such as the formula “expression is type,” which is also equivalent to a single call to “expression is type? (type) expression: (type) null” (see Example 5.46).

> The null reference refers to an object that has not yet been assigned; it basically serves as a blank or nonvalue, which can be substituted for later. It is also the default value to any nonassigned reference types, and can be used to mark a position where no actual reference is needed.

### Example 5.46. The binary operator as.

```csharp
using System;
namespace Chapter5 {
    public class TestAS {
        public static void Main() {
            object MyString = new object();
            MyString = 123;

            string s = MyString as string;

            if (s != null)
                Console.WriteLine(MyString);
            else
                Console.WriteLine("Test Failed!");
        }
    }
}
```

## Delegates

Delegates are objects used as references to encapsulate specific methods, which include signatures and formal return types. The delegate, while similar to the C++ function pointer, is actually type safe and considered OOP (Object-Oriented Programming) compliant. Delegates also allow for six key modifiers: new, public, protected, internal, private, and unsafe (unsafe is only used when dealing with parameters that are also pointers). Delegates are most frequently used to pass methods as parameters. Type safety is based on the matching of signatures as part of their declaration—delegates need to be declared before they are called (see Example 5.47).

### Example 5.47. A simple delegate.

```csharp
using System;

namespace Chapter5 {
    // Prototype
    public delegate void TryDelegate();

    public class Delegates {
        static void Main() {
            TryDelegate();
        }

        public static void TryDelegate() {
            Console.WriteLine("Hello World!");
        }
    }
}
```

## Events

Events are used to pass information between delegates; they are null before they are referenced, and their properties must include both an add and a remove accessor. Events are used to specify delegates and are referenced at runtime; they can include multiple methods, and are applicable to other programs. When defining events, we must make sure to include a delegate. If the event is redefined, then we'll only need to reference that delegate (see Example 5.48).

### Example 5.48. Events.

```csharp
using System.Collections;

namespace Chapter5 {
    public delegate void TryDelegate(int i);

    public class EventSetup {
        private Hashtable Test = new Hashtable();

        public event TryDelegate Event {
            add {
                Test["Event"] = (TryDelegate)Test["Event"] + value;
            }
            remove {
                Test["Event"] = (TryDelegate)Test["Event"] - value;
            }
        }
    }

    public class Events {
        public static void Main() {
        }
    }
}
```

## Preprocessor Directives

Preprocessor directives redirect and/or skip different portions of coding. This becomes necessary for a number of complex reasons, but the actual application of these directives are rather simple. For example, we can define an area of coding, insert clauses for execution, and include error warnings and/or data filters allowing us to test specific aspects and/or troubleshoot otherwise untestable clauses. The most commonly used preprocessor directives are the #region and #endregion markers, which are a special set of directives that can hide previously tested or otherwise cumbersome coding to allow the programmer a more comfortable view of the applications at hand. For a complete list of preprocessor definitions, see Table 5.2 (also see Example 5.49).

### Example 5.49. Implementing preprocessor directives.

```csharp
#define DebugTest
#define ReleaseTest

#if DebugTest
#undef DebugTest
#elif ReleaseTest
#warning "This is a warning!"
#else
#error "Error Detected"
#endif

using System;
namespace Chapter5 {
    class Class1 {
        static void Main() {}
    }
}
```
