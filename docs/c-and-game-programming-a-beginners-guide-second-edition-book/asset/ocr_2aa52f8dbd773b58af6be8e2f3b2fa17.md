# Example B.63.

```
```csharp
class Appendix_B {
    protected short pin_number;
    private void ReadFiles() {
        this.pin_number = 1;
    }
    static void Main() {}
}
```
```

# throw

In addition to being able to catch both generalized and specific exceptions, we can also learn to throw a few of our own. This is not usually necessary for the context of this book, but the technique can serve to clarify the definitions of some otherwise confusing errors (see Example B.64).

# Example B.64.

```
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
```

# true

A user-defined Boolean type operator that returns the value true (see Example B.65).

# Example B.65.

```
```csharp
class Appendix_B {
    static void Main() {
        bool Variable1 = true;
    }
}
```
```

# try

When it comes to user input, we can never guarantee the results, therefore, we need to think ahead and plan for possible errors. The try block scenario is a test application that is used in