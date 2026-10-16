The preceding passes in the name of a delegate but without any parameters. Given that `operations[i]` is a delegate, syntactically:

+   - `operations[i]` means the *delegate* (that is, the method represented by the delegate)
+   - `operations[i](2.0)` means *actually call this method, passing in the value in parentheses*

The `ProcessAndDisplayNumber` method is defined to take a delegate as its first parameter:

```
static void ProcessAndDisplayNumber(DoubleOp action, double
value)
```

Then, when in this method, you call:

```
double result = action(value);
```

This actually causes the method that is wrapped up by the `action` delegate instance to be called, and its return result stored in `result`. Running this example gives you the following:

```
SimpleDelegate
Using operations[0]:
Value is 2, result of operation is 4
Value is 7.94, result of operation is 15.88
Value is 1.414, result of operation is 2.828

Using operations[1]:
Value is 2, result of operation is 4
Value is 7.94, result of operation is 63.0436
Value is 1.414, result of operation is 1.999396
```

# Action<T> and Func<T> Delegates

Instead of defining a new delegate type with every parameter and return type, you can use the `Action<T>` and `Func<T>` delegates. The generic `Action<T>` delegate is meant to reference a method with `void` return. This delegate class exists in different variants so that you can pass up to 16 different parameter types. The `Action` class without the generic parameter is for calling methods without parameters. `Action<in T>` is for calling a method with one parameter; `Action<in T1, in T2>` for a method with two parameters; and `Action<in T1, in T2, in T3, in T4, in T5, in T6, in T7, in T8>` for a method with eight parameters.

The `Func<T>` delegates can be used in a similar manner. `Func<T>` allows you to invoke methods with a return type. Similar to `Action<T>`, `Func<T>` is defined in different variants to pass up to 16 parameter types and a return type. `Func<out TResult>` is the delegate type to invoke a method with a return type and without parameters. `Func<in T, out TResult>` is for a method with one parameter, and `Func<in T1, in T2, in T3, in T4, out TResult>` is for a method with four parameters.

The example in the preceding section declared a delegate with a double parameter and a double return type: