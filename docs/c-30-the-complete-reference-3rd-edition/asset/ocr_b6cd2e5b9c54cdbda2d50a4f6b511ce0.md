WriteLine(). Many classes override this method. Doing so allows them to tailor a description specifically for the types of objects that they create. For example:

```
// Demonstrate ToString()
using System;

class MyClass {
    static int count = 0;
    int id;

    public MyClass() {
        id = count;
        count++;
    }

    public override string ToString() {
        return "MyClass object #" + id;
    }
}

class Test {
    static void Main() {
        MyClass ob1 = new MyClass();
        MyClass ob2 = new MyClass();
        MyClass ob3 = new MyClass();

        Console.WriteLine(ob1);
        Console.WriteLine(ob2);
        Console.WriteLine(ob3);
    }
}
```

The output from the program is shown here:

```
MyClass object #0
MyClass object #1
MyClass object #2
```

# Boxing and Unboxing

As explained, all C# types, including the value types, are derived from object. Thus, a reference of type object can be used to refer to any other type, including value types. When an object reference refers to a value type, a process known as boxing occurs. Boxing causes the value of a value type to be stored in an object instance. Thus, a value type is “boxed” inside an object. This object can then be used like any other object. In all cases, boxing occurs automatically. You simply assign a value to an object reference. C# handles the rest.

Unboxing is the process of retrieving a value from a boxed object. This action is performed using an explicit cast from the object reference to its corresponding value type. Attempting to unbox an object into a different type will result in a runtime error.