```csharp
y = b;
Show();
}

// Overload set.
public void Set(double a, double b) {
Console.Write("Inside Set(double, double). ");
x = (int) a;
y = (int) b;
Show();
}

public void Show() {
Console.WriteLine("Values are x: {0}, y: {1}", x, y);
}

class InvokeMethDemo {
static void Main() {
Type t = typeof(MyClass);
MyClass reflectOb = new MyClass(10, 20);
int val;

Console.WriteLine("Invoking methods in " + t.Name);
Console.WriteLine();
MethodInfo[] mi = t.GetMethods();

// Invoke each method.
foreach(MethodInfo m in mi) {
// Get the parameters.
ParameterInfo[] pi = m.GetParameters();

if(m.Name.CompareTo("Set")==0 && pi[0].ParameterType == typeof(int)) {
object[] args = new object[2];
args[0] = 9;
args[1] = 18;
m.Invoke(reflectOb, args);
}
else if(m.Name.CompareTo("Set")==0 && pi[0].ParameterType == typeof(double)) {
object[] args = new object[2];
args[0] = 1.12;
args[1] = 23.4;
m.Invoke(reflectOb, args);
}
else if(m.Name.CompareTo("Sum")==0) {
val = (int) m.Invoke(reflectOb, null);
Console.WriteLine("sum is " + val);
}
else if(m.Name.CompareTo("IsBetween")==0) {
object[] args = new object[1];
args[0] = 14;
if((bool) m.Invoke(reflectOb, args))
Console.WriteLine("14 is between x and y");
}
else if(m.Name.CompareTo("Show")==0) {
    m.Invoke(reflectOb, null);
}
}
}
```

The output is shown here:

```
Invoking methods in MyClass

sum is 30
14 is between x and y
Inside Set(int, int). Values are x: 9, y: 18
Inside Set(double, double). Values are x: 1, y: 23
Values are x: 1, y: 23
```

Look closely at how the methods are invoked. First, a list of methods is obtained. Then, inside the foreach loop, parameter information is retrieved. Next, using a series of if/else statements, each method is executed with the proper type and number of arguments. Pay special attention to the way that the overloaded Set() method is executed by the following code:

```
if(m.Name.CompareTo("Set")==0 &&
    pi[0].ParameterType == typeof(int)) {
    object[] args = new object[2];
    args[0] = 9;
    args[1] = 18;
    m.Invoke(reflectOb, args);
}
else if(m.Name.CompareTo("Set")==0 &&
    pi[0].ParameterType == typeof(double)) {
    object[] args = new object[2];
    args[0] = 1.12;
    args[1] = 23.4;
    m.Invoke(reflectOb, args);
}
```

If the name of the method is Set, then the type of the first parameter is tested to determine which version of the method was found. If it was Set(int, int), then int arguments are loaded into args. Otherwise, double arguments are used.

## Obtaining a Type's Constructors

In the previous example, there is no advantage to using reflection to invoke methods on MyClass since an object of type MyClass was explicitly created. It would be easier to just call its methods normally. However, the power of reflection starts to become apparent when an object is created dynamically at runtime. To do this, you will need to first obtain a list of the constructors. Then, you will create an instance of the type by invoking one of the constructors. This mechanism allows you to instantiate any type of object at runtime without naming it in a declaration statement.

To obtain the constructors for a type, call GetConstructors() on a Type object. One commonly used form is shown here:

```
ConstructorInfo[] GetConstructors()
```

It returns an array of ConstructorInfo objects that describe the constructors. ConstructorInfo is derived from the abstract class MethodBase, which inherits MemberInfo. It also defines several members of its own. The one we are interested in is GetParameters(), which returns a list of the parameters associated with a constructor. It works just like GetParameters() defined by MethodInfo, described earlier.

Once an appropriate constructor has been found, an object is created by calling the Invoke() method defined by ConstructorInfo. One form is shown here:

```
object Invoke(object[] args)
```

Any arguments that need to be passed to the method are specified in the array args. If no arguments are needed, pass null to args. In all cases, args must contain exactly the same number of elements as there are arguments and the types of arguments must be compatible with the types of the parameters. Invoke() returns a reference to the object that was constructed.

The following program uses reflection to create an instance of MyClass:

