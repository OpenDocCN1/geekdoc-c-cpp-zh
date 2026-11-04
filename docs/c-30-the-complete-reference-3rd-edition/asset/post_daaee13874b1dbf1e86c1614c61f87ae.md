
// Construct array given its size.
public RangeArray(int low, int high) {
    high++;
    if(high <= low) {
        throw new RangeArrayException("Low index not less than high.");
    }
    a = new int[high - low];
    Length = high - low;
    lowerBound = low;
    upperBound = --high;
}

// This is the indexer for RangeArray.
public int this[int index] {
    // This is the get accessor.
    get {
        if(ok(index)) {
            return a[index - lowerBound];
        } else {
            throw new RangeArrayException("Range Error.");
        }
    }

    // This is the set accessor.
    set {
        if(ok(index)) {
            a[index - lowerBound] = value;
        } else throw new RangeArrayException("Range Error.");
    }
}

// Return true if index is within bounds.
private bool ok(int index) {
    if(index >= lowerBound && index <= upperBound) return true;
    return false;
}

// Demonstrate the index-range array.
class RangeArrayDemo {
    static void Main() {
        try {
            RangeArray ra = new RangeArray(-5, 5);
            RangeArray ra2 = new RangeArray(1, 10);

            // Demonstrate ra.
            Console.WriteLine("Length of ra: " + ra.Length);

            for(int i = -5; i <= 5; i++)
                ra[i] = i;
            Console.Write("Contents of ra: ");
            for(int i = -5; i <= 5; i++)
                Console.Write(ra[i] + " ");
            Console.WriteLine("\n");

            // Demonstrate ra2.
            Console.WriteLine("Length of ra2: " + ra2.Length);

            for(int i = 1; i <= 10; i++)
                ra2[i] = i;

            Console.Write("Contents of ra2: ");
            for(int i = 1; i <= 10; i++)
                Console.Write(ra2[i] + " ");

            Console.WriteLine("\n");
        } catch (RangeArrayException exc) {
            Console.WriteLine(exc);
        }

        // Now, demonstrate some errors.
        Console.WriteLine("Now generate some range errors.");

        // Use an invalid constructor.
        try {
            RangeArray ra3 = new RangeArray(100, -10); // Error
        } catch (RangeArrayException exc) {
            Console.WriteLine(exc);
        }

        // Use an invalid index.
        try {
            RangeArray ra3 = new RangeArray(-2, 2);

            for(int i = -2; i <= 2; i++)
                ra3[i] = i;

            Console.Write("Contents of ra3: ");
            for(int i = -2; i <= 10; i++) // generate range error
                Console.Write(ra3[i] + " ");
        } catch (RangeArrayException exc) {
            Console.WriteLine(exc);
        }
    }
}
The output from the program is shown here:

Length of ra: 11
Contents of ra: -5 -4 -3 -2 -1 0 1 2 3 4 5
```
Length of ra2: 10
Contents of ra2: 1 2 3 4 5 6 7 8 9 10

Now generate some range errors.
Low index not less than high.
Contents of ra3: -2 -1 0 1 2 Range Error.
```
When a range error occurs, RangeArray throws an object of type RangeArrayException. Notice there are three places in RangeArray that this might occur: in the get indexer accessor, in the set indexer accessor, and by the RangeArray constructor. To catch these exceptions implies that RangeArray objects must be constructed and accessed from within a try block, as the program illustrates. By using an exception to report errors, RangeArray now acts like one of C#’s built-in types and can be fully integrated into a program’s exception-handling mechanism.

Notice that none of the RangeArrayException constructors provide any statements in their body. Instead, they simply pass their arguments along to Exception via base. As explained, in cases in which your exception class does not add any functionality, you can simply let the Exception constructors handle the process. There is no requirement that your derived class add anything to what is inherited from Exception.

Before moving on, you might want to experiment with this program a bit. For example, try commenting-out the override of ToString() and observe the results. Also, try creating an exception using the default constructor, and observe what C# generates as its default message.

## Catching Derived Class Exceptions

