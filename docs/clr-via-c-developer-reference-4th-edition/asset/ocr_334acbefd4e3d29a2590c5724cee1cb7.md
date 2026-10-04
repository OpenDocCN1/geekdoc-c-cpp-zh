```
// 4. Same as: M(o, "1", default(DateTime), new Guid());
M(s_n++, s_n.ToString());
```

```
// 5. Same as: t1 = "2"; Int32 t2 = 3;
//
M(t2, t1, default(DateTime), new Guid());
M(s: (s_n++).ToString(), x: s_n++);
}
```

When I run this program, I get the following output:

```
x=9, s=A, dt=1/1/0001 12:00:00 AM, guid=00000000-0000-0000-0000-000000000000
x=8, s=X, dt=1/1/0001 12:00:00 AM, guid=00000000-0000-0000-0000-000000000000
x=5, s=A, dt=8/6/2012 10:14:25 PM, guid=d2a5a9da-6009-4aae-9295-839155811309
x=0, s=I, dt=1/1/0001 12:00:00 AM, guid=00000000-0000-0000-0000-000000000000
x=3, s=2, dt=1/1/0001 12:00:00 AM, guid=00000000-0000-0000-0000-000000000000
```

As you can see, whenever arguments are left out at the call site, the C# compiler embeds the parameter's default value. The third and fifth calls to M use C#'s named parameter feature. In this case, I'm explicitly passing a value for x and indicating that I want to pass an argument for the parameters named guid and dt.

When you pass arguments to M, the compiler evaluates the arguments from left to right. In the fourth call to M, s_n (0) is passed for x, s_n (1) is passed as a string for s then s_n is incremented to 2. When you pass arguments using named parameters, the compiler still evaluates the arguments from left to right. In the fifth call to M, the value in s_n (2) is converted to a string and saved in a temporary variable (t1) that the compiler creates. s_n is incremented to 3 and this value is saved in another temporary variable (t2) created by the compiler, then s_n is incremented to 4. Ultimately, M is invoked, passing it t2, t1, a default DateTime, and a new Guid.

# Rules and Guidelines

There are some additional rules and guidelines that you should know about when defining a method that specifies default values for some of its parameters:

+   - You can specify default values for the parameters of methods, constructor methods, and parameter properties (C# indexers). You can also specify default values for parameters that are part of a delegate definition. Then, when invoking a variable of this delegate type, you may omit the arguments and accept the default values.

+   - Parameters with default values may come after others that do not have default values. That is, after you define a parameter as having a default value, then all parameters to the right of it must also have default values. For example, in the definition of my M method, I would get a compiler error if I removed the default value ("") for s. There is one exception to this rule: a params array parameter (discussed later in this chapter) must come after all parameters (including those that have default values), and the array cannot have a default value itself.