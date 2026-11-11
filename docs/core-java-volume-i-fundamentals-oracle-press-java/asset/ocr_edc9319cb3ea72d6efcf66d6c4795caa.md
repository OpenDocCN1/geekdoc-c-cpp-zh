Listing 6.8 contains the complete source code for the talking clock program with an anonymous inner class. If you compare this program with Listing 6.7, you will see that in this case, the solution with the anonymous inner class is quite a bit shorter and, hopefully, with some practice, as easy to comprehend.

For many years, Java programmers routinely used anonymous inner classes for event listeners and other callbacks. Nowadays, you are better off using a lambda expression. For example, the `start` method from the beginning of this section can be written much more concisely with a lambda expression like this:

```
~~~java
public void start(int interval, boolean beep)
{
    var timer = new Timer(interval, event -> {
        System.out.println(
            "At the tone, the time is " +
            Instant.ofEpochMilli(event.getWhen()));
        if (beep) Toolkit.getDefaultToolkit().beep(); });
    timer.start();
}
~~~
```

**NOTE:**

If you store an anonymous class instance in a variable defined with `var`, the variable knows about added methods or fields:

```
~~~java
var bob = new Object() { String name = "Bob"; }
System.out.println(bob.name);
~~~
```

If you declare bob as having type `Object`, then `bob.name` does not compile.