When the program runs, the Java runtime system notices the broken promise and generates a ClassCastException. If you do not catch the exception, your program terminates. Thus, it is good programming practice to find out whether a cast will succeed before attempting it. Simply use the instanceof operator. For example:

```
```java
if (staff[1] instanceof Manager)
{
    boss = (Manager) staff[1];
    . . .
}
```
```

Finally, the compiler will not let you make a cast if there is no chance for the cast to succeed. For example, the cast

```
```java
String c = (String) staff[1];
```
```

is a compile-time error because String is not a subclass of Employee.

To sum up:

+   - You can cast only within an inheritance hierarchy.
+   - Use instanceof to check before casting from a superclass to a subclass.

> > **NOTE:** The test
> > 
> > `x instanceof C`
> > 
> > does not generate an exception if x is null. It simply returns false. That makes sense: null refers to no object, so it certainly doesn’t refer to an object of type C.

Actually, converting the type of an object by a cast is not usually a good idea. In our example, you do not need to cast an Employee object to a Manager object for most purposes. The getSalary method will work correctly on both objects of both classes. The dynamic binding that makes polymorphism work locates the correct method automatically.

The only reason to make the cast is to use a method that is unique to managers, such as setBonus. If for some reason you find yourself wanting to call setBonus on Employee objects, ask yourself whether this is an indication of a design flaw in the superclass. It may make sense to redesign the superclass and add a setBonus method. Remember, it takes only one uncaught ClassCastException to terminate your program. In general, it is best to minimize the use of casts and the instanceof operator.