```csharp
// Create an object using reflection.
using System;
using System.Reflection;

class MyClass {
    int x;
    int y;

    public MyClass(int i) {
        Console.WriteLine("Constructing MyClass(int, int). ");
        x = y = i;
    }

    public MyClass(int i, int j) {
        Console.WriteLine("Constructing MyClass(int, int). ");
        x = i;
        y = j;
        Show();
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
        y = b;
        Show();
    }

// Overload Set.
public void Set(double a, double b) {
    Console.Write("Inside Set(double, double). ");
    x = (int) a;
    y = (int) b;
    Show();
}

public void Show() {
    Console.WriteLine("Values are x: {0}, y: {1}", x, y);
}

class InvokeConsDemo {
    static void Main() {
        Type t = typeof(MyClass);
        int val;
        // Get constructor info.
        ConstructorInfo[] ci = t.GetConstructors();

        Console.WriteLine("Available constructors: ");
        foreach (ConstructorInfo c in ci) {
            // Display return type and name.
            Console.Write("  " + c.Name + "(");

            // Display parameters.
            ParameterInfo[] pi = c.GetParameters();

            for(int i=0; i < pi.Length; i++) {
                Console.Write(pi[i].ParameterType.Name +
                    " " + pi[i].Name);
                if(i+1 < pi.Length) Console.Write(", ");
            }

            Console.WriteLine(")");
        }
        Console.WriteLine();

        // Find matching constructor.
        int x;
        for(x=0; x < ci.Length; x++) {
            ParameterInfo[] pi = ci[x].GetParameters();
            if(pi.Length == 2) break;
        }

        if(x == ci.Length) {
Console.WriteLine("No matching constructor found.");
return;
}
else
Console.WriteLine("Two-parameter constructor found.\n");

// Construct the object.
object[] consargs = new object[2];
consargs[0] = 10;
consargs[1] = 20;
object reflectOb = ci[x].Invoke(consargs);

Console.WriteLine("\nInvoking methods on reflectOb.");
Console.WriteLine();
MethodInfo[] mi = t.GetMethods();

// Invoke each method.
foreach (MethodInfo m in mi) {
    // Get the parameters.
    ParameterInfo[] pi = m.GetParameters();

    if(m.Name.CompareTo("Set")==0 && pi[0].ParameterType == typeof(int)) {
        // This is Set(int, int).
        object[] args = new object[2];
        args[0] = 9;
        args[1] = 18;
        m.Invoke(reflectOb, args);
    }
    else if(m.Name.CompareTo("Set")==0 && pi[0].ParameterType == typeof(double)) {
        // This is Set(double, double).
        object[] args = new object[2];
        args[0] = 1.12;
        args[1] = 23.4;
        m.Invoke(reflectOb, args);
    }
    else if(m.Name.CompareTo("Sum")==0) {
        val = (int) m.Invoke(reflectOb, null);
        Console.WriteLine("sum is " + val);
    }
    else if(m.Name.CompareTo("IsBetween")==0) {
        object[] args = new object[1];
        args[0] = 14;
        if((bool) m.Invoke(reflectOb, args))
            Console.WriteLine("14 is between x and y");
    }
    else if(m.Name.CompareTo("Show")==0) {
        m.Invoke(reflectOb, null);
    }
}
}
```

The output is shown here:

```
Available constructors:
    MyClass(Int32 i)
    MyClass(Int32 i, Int32 j)

Two-parameter constructor found.

Constructing MyClass(int, int).
Values are x: 10, y: 20

Invoking methods on reflectOb.

sum is 30
14 is between x and y
Inside Set(int, int). Values are x: 9, y: 18
Inside Set(double, double). Values are x: 1, y: 23
Values are x: 1, y: 23
```

Let's look at how reflection is used to construct a MyClass object. First, a list of the public constructors is obtained using the following statement:

```
ConstructorInfo[] ci = t.GetConstructors();
```

Next, for the sake of illustration, the constructors are displayed. Then the list is searched for a constructor that takes two arguments, using this code:

```
for(x=0; x < ci.Length; x++) {
    ParameterInfo[] pi = ci[x].GetParameters();
    if(pi.Length == 2) break;
}
```

If the constructor is found (as it will be in this case), an object is instantiated by the following sequence:

```
// Construct the object.
object[] consargs = new object[2];
consargs[0] = 10;
consargs[1] = 20;
object reflectOb = ci[x].Invoke(consargs);
```

After the call to Invoke(), reflectOb will refer to an object of type MyClass. The program then executes methods on that instance.

One important point needs to be made. In this example, for the sake of simplicity, it was assumed that the only two-argument constructor was one that took two int arguments. Obviously, in real-world code this would need to be verified by checking the parameter type of each argument.

## Obtaining Types from Assemblies

In the preceding example, everything about MyClass has been discovered using reflection except for one item: the type MyClass, itself. That is, although the preceding examples dynamically determined information about MyClass, they still relied upon the fact that the
