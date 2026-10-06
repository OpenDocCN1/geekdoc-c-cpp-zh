Both are applicable methods when a call is made using an integer argument; in other words, if either method existed, the call aMethod(12) would work. When the two methods coexist, however, neither is "better" Because C# cannot determine which one is better, the code will not compile.

If two signatures are equal good, the one that does not omit optional parameters is considered better. For example, suppose you have two methods as follows:

```
private static void BMethod(int a)
private static void BMethod(int a, char b = 'B')
```

If either method existed, the call BMethod(12) would work, but when the two coexist, the first version is better because no optional parameters are omitted in the call.

Watch the video Using Optional Parameters.

# TWO TRUTHS & A LIE
Using Optional Parameters

+   1. An optional parameter to a method is one for which an argument can be a value parameter, a ref parameter, or an out parameter.
2. You make a parameter optional by providing a value for it in the method declaration.
3. If you assign a default value to any variable in a method's parameter list, then all parameters to the right of that parameter must also have default values.

> Only value parameters can be optional.
The false statement is #1 An optional parameter to a method is one for which a default value is automatically supplied if you do not explicitly send one as an