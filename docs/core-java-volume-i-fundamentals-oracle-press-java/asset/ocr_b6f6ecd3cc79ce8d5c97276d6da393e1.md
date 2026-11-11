```
```java
var timer = new Timer(1000, event ->
System.out.println(event));
```
```

It would be nicer if you could just pass the `println` method to the `Timer` constructor. Here is how you do that:

```
```java
var timer = new Timer(1000, System.out::println);
```
```

The expression `system.out::println` is a *method reference*. It directs the compiler to produce an instance of a functional interface, overriding the single abstract method of the interface to call the given method. In this example, an `ActionListener` is produced whose `actionPerformed(ActionEvent e)` method calls `System.out.println(e)`.

**NOTE:**

Like a lambda expression, a method reference is not an object. It gives rise to an object when assigned to a variable whose type is a functional interface.

**NOTE:**

There are ten overloaded `println` methods in the `PrintStream` class (of which `System.out` is an instance). The compiler needs to figure out which one to use, depending on context. In our example, the method reference `System.out::println` must be turned into an `ActionListener` instance with a method

```
```java
void actionPerformed(ActionEvent e)
```
```

The `println(Object x)` method is selected from the ten overloaded `println` methods since `Object` is the best match for `ActionEvent`. When the `actionPerformed` method is called, the event object is printed.