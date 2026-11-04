If we didn't have dynamic here, we would have to obtain the GetCalc method in a manual way, much like classic use of .NET Reflection works. For example, the following piece of code yields the same results:

```
var py = Python.CreateEngine();
var script = py.ImportModule("Calc");

// Gets a Python function object, returned as "dynamic".
dynamic getCalc = script.GetVariable("GetCalc");
dynamic calc = getCalc();
```

Now we type the script variable statically as a ScriptScope and call the GetVariable method to obtain the defined GetCalc function. In dynamic languages, all those top-level constructs are simply treated in the same manner, so the GetCalc function can be retrieved as a variable. This GetVariable method's return type is dynamic once more (just like the Execute method we saw earlier). In this case, we make a call to the retrieved Python function object using delegate invocation syntax.

Because we've gotten rid of one layer of dynamic treatment, we're increasingly losing code clarity. All of a sudden, we need to call cryptic methods such as GetVariable, passing in strings to communicate our intent. This is precisely what dynamic helps with: reducing clutter needed to establish calls involving dynamic typing.

# DYNAMIC TYPES ARE DYNAMIC: THEY CAN AND WILL CHANGE

One key aspect of dynamically typed scripting languages is that the (nonexisting) type of variables can change over time. At one point, a variable may contain an integer, and then it could be holding on to a string or even a function.

This effectively provides the same "flexibility" as typing an object using the least specific type in a statically typed system (that is, System.Object). However, in a static world, this is also the least useful type because few to no useful operations can be done on it. In dynamic languages, you can apply any operation to anything, at the cost of possible runtime errors when the lack of (or incompatibility of) an operation gets detected.

In our running example, we can show how the GetCalc top-level variable can be replaced from inside C#, using dynamic. Where the variable originally contained a PythonFunction object, we replace it with a string. Obviously, this will cause further use of the variable as if it were a function to fail because you can't "invoke a string":

```
// IronPython.Runtime.PythonFunction
Console.WriteLine(script.GetCalc.GetType());

// System.String
script.GetCalc = "Oops!";
Console.WriteLine(script.GetCalc.GetType());

// Oops! Can't invoke a string...
```