You need to be careful how you order catch clauses when trying to catch exception types that involve base and derived classes, because a catch for a base class will also match any of its derived classes. For example, because the base class of all exceptions is Exception, catching Exception catches all possible exceptions. Of course, using catch without an exception type provides a cleaner way to catch all exceptions, as described earlier. However, the issue of catching derived class exceptions is very important in other contexts, especially when you create exceptions of your own.

If you want to catch exceptions of both a base class type and a derived class type, put the derived class first in the catch sequence. This is necessary because a base class catch will also catch all derived classes. Fortunately, this rule is self-enforcing because putting the base class first causes a compile-time error.

The following program creates two exception classes called ExceptA and ExceptB. ExceptA is derived from Exception. ExceptB is derived from ExceptA. The program then throws an exception of each type. For brevity, the custom exceptions supply only one constructor (which takes a string that describes the exception). But remember, in commercial code, your custom exception classes will normally provide all four of the constructors defined by Exception.

```
// Derived exceptions must appear before base class exceptions.

using System;

// Create an exception.
class ExceptA : Exception {
    public ExceptA(string str) : base(str) { }

    public override string ToString() {
        return Message;
    }
}

// Create an exception derived from ExceptA.
class ExceptB : ExceptA {
    public ExceptB(string str) : base(str) { }

    public override string ToString() {
        return Message;
    }
}

class OrderMatters {
    static void Main() {
        for(int x = 0; x < 3; x++) {
            try {
                if(x==0) throw new ExceptA("Caught an ExceptA exception");
                else if(x==1) throw new ExceptB("Caught an ExceptB exception");
                else throw new Exception();
            }
            catch (ExceptB exc) {
                Console.WriteLine(exc);
            }
            catch (ExceptA exc) {
                Console.WriteLine(exc);
            }
            catch (Exception exc) {
                Console.WriteLine(exc);
            }
        }
    }
}
```
The output from the program is shown here:

```
Caught an ExceptA exception
Caught an ExceptB exception
System.Exception: Exception of type 'System.Exception' was thrown.
    at OrderMatters.Main()
```

Notice the type and order of the catch clauses. This is the only order in which they can occur. Since ExceptB is derived from ExceptA, the catch for ExceptB must be before the one for ExceptA. Similarly, the catch for Exception (which is the base class for all exceptions) must appear last. To prove this point for yourself, try rearranging the catch clauses. Doing so will result in a compile-time error.

One good use of a base class catch clause is to catch an entire category of exceptions. For example, imagine you are creating a set of exceptions for some device. If you derive all of the exceptions from a common base class, then applications that don't need to know precisely what problem occurred could simply catch the base class exception, avoiding the unnecessary duplication of code.

## Using checked and unchecked

A special feature in C# relates to the generation of overflow exceptions in arithmetic computations. As you know, it is possible for some types of arithmetic computations to produce a result that exceeds the range of the data type involved in the computation. When this occurs, the result is said to overflow. For example, consider the following sequence:

```
byte a, b, result;
a = 127;
b = 127;

result = (byte) (a * b);
```

Here, the product of a and b exceeds the range of a byte value. Thus, the result overflows the type of the result.

C# allows you to specify whether your code will raise an exception when overflow occurs by using the keywords checked and unchecked. To specify that an expression be checked for overflow, use checked. To specify that overflow be ignored, use unchecked. In this case, the result is truncated to fit into the target type of the expression.

The checked keyword has these two general forms. One checks a specific expression and is called the operator form of checked. The other checks a block of statements and is called the statement form.

```
checked (expr)

checked {
  // statements to be checked
}
```

Here, expr is the expression being checked. If a checked expression overflows, then an OverflowException is thrown.

The unchecked keyword also has two general forms. The first is the operator form, which ignores overflow for a specific expression. The second ignores overflow for a block of statements.

```
unchecked (expr)

unchecked {
  // statements for which overflow is ignored
}
```

Here, expr is the expression that is not being checked for overflow. If an unchecked expression overflows, then truncation will occur.

Here is a program that demonstrates both checked and unchecked:

```
// Using checked and unchecked.

using System;

class CheckedDemo {
  static void Main() {
    byte a, b;
```
