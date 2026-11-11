
Returns a new `Integer` object initialized to the integer whose digits are contained in the string `s`. The string must represent an integer in base 10 (for the first method) or in the base given by the `radix` parameter (for the second method).

### `java.text.NumberFormat` 1.1

- `Number parse(String s)` returns the numeric value, assuming the specified `String` represents a number.

## 5.5 Methods with a Variable Number of Parameters

It is possible to provide methods that can be called with a variable number of parameters. (These are sometimes called “varargs” methods.)

You have already seen such a method: `printf`. For example, the calls

```java
System.out.printf("%d", n);
```

and

```java
System.out.printf("%d %s", n, "widgets");
```

both call the same method, even though one call has two parameters and the other has three.

The `printf` method is defined like this:

```java
public class PrintStream
{
    public PrintStream printf(String fmt, Object... args)
    {
        return format(fmt, args);
    }
}
```

Here, the ellipsis `...` is part of the Java code. It denotes that the method can receive an arbitrary number of objects (in addition to the `fmt` parameter).

The `printf` method actually receives two parameters: the format string and an `Object[]` array that holds all other parameters. (If the caller supplies integers or other primitive type values, autoboxing turns them into objects.) It now faces the unenviable task of scanning the `fmt` string and matching up the ith format specifier with the value `args[i]`.

In other words, for the implementor of `printf`, the `Object...` parameter type is exactly the same as `Object[]`.

The compiler needs to transform each call to `printf`, bundling the parameters into an array and autoboxing as necessary:

```java
System.out.printf("%d %s", new Object[] { Integer.valueOf(n),
        "widgets" });
```

You can define your own methods with variable parameters, and you can specify any type for the parameters, even a primitive type. Here is a simple example: a function that computes the maximum of a variable number of values.

```java
public static double max(double... values)
{
    double largest = Double.NEGATIVE_INFINITY;
    for (double v : values) if (v > largest) largest = v;
    return largest;
}
```

Simply call the function like this:

```java
double m = max(3.1, 40.4, -5);
```

The compiler passes a new `double[] { 3.1, 40.4, -5 }` to the `max` function.

**NOTE:**

It is legal to pass an array as the last parameter of a method with variable parameters. For example:

```java
System.out.printf("%d %s", new Object[] { Integer.valueOf(1),
        "widgets" });
```

Therefore, you can redefine an existing function whose last parameter is an array to a method with variable parameters, without breaking any existing code. For example, `MessageFormat.format` was enhanced in this way in Java 5. If you like, you can even declare the `main` method as

```java
public static void main(String... args)
```

## 5.6 Abstract Classes

As you move up the inheritance hierarchy, classes become more general and probably more abstract. At some point, the ancestor class becomes *so* general that you think of it more as a basis for other classes than as a class with specific instances you want to use. Consider, for example, an extension of our `Employee` class hierarchy. An employee is a person, and so is a student. Let us extend our class hierarchy to include classes `Person` and `Student`. Figure 5.2 shows the inheritance relationships between these classes.

![](img/0e7b74ef51a065c077b42cd87b362288_392_0.png)

**Figure 5.2** Inheritance diagram for `Person` and its subclasses

Why bother with so high a level of abstraction? There are some attributes that make sense for every person, such as a name. Both students and employees have names, and introducing a common superclass lets us factor out the `getName` method to a higher level in the inheritance hierarchy.

Now let’s add another method, `getDescription`, whose purpose is to return a brief description of the person, such as

```
an employee with a salary of $50,000.00
a student majoring in computer science
```

It is easy to implement this method for the `Employee` and `Student` classes. But what information can you provide in the `Person` class? The `Person` class knows nothing about the person except the name. Of course, you could implement `Person.getDescription()` to return an empty string. But there is a better way. If you use the `abstract` keyword, you do not need to implement the method at all.

```java
public abstract String getDescription();
// no implementation required
```

For added clarity, a class with one or more abstract methods must itself be declared abstract.

```java
public abstract class Person
{
    . . .
    public abstract String getDescription();
}
```

In addition to abstract methods, abstract classes can have fields and concrete methods. For example, the `Person` class stores the name of the person and has a concrete method that returns it.

```java
public abstract class Person
{
    private String name;

    public Person(String name)
    {
        this.name = name;
    }

    public abstract String getDescription();

    public String getName()
    {
        return name;
    }
}
```

![](img/0e7b74ef51a065c077b42cd87b362288_393_0.png)

> **TIP:**
>
> Some programmers don’t realize that abstract classes can have concrete methods. You should always move common fields and methods (whether abstract or not) to the superclass (whether abstract or not).

Abstract methods act as placeholders for methods that are implemented in the subclasses. When you extend an abstract class, you have two choices. You can leave some or all of the abstract methods undefined; then, you must tag the subclass as abstract as well. Or, you can define all methods, and the subclass is no longer abstract.

For example, we will define a `Student` class that extends the abstract `Person` class and implements the `getDescription` method. None of the methods of the `Student` class are abstract, so it does not need to be declared as an abstract class.

A class can even be declared as abstract though it has no abstract methods.

Abstract classes cannot be instantiated. That is, if a class is declared as abstract, no objects of that class can be created. For example, the expression

```java
new Person("Vince Vu")
```

is an error. However, you can create objects of concrete subclasses.

Note that you can still create *object variables* of an abstract class, but such a variable must refer to an object of a nonabstract subclass. For example:

```java
Person p = new Student("Vince Vu", "Economics");
```

Here `p` is a variable of the abstract type `Person` that refers to an instance of the nonabstract subclass `Student`.

![](img/0e7b74ef51a065c077b42cd87b362288_394_0.png)

**C++ NOTE:**

In C++, an abstract method is called a *pure virtual function* and is tagged with a trailing `= 0`, such as in

```cpp
class Person // C++
{
public:
    virtual string getDescription() = 0;
    ...
};
```

A C++ class is abstract if it has at least one pure virtual function. In C++, there is no special keyword to denote abstract classes.

Let us define a concrete subclass `Student` that extends the abstract class `Person`:

```java
public class Student extends Person
{
    private String major;

    public Student(String name, String major)
    {
        super(name);
        this.major = major;
    }

    public String getDescription()
    {
        return "a student majoring in " + major;
    }
}
```

The `Student` class defines the `getDescription` method. Therefore, all methods in the `Student` class are concrete, and the class is no longer an abstract class.

The program shown in Listing 5.8 defines the abstract superclass `Person` (Listing 5.9) and two concrete subclasses, `Employee` (Listing 5.10) and `Student` (Listing 5.11). We fill an array of `Person` references with employee and student objects:

```java
var people = new Person[2];
people[0] = new Employee(...);
```
