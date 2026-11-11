Of course, the subclass programmer should define its own toString() method and add the subclass fields. If the superclass uses getClass().getName(), then the subclass can simply call super.toString(). For example, here is a toString method for the Manager class:

```
    public class Manager extends Employee
    {
        . . .
        public String toString()
        {
            return super.toString()
                 + "[bonus=" + bonus
                 + "]";
        }
    }
```

Now a Manager object is printed as

```
    Manager[name=...,salary=...,hireDay=...[bonus=...]]
```

The toString method is ubiquitous for an important reason: Whenever an object is concatenated with a string by the “+” operator, the Java compiler automatically invokes the toString method to obtain a string representation of the object. For example:

```
    var p = new Point(10, 20);
    String message = "The current position is " + p;
        // automatically invokes p.toString()
```

> **TIP:** Instead of writing x.toString(), you can write "" + x. This statement concatenates the empty string with the string representation of x that is exactly x.toString(). Unlike toString, this statement even works if x is of primitive type.

If x is any object and you call

```
    System.out.println(x);
```

then the println method simply calls x.toString() and prints the resulting string.

The Object class defines the toString method to print the class name and the hash code of the object. For example, the call

```
    System.out.println(System.out)
```