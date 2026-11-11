
## 8.1 Why Generic Programming?

*Generic programming* means writing code that can be reused for objects of many different types. For example, you don’t want to program separate classes to collect `String` and `File` objects. And you don’t have to—the single class `ArrayList` collects objects of any class. This is one example of generic programming.

Actually, Java had an `ArrayList` class before it had generic classes. Let us investigate how the mechanism for generic programming has evolved, and what that means for users and implementors.

### 8.1.1 The Advantage of Type Parameters

Before generic classes were added to Java, generic programming was achieved with *inheritance*. The `ArrayList` class simply maintained an array of `Object` references:

```java
public class ArrayList // before generic classes
{
    private Object[] elementData;
    . . .
    public Object get(int i) { . . . }
    public void add(Object o) { . . . }
}
```

This approach has two problems. A cast is necessary whenever you retrieve a value:

```java
ArrayList files = new ArrayList(); . . .
String filename = (String) files.get(0);
```

Moreover, there is no error checking. You can add values of any class:

```java
files.add(new File(". . ."));
```

This call compiles and runs without error. Elsewhere, casting the result of `get` to a `String` will cause an error.

Generics offer a better solution: *type parameters*. The `ArrayList` class now has a type parameter that indicates the element type:

```java
var files = new ArrayList<String>();
```

This makes your code easier to read. You can tell right away that this particular array list contains `String` objects.

**NOTE:**

If you declare a variable with an explicit type instead of `var`, you can omit the type parameter in the constructor by using the “diamond” syntax:

```java
ArrayList<String> files = new ArrayList<>();
```

The omitted type is inferred from the type of the variable.

Java 9 expands the use of the diamond syntax to situations where it was previously not accepted. For example, you can now use diamonds with anonymous subclasses:

```java
ArrayList<String> passwords = new ArrayList<>() // diamond OK in Java 9
{
    public String get(int n)
    {
        return super.get(n).replaceAll(".", "*");
    }
};
```

The compiler can make good use of the type information too. No cast is required for calling `get`. The compiler knows that the return type is `String`, not `Object`:

```java
String filename = files.get(0);
```

编译器还知道 `ArrayList<String>` 的 `add` 方法有一个 `String` 类型的参数。这比使用 `Object` 参数安全得多。现在编译器可以检查你不会插入错误类型的对象。例如，下面这条语句

```java
files.add(new File(". . .")); // 只能向 ArrayList<String> 添加 String 对象
```

无法编译。编译器错误比运行时类转换异常要好得多。

这就是类型参数的吸引力：它们让你的程序更易读、更安全。

### 8.1.2 谁想成为泛型程序员？

使用像 `ArrayList` 这样的泛型类很容易。大多数 Java 程序员会直接使用 `ArrayList<String>` 这样的类型，就好像它们已经内建到语言中一样，就像 `String[]` 数组那样。（当然，数组列表比数组更好，因为它们可以自动扩展。）

然而，实现一个泛型类并不容易。使用你代码的程序员会想为你的类型参数插入各种类。他们会期望一切都能正常工作，没有繁琐的限制和令人困惑的错误消息。因此，作为一名泛型程序员，你的工作是预见你的类的所有潜在未来用途。

这能有多难？这里有一个标准类库设计者必须应对的典型问题。`ArrayList` 类有一个方法 `addAll`，用于添加另一个集合的所有元素。程序员可能想将 `ArrayList<Manager>` 中的所有元素添加到 `ArrayList<Employee>` 中。但是，当然，反过来做不应该合法。你如何允许一个调用而禁止另一个？Java 语言设计者发明了一个巧妙的新概念——*通配符类型*，来解决这个问题。通配符类型相当抽象，但它们允许库构建者使方法尽可能灵活。

Generic programming falls into three skill levels. At a basic level, you just use generic classes—typically, collections such as `ArrayList`—without thinking how and why they work. Most application programmers will want to stay at that level until something goes wrong. You may, however, encounter a confusing error message when mixing different generic classes, or when interfacing with legacy code that knows nothing about type parameters; at that point, you’ll need to learn enough about Java generics to solve problems systematically rather than through random tinkering. Finally, of course, you may want to implement your own generic classes and methods.

