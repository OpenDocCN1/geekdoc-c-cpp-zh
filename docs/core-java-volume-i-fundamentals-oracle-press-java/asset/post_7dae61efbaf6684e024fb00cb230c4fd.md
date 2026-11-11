
```java
(String first, String second)
    -> first.length() - second.length()
```

You have just seen your first *lambda expression*. Such an expression is simply a block of code, together with the specification of any variables that must be passed to the code.

Why the name? Many years ago, before there were any computers, the logician Alonzo Church wanted to formalize what it means for a mathematical function to be effectively computable. (Curiously, there are functions that are known to exist, but nobody knows how to compute their values.) He used the Greek letter lambda (λ) to mark parameters. Had he known about the Java API, he would have written

```
λfirst. λsecond. first.length() - second.length()
```

> **NOTE:**
>
> Why the letter λ? Did Church run out of other letters of the alphabet? Actually, the venerable *Principia Mathematica* used the ^ accent to denote free variables, which inspired Church to use an uppercase lambda Λ for parameters. But in the end, he switched to the lowercase version. Ever since, an expression with parameter variables has been called a lambda expression.

What you have just seen is a simple form of lambda expressions in Java: parameters, the `->` arrow, and an expression. If the code carries out a computation that doesn't fit in a single expression, write it exactly like you would have written a method: enclosed in `{}` and with explicit `return` statements. For example,

```java
(String first, String second) ->
{
    if (first.length() < second.length()) return -1;
    else if (first.length() > second.length()) return 1;
    else return 0;
}
```

If a lambda expression has no parameters, you still supply empty parentheses, just as with a parameterless method:

```java
() -> { for (int i = 100; i >= 0; i--) System.out.println(i); }
```

If the parameter types of a lambda expression can be inferred, you can omit them. For example,

```java
Comparator<String> comp
    = (first, second) // same as (String first, String second)
    -> first.length() - second.length();
```

Here, the compiler can deduce that first and second must be strings because the lambda expression is assigned to a string comparator. (We will have a closer look at this assignment in the next section.)

If a method has a single parameter with inferred type, you can even omit the parentheses:

```java
ActionListener listener = event ->
    System.out.println("The time is "
    + Instant.ofEpochMilli(event.getWhen()));
    // instead of (event) -> . . . or (ActionEvent event) -> . . .
```

You never specify the result type of a lambda expression. It is always inferred from context. For example, the expression

```java
(String first, String second) -> first.length() - second.length()
```

can be used in a context where a result of type int is expected.

```java
System.out.println(Arrays.toString(planets));
System.out.println("Sorted in dictionary order:");
Arrays.sort(planets);
System.out.println(Arrays.toString(planets));
System.out.println("Sorted by length:");
Arrays.sort(planets, (first, second) -> first.length() - second.length());
System.out.println(Arrays.toString(planets));

var timer = new Timer(1000, event ->
    System.out.println("The time is " + new Date()));
timer.start();

// keep program running until user selects "OK"
JOptionPane.showMessageDialog(null, "Quit program?");
System.exit(0);
}
}
```

### 6.2.3 Functional Interfaces

As we discussed, there are many existing interfaces in Java that encapsulate blocks of code, such as `ActionListener` or `Comparator`. Lambdas are compatible with these interfaces.

You can supply a lambda expression whenever an object of an interface with a single abstract method is expected. Such an interface is called a *functional interface*.

> **NOTE:**
>
> You may wonder why a functional interface must have a single *abstract* method. Aren’t all methods in an interface abstract? Actually, it has always been possible for an interface to redeclare methods from the Object class such as `toString` or `clone`, and these declarations do not make the methods abstract. (Some interfaces in the Java API redeclare Object methods in order to attach javadoc comments. Check out the Comparator API for an example.) More importantly, as you saw in [Section 6.1.5](#), “Default Methods,” on p. 323, interfaces can declare nonabstract methods.

To demonstrate the conversion to a functional interface, consider the `Arrays.sort` method. Its second parameter requires an instance of `Comparator`, an interface with a single method. Simply supply a lambda:

```java
Arrays.sort(words,
    (first, second) -> first.length() - second.length());
```

Behind the scenes, the `Arrays.sort` method receives an object of some class that implements `Comparator<String>`. Invoking the compare method on that object executes the body of the lambda expression. The management of these objects and classes is completely implementation-dependent, and it can be much more efficient than using traditional inner classes. It is best to think of a lambda expression as a function, not an object, and to accept that it can be passed to a functional interface.

This conversion to interfaces is what makes lambda expressions so compelling. The syntax is short and simple. Here is another example:

```java
var timer = new Timer(1000, event ->
{
    System.out.println("At the tone, the time is "
        + Instant.ofEpochMilli(event.getWhen()));
    Toolkit.getDefaultToolkit().beep();
});
```

That’s a lot easier to read than the alternative with a class that implements the `ActionListener` interface.

In fact, conversion to a functional interface is the *only* thing that you can do with a lambda expression in Java. In other programming languages that support function literals, you can declare function types such as `(String, String) -> int`, declare variables of those types, and use the variables to

The `ArrayList` class has a `removeIf` method whose parameter is a `Predicate`. It is specifically designed to pass a lambda expression. For example, the following statement removes all null values from an array list:

```java
list.removeIf(e -> e == null);
```

Another useful functional interface is `Supplier<T>`:

```java
public interface Supplier<T>
{
    T get();
}
```

A supplier has no arguments and yields a value of type T when it is called. Suppliers are used for *lazy evaluation*. For example, consider the call

```java
LocalDate hireDay = Objects.requireNonNullElse(day,
    LocalDate.of(1970, 1, 1));
```

This is not optimal. We expect that day is rarely null, so we only want to construct the default `LocalDate` when necessary. By using the supplier, we can defer the computation:

```java
LocalDate hireDay = Objects.requireNonNullElseGet(day,
    () -> LocalDate.of(1970, 1, 1));
```

The `requireNonNullElseGet` method only calls the supplier when the value is needed.

### 6.2.4 Method References

Sometimes, a lambda expression involves a single method. For example, suppose you simply want to print the event object whenever a timer event occurs. Of course, you could call

```java
var timer = new Timer(1000, event ->
    System.out.println(event));
```

It would be nicer if you could just pass the `println` method to the `Timer` constructor. Here is how you do that:

```java
var timer = new Timer(1000, System.out::println);
```

The expression `System.out::println` is a *method reference*. It directs the compiler to produce an instance of a functional interface, overriding the single abstract method of the interface to call the given method. In this example, an `ActionListener` is produced whose `actionPerformed(ActionEvent e)` method calls `System.out.println(e)`.

**NOTE:**

Like a lambda expression, a method reference is not an object. It gives rise to an object when assigned to a variable whose type is a functional interface.

**NOTE:**

There are ten overloaded `println` methods in the `PrintStream` class (of which `System.out` is an instance). The compiler needs to figure out which one to use, depending on context. In our example, the method reference `System.out::println` must be turned into an `ActionListener` instance with a method

```java
void actionPerformed(ActionEvent e)
```

The `println(Object x)` method is selected from the ten overloaded `println` methods since `Object` is the best match for `ActionEvent`. When the `actionPerformed` method is called, the event object is printed.
