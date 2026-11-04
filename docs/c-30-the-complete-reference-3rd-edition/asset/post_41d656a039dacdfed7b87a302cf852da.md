
## Using Reflection

Using Type's methods and properties, it is possible to obtain detailed information about a type at runtime. This is an extremely powerful feature, because once you have obtained information about a type, you can invoke its constructors, call its methods, and use its properties. Thus, reflection enables you to use code that was not available at compile time.

The Reflection API is quite large, and it is not possible to cover the entire topic here. (Complete coverage of reflection could easily fill an entire book!) However, because the Reflection API is logically designed, once you understand how to use a part of it, the rest just falls into place. With this thought in mind, the following sections demonstrate four key reflection techniques: obtaining information about methods, invoking methods, constructing objects, and loading types from assemblies.

### Obtaining Information About Methods

Once you have a Type object, you can obtain a list of methods supported by the type by using GetMethods(). One form is shown here:

```csharp
MethodInfo[] GetMethods()
```

It returns an array of MethodInfo objects that describe the methods supported by the invoking type. MethodInfo is in the System.Reflection namespace. MethodInfo is derived from the abstract class MethodBase, which inherits MemberInfo. Thus, the properties and methods defined by all three of these classes are available for your use. For example, to obtain the name of a method, use the Name property. Two members that are of particular interest at this time are ReturnType and GetParameters(). The return type of a method is found in the read-only ReturnType property, which is an object of Type. The method GetParameters() returns a list of the parameters associated with a method. It has this general form:

```csharp
ParameterInfo[] GetParameters();
```

The parameter information is held in a ParameterInfo object. ParameterInfo defines a large number of properties and methods that describe the parameter. Two properties that are of particular value are Name, which is a string that contains the name of the parameter, and ParameterType, which describes the parameter's type. The parameter's type is encapsulated within a Type object. Here is a program that uses reflection to obtain the methods supported by a class called MyClass. For each method, it displays the return type and name of the method, and the name and type of any parameters that each method may have.

```csharp
// Analyze methods using reflection.

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
        if(x < i && i < y) return true;
        else return false;
    }

    public void Set(int a, int b) {
        x = a;
        y = b;
    }

    public void Set(double a, double b) {
        x = (int) a;
        y = (int) b;
    }

    public void Show() {
        Console.WriteLine("x: {0}, y: {1}", x, y);
    }
}

class ReflectDemo {
    static void Main() {
        Type t = typeof(MyClass); // get a Type object representing MyClass

        Console.WriteLine("Analyzing methods in " + t.Name);
        Console.WriteLine();

        Console.WriteLine("Methods supported: ");

        MethodInfo[] mi = t.GetMethods();

        // Display methods supported by MyClass.
        foreach(MethodInfo m in mi) {
            // Display return type and name.
            Console.Write(" " + m.ReturnType.Name +
                " " + m.Name + "(");

            // Display parameters.
            ParameterInfo[] pi = m.GetParameters();

            for(int i=0; i < pi.Length; i++) {
                Console.Write(pi[i].ParameterType.Name +
                    " " + pi[i].Name);
                if(i+1 < pi.Length) Console.Write(", ");
            }
            Console.WriteLine(")");
        }
        Console.WriteLine();
    }
}
```

The output is shown here:

```text
Analyzing methods in MyClass

Methods supported:
    Int32 Sum()
    Boolean IsBetween(Int32 i)
    Void Set(Int32 a, Int32 b)
    Void Set(Double a, Double b)
    Void Show()
    Type GetType()
    String ToString()
    Boolean Equals(Object obj)
    Int32 GetHashCode()
```

Let's look at this program closely. First, notice that MyClass defines a public constructor and a number of public methods, including the overloaded Set() method. Inside Main(), a Type object representing MyClass is obtained using this line of code:

```csharp
Type t = typeof(MyClass); // get a Type object representing MyClass
```

Recall that typeof returns a Type object that represents the specified type, which in this case is MyClass.

Using t and the Reflection API, the program then displays information about the methods supported by MyClass. First, a list of the methods is obtained by the following statement:

```csharp
MethodInfo[] mi = t.GetMethods();
```

Next, a foreach loop is established that cycles through mi. With each pass, the return type, name, and parameters for each method are displayed by the following code:

```csharp
// Display return type and name.
Console.Write("  " + m.ReturnType.Name +
              "  " + m.Name + "(");

// Display parameters.
ParameterInfo[] pi = m.GetParameters();

for(int i=0; i < pi.Length; i++) {
    Console.Write(pi[i].ParameterType.Name +
                  " " + pi[i].Name);
    if(i+1 < pi.Length) Console.Write(", ");
}
```

In this sequence, the parameters associated with each method are obtained by calling GetParameters() and stored in the pi array. Then a for loop cycles through the pi array, displaying the type and name of each parameter. The key point is that this information is obtained dynamically at runtime without relying on prior knowledge of MyClass.

### A Second Form of GetMethods()

A second form of GetMethods() lets you specify various flags that filter the methods that are retrieved. It has this general form:

```csharp
MethodInfo[] GetMethods(BindingFlags flags)
```

This version obtains only those methods that match the criteria you specify. BindingFlags is an enumeration. Here are several commonly used values:

| Value | Meaning |
|-------|---------|
| DeclaredOnly | Retrieves only those methods defined by the specified class. Inherited methods are not included. |
| Instance | Retrieves instance methods. |
| NonPublic | Retrieves nonpublic methods. |
| Public | Retrieves public methods. |
| Static | Retrieves static methods. |

You can OR together two or more flags. In fact, minimally you must include either Instance or Static with Public or NonPublic. Failure to do so will result in no methods being retrieved. One of the main uses of the BindingFlags form of GetMethods() is to enable you to obtain a list of the methods defined by a class without also retrieving the inherited methods. This is especially useful for preventing the methods defined by object from being obtained. For example, try substituting this call to GetMethods() into the preceding program:

```csharp
// Now, only methods declared by MyClass are obtained.
MethodInfo[] mi = t.GetMethods(BindingFlags.DeclaredOnly |
                               BindingFlags.Instance |
                               BindingFlags.Public );
```

After making this change, the program produces the following output:

```text
Analyzing methods in MyClass

Methods supported:
    Int32 Sum()
    Boolean IsBetween(Int32 i)
    Void Set(Int32 a, Int32 b)
    Void Set(Double a, Double b)
    Void Show()
```

As you can see, only those methods explicitly defined by MyClass are displayed.

### Calling Methods Using Reflection

Once you know what methods a type supports, you can call one or more of them. To do this, you will use the Invoke() method that is contained in MethodInfo. One of its forms is shown here:

```csharp
object Invoke(object ob, object[] args)
```

Here, ob is a reference to the object on which the method is invoked. For static methods, pass null to ob. Any arguments that need to be passed to the method are specified in the array args. If no arguments are needed, args must be null. Also, args must contain exactly the same number of elements as there are arguments. Therefore, if two arguments are needed, then args must be two elements long. It can't, for example, be three or four elements long. The value returned by the invoked method is returned by Invoke().

To call a method, simply call Invoke() on an instance of MethodInfo that was obtained by calling GetMethods(). The following program demonstrates the procedure:

```csharp
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
