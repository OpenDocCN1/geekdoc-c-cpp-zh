```
```java
public void start();
}
```
```

Notice the static `access$0` method that the compiler added to the outer class. It returns the `beep` field of the object that is passed as a parameter. (The method name might be slightly different, such as `access$000`, depending on the compiler.)

That was a potential security risk, and it made life complicated for tools that analyze class files. As of Java 11, the virtual machine understands nesting relationships between classes, and the access methods are no longer generated.

# ### 6.3.4 Local Inner Classes

If you look carefully at the code of the `TalkingClock` example, you will find that you need the name of the type `TimePrinter` only once: when you create an object of that type in the `start` method.

In a situation like this, you can define the class *locally* in a *single method*.

```
```java
public void start()
{
   class TimePrinter implements ActionListener
   {
      public void actionPerformed(ActionEvent event)
      {
         System.out.println("At the tone, the time is "
            + Instant.ofEpochMilli(event.getWhen()));
         if (beep) Toolkit.getDefaultToolkit().beep();
      }
   }
   var listener = new TimePrinter();
   var timer = new Timer(interval, listener);
   timer.start();
}
```
```