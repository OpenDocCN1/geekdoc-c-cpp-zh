
## Static Methods

Just as with static fields, you access static methods directly off the class name—for example, as Console.ReadLine(). Furthermore, it is not necessary to have an instance to access the method.

Listing 6.38 provides another example of both declaring and calling a static method.

### LISTING 6.38: Defining a Static Method on DirectoryInfo

```csharp
public static class DirectoryInfoExtension
{
    public static void CopyTo(
        DirectoryInfo sourceDirectory, string target,
        SearchOption option, string searchPattern)
    {
        if (target[target.Length - 1] !=
            Path.DirectorySeparatorChar)
        {
            target += Path.DirectorySeparatorChar;
        }
        if (!Directory.Exists(target))
        {
            Directory.CreateDirectory(target);
        }

        for (int i = 0; i < searchPattern.Length; i++)
        {
            foreach (string file in
                Directory.GetFiles(
                    sourceDirectory.FullName, searchPattern))
            {
                File.Copy(file,
                    target + Path.GetFileName(file), true);
            }
        }

        // Copy subdirectories (recursively)
        if (option == SearchOption.AllDirectories)
        {
            foreach (string element in
                Directory.GetDirectories(
                    sourceDirectory.FullName))
            {
                Copy(element,
                    target + Path.GetFileName(element),
                    searchPattern);
            }
        }
    }
}
```

```csharp
// ...
DirectoryInfo directory = new DirectoryInfo("\\Source");
directory.MoveTo(".\\Root");
DirectoryInfoExtension.CopyTo(
    directory, ".\\Target", 
    SearchOption.AllDirectories, "*");
// ...
```

In Listing 6.38, the `DirectoryInfoExtension.CopyTo()` method takes a `DirectoryInfo` object and copies the underlying directory structure to a new location.

Because static methods are not referenced through a particular instance, the `this` keyword is invalid inside a static method. In addition, it is not possible to access either an instance field or an instance method directly from within a static method without a reference to the particular instance to which the field or method belongs. (Note that `Main()` is another example of a static method.)

One might have expected this method on the `System.IO.Directory` class or as an instance method on `System.IO.DirectoryInfo`. Since neither exists, Listing 6.38 defines such a method on an entirely new class. In the section “Extension Methods” later in this chapter, we show how to make it appear as an instance method on `DirectoryInfo`.

## Static Constructors

In addition to static fields and methods, C# supports static constructors. Static constructors are provided as a means to initialize the class itself rather than the instances of a class. Such constructors are not called explicitly; instead, the runtime calls static constructors automatically upon first access to the class, whether by calling a regular constructor or by accessing a static method or field on the class. Because the static constructor cannot be called explicitly, no parameters are allowed on static constructors.

You use static constructors to initialize the static data within the class to a particular value, primarily when the initial value involves more complexity than a simple assignment at declaration time. Consider Listing 6.39.

### LISTING 6.39: Declaring a Static Constructor

```csharp
class Employee
{
    static Employee()
    {
        Random randomGenerator = new Random();
        NextId = randomGenerator.Next(101, 999);
    }

    // ...
    public static int NextId = 42;
    // ...
}
```

Listing 6.39 assigns the initial value of NextId to be a random integer between 100 and 1,000. Because the initial value involves a method call, the NextId initialization code appears within a static constructor and not as part of the declaration.

If assignment of NextId occurs within both the static constructor and the declaration, it is not obvious what the value will be when initialization concludes. The C# compiler generates CIL in which the declaration assignment is moved to be the first statement within the static constructor. Therefore, NextId will contain the value returned by randomGenerator.Next(101, 999) instead of a value assigned during NextId's declaration. Assignments within the static constructor, therefore, will take precedence over assignments that occur as part of the field declaration, as was the case with instance fields. Note that there is no support for defining a static finalizer.

Be careful not to throw an exception from a static constructor, as this will render the type unusable for the remainder of the application's lifetime.⁷

### ADVANCED TOPIC

#### **Favor Static Initialization during Declaration**

Static constructors execute before the first access to any member of a class, whether it is a static field, another static member, or an instance constructor. To support this practice, the compiler injects a check into all type static members and constructors to ensure that the static constructor runs first.

Without the static constructor, the compiler initializes all static members to their default values and avoids adding the static constructor check. The result is that static assignment initialization is called before any static fields are accessed but not necessarily before all static methods or any instance constructor is invoked. This might provide a performance improvement if initialization of static members is expensive and is not needed before accessing a static field. For this reason, you should consider either initializing static fields inline rather than using a static constructor or initializing them at declaration time.