Application programmers probably won’t write lots of generic code. The JDK developers have already done the heavy lifting and supplied type parameters for all the collection classes. As a rule of thumb, only code that traditionally involved lots of casts from very general types (such as `Object` or the `Comparable` interface) will benefit from using type parameters.

In this chapter, I will show you everything you need to know to implement your own generic code. However, I expect that most readers will use this knowledge primarily for help with troubleshooting and to satisfy their curiosity about the inner workings of the parameterized collection classes.

## 8.2 Defining a Simple Generic Class

A *generic class* is a class with one or more type variables. In this chapter, a simple `Pair` class is used as an example. This class allows us to focus on generics without being distracted by data storage details. Here is the code for the generic `Pair` class:

```java
public class Pair<T>
{
    private T first;
    private T second;

    public Pair() { first = null; second = null; }
    public Pair(T first, T second) { this.first = first; this.second = second; }

    public T getFirst() { return first; }
    public T getSecond() { return second; }

    public void setFirst(T newValue) { first = newValue; }
    public void setSecond(T newValue) { second = newValue; }
}
```

The Pair class introduces a type variable T, enclosed in angle brackets < >, after the class name. A generic class can have more than one type variable. For example, we could have defined the Pair class with separate types for the first and second field:

```java
public class Pair<T, U> { . . . }
```

The type variables are used throughout the class definition to specify method return types and the types of fields and local variables. For example:

```java
private T first; // uses the type variable
```

**NOTE:**

It is common practice to use uppercase letters for type variables, and to keep them short. The Java library uses the variable E for the element type of a collection, K and V for key and value types of a table, and T (and the neighboring letters U and S, if necessary) for “any type at all.”

You *instantiate* the generic type by substituting types for the type variables, such as

```java
Pair<String>
```

You can think of the result as an ordinary class with constructors

```java
Pair<String>()
Pair<String>(String, String)
```

and methods

```java
String getFirst()
String getSecond()
void setFirst(String)
void setSecond(String)
```

In other words, the generic class acts as a factory for ordinary classes.

The program in [Listing 8.1](#listing-81) puts the Pair class to work. The static minmax method traverses an array and simultaneously computes the minimum and maximum values. It uses a Pair object to return both results. Recall that the compareTo method compares two strings, returning 0 if the strings are identical, a negative integer if the first string comes before the second in dictionary order, and a positive integer otherwise.

![](img/0e7b74ef51a065c077b42cd87b362288_647_0.png)

**C++ NOTE:**

Superficially, generic classes in Java are similar to template classes in C++. The only obvious difference is that Java has no special template keyword. However, as you will see throughout this chapter, there are substantial differences between these two mechanisms.

**Listing 8.1** `pair1/PairTest1.java`

```java
package pair1;

/**
 * @version 1.01 2012-01-26
 * @author Cay Horstmann
 */
public class PairTest1
{
    public static void main(String[] args)
    {
        String[] words = { "Mary", "had", "a", "little", "lamb" };
        Pair<String> mm = ArrayAlg.minmax(words);
        System.out.println("min = " + mm.getFirst());
        System.out.println("max = " + mm.getSecond());
    }
}

class ArrayAlg
{
    /**
     * Gets the minimum and maximum of an array of strings.
     * @param a an array of strings
     * @return a pair with the min and max values, or null if a
     * is null or empty
     */
    public static Pair<String> minmax(String[] a)
    {
        if (a == null || a.length == 0) return null;
        String min = a[0];
        String max = a[0];
        for (int i = 1; i < a.length; i++)
        {
            if (min.compareTo(a[i]) > 0) min = a[i];
            if (max.compareTo(a[i]) < 0) max = a[i];
        }
        return new Pair<>(min, max);
    }
}
```

## 8.3 Generic Methods

In the preceding section, you have seen how to define a generic class. You can also define a single method with type parameters.
