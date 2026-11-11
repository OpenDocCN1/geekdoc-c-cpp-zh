different parameters. The compiler must sort out which method to call. It picks the correct method by matching the parameter types in the headers of the various methods with the types of the values used in the specific method call. A compile-time error occurs if the compiler cannot match the parameters, either because there is no match at all or because there is not one that is better than all others. (The process of finding a match is called *overloading resolution*.)

![](bbox=[0.128, 0.284, 0.18, 0.325])

# NOTE:

Java allows you to overload any method—not just constructor methods. Thus, to completely describe a method, you need to specify its name together with its parameter types. This is called the *signature* of the method. For example, the `String` class has four public methods called `indexOf`. They have signatures

```
```text
indexOf(int)
indexOf(int, int)
indexOf(String)
indexOf(String, int)
```
```

The return type is not part of the method signature. That is, you cannot have two methods with the same names and parameter types but different return types.

# 4.6.2 Default Field Initialization

If you don’t set a field explicitly in a constructor, it is automatically set to a default value: numbers to `0`, boolean values to `false`, and object references to `null`. Some people consider it poor programming practice to rely on the defaults. Certainly, it makes it harder for someone to understand your code if fields are being initialized invisibly.