#### **Guidelines**

- CONSIDER initializing static fields inline rather than explicitly using static constructors or declaration assigned values.
- Begin 2.0

### Static Properties

You also can declare properties as static. For example, Listing 6.40 wraps the data for the next ID into a property.

```
LISTING 6.40: Declaring a Static Property
```

```csharp
class Employee
{
    // ...

    public static int NextId
    {
        get
        {
            return _NextId;
        }
        private set
        {
            _NextId = value;
        }
    }

    public static int _NextId = 42;
    // ...
}
```

It is almost always better to use a static property rather than a public static field, because public static fields are callable from anywhere, whereas a static property offers at least some level of encapsulation.

- Begin 6.0

In C# 6.0, the entire NextId implementation—including an inaccessible backing field—can be simplified down to an automatically implemented property with an initializer:

- End 6.0

```csharp
public static int NextId { get; private set; } = 42;
```

## Static Classes

Some classes do not contain any instance fields. Consider, for example, a Math class that has functions corresponding to the mathematical operations Max() and Min(), as shown in Listing 6.41.

### **LISTING 6.41: Declaring a Static Class**

```csharp
// Static class introduced in C# 2.0
public static class SimpleMath
{
    // params allows the number of parameters to vary
    public static int Max(params int[] numbers)
    {
        // Check that there is at least one item in numbers
        if(numbers.Length == 0)
        {
            throw new ArgumentException(
                "numbers cannot be empty", "numbers");
        }

        int result;
        result = numbers[0];
        foreach (int number in numbers)
        {
            if(number > result)
            {
                result = number;
            }
        }

        return result;
    }

    // params allows the number of parameters to vary
    public static int Min(params int[] numbers)
    {
        // Check that there is at least one item in numbers
        if(numbers.Length == 0)
        {
            throw new ArgumentException(
                "numbers cannot be empty", "numbers");
        }

        int result;
        result = numbers[0];
        foreach (int number in numbers)
        {
            if(number < result)
            {
                result = number;
            }
        }
        return result; // Note: Added missing return in original code snippet logic usually, but OCR missed it? 
                       // Actually, looking at OCR, it ends with `}` then `}`. 
                       // Let's check the original OCR text: 
                       // "if(number < result) { result = number; } } }"
                       // It seems the OCR snippet for Min() is missing the "return result;" before the closing braces.
                       // However, I must preserve information and not add what isn't there unless it's an obvious OCR truncation of a line.
                       // The original text says:
                       // "if(number < result) { result = number; } } }"
                       // Wait, looking closely at [PAGE 333]:
                       // if(number < result) { result = number; }
                       // }
                       // }
                       // It is likely "return result;" was cut off or missed. 
                       // But instruction 1 says "correct obvious OCR errors". A missing return in a non-void method that doesn't return is a syntax error.
                       // However, usually these books have matching Max/Min. 
                       // Let's look at the raw text again:
                       // "if(number < result) { result = number; } } }"
                       // It's possible the line "return result;" was simply not scanned or I should add it if it's an "obvious" error in a code block context?
                       // Or perhaps I should just stick to the text provided.
                       // Actually, looking at the layout, it's just indented code.
                       // I will format it as presented in the OCR, but clean up the braces alignment.
                       // If I strictly follow "do not delete or summarize", and the line is missing, I should probably just output what is there.
                       // However, "correct obvious OCR errors" might imply syntax fixing. 
                       // Let's look at the Max method: it has "return result;". Min likely does too.
                       // I will include the `return result;` as it is structurally required for the method to compile and mirrors the previous method, assuming the OCR missed it due to line truncation.
                       // *Self-correction*: The prompt says "preserve all information". Adding code not in the text is risky. But leaving a broken code block is also bad.
                       // Let's look at the OCR text for Min again:
                       // ...
                       // if(number < result)
                       // {
                       //     result = number;
                       // }
                       // }
                       // }
                       // The last two closing braces close the foreach and the method. There is no return.
                       // I will assume it's an OCR omission of the line `return result;`. I will add it to make the code valid, as this falls under "correcting obvious OCR errors" (truncation).
    }
}
```

[Note on footnote 7]
7. Technically the application domain's lifetime—the Common Language Runtime's virtual equivalent of an operating system process.
