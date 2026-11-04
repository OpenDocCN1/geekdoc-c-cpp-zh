```
string result = String.Concat("The value is " + 19);
Console.WriteLine("result: " + result);

result = String.Concat("hello ", 88, " ", 20.0, " ",
false, ", ", 23.45M);
Console.WriteLine("result: " + result);

MyClass mc = new MyClass();

result = String.Concat(mc, " current count is ",
MyClass.Count);
Console.WriteLine("result: " + result);
}
```

The output is shown here:

```
result: The value is 19
result: hello 88 20 False 23.45
result: MyClass current count is 1
```

In this example, Concat() concatenates the string representations of various types of data. For each argument, the ToString() method associated with that argument is called to obtain a string representation. Thus, in this call to Concat()

```
string result = String.Concat("The value is " + 19);
```

Int32.ToString() is invoked to obtain the string representation of the integer value 19.
Concat() then concatenates the strings and returns the result.

Also notice how an object of the user-defined class MyClass can be used in this call to Concat():

```
result = String.Concat(mc, " current count is ",
MyClass.Count);
```

In this case, the string representation of mc, which is of type MyClass, is returned. By default, this is simply its class name. However, if you override the ToString() method, then MyClass can return a different string. For example, try adding this version of ToString() to MyClass in the preceding program:

```
public override string ToString() {
return "An object of type MyClass";
}
```

When this version is used, the last line in the output will be

```
result: An object of type MyClass current count is 1
```

# Searching a String

String offers many methods that allow you to search a string. For example, you can search for either a substring or a character. You can also search for the first or last occurrence of either.