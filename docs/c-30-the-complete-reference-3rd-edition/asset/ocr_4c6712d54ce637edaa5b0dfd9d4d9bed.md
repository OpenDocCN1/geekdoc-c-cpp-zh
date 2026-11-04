```
Boolean IsBetween(Int32 i)
Void Set(Int32 a, Int32 b)
Void Set(Double a, Double b)
Void Show()
```

As you can see, only those methods explicitly defined by MyClass are displayed.

# Calling Methods Using Reflection

Once you know what methods a type supports, you can call one or more of them. To do this, you will use the Invoke() method that is contained in MethodInfo. One of its forms is shown here:

```
object Invoke(object ob, object[] args)
```

Here, ob is a reference to the object on which the method is invoked. For static methods, pass null to ob. Any arguments that need to be passed to the method are specified in the array args. If no arguments are needed, args must be null. Also, args must contain exactly the same number of elements as there are arguments. Therefore, if two arguments are needed, then args must be two elements long. It can't, for example, be three or four elements long. The value returned by the invoked method is returned by Invoke().

To call a method, simply call Invoke() on an instance of MethodInfo that was obtained by calling GetMethods(). The following program demonstrates the procedure:

```
// Invoke methods using reflection.
using System;
using System.Reflection;

class MyClass {
    int x;
    int y;

    public MyClass(int i, int j) {
        x = i;
        y = j;
    }

    public int Sum() {
        return x+y;
    }

    public bool IsBetween(int i) {
        if((x < i) && (i < y)) return true;
        else return false;
    }

    public void Set(int a, int b) {
        Console.Write("Inside Set(int, int). ");
        x = a;
```