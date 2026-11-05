A parameter array permits a variable number of arguments to be passed to a method. A parameter array is declared with the params modifier. Only the last parameter of a method can be a parameter array, and the type of a parameter array must be a single-dimensional array type. The Write and WriteLine methods of the System.Console class are good examples of parameter array usage. They are declared as follows.

```
```csharp
public class Console
{
    public static void Write(string fmt, params object[] args) {...}
    public static void WriteLine(string fmt, params object[] args) {...}
    ...
}
```
```

Within a method that uses a parameter array, the parameter array behaves exactly like a regular parameter of an array type. However, in an invocation of a method with a parameter array, it is possible to pass either a single argument of the parameter array type or any number of arguments of the element type of the parameter array. In the latter case, an array instance is automatically created and initialized with the given arguments. This example

```
```csharp
Console.WriteLine("x={0} y={1} z={2}", x, y, z);
```
```

is equivalent to writing the following.

```
```csharp
string s = "x={0} y={1} z={2}";
object[] args = new object[3];
args[0] = x;
args[1] = y;
args[2] = z;
Console.WriteLine(s, args);
```
```

> **BRAD ABRAMS** You may recognize the similarity between params and the C programming language's varargs concept. In keeping with our goal of making C# very simple to understand, the params modifier does not require a special calling convention or special library support. As such, it has proven to be much less prone to error than varargs.

Note, however, that the C# model does create an extra object allocation (the containing array) implicitly on each call. This is rarely a problem, but in inner-loop type scenarios where it could get inefficient, we suggest providing overloads for the mainstream cases and using the params overload for only the edge cases. An example is the StringBuilder.AppendFormat() family of overloads:

```
```csharp
public StringBuilder AppendFormat(string format, object arg0);
public StringBuilder AppendFormat(string format, object arg0, object arg1);
public StringBuilder AppendFormat(string format, object arg0, object arg1, object arg2);
public StringBuilder AppendFormat(string format, params object[] args);
```
```