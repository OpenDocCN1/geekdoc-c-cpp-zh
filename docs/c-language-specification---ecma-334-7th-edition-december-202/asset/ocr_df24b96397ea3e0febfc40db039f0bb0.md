# 20.3 Delegate members

Every delegate type inherits members from the Delegate class as described in §15.3.4. In addition, every delegate type must provide a non-generic Invoke method whose parameter list matches the formal_parameter_list in the delegate declaration, whose return type matches the return_type or ref_return_type in the delegate declaration, and for returns-by-ref delegates whose ref_kind matches that in the delegate declaration. The Invoke method shall be at least as accessible as the containing delegate type. Calling the Invoke method on a delegate type is semantically equivalent to using the delegate invocation syntax (§20.6).

Implementations may define additional members in the delegate type.

Except for instantiation, any operation that can be applied to a class or class instance can also be applied to a delegate class or instance, respectively. In particular, it is possible to access members of the System.Delegate type via the usual member access syntax.

# 20.4 Delegate compatibility

A method or delegate type M is compatible with a delegate type D if all of the following are true:

+   - D and M have the same number of parameters, and each parameter in D has the same in, out, or ref modifiers as the corresponding parameter in M.
+   - For each value parameter, an identity conversion (§10.2.2) or implicit reference conversion (§10.2.8) exists from the parameter type in D to the corresponding parameter type in M.
+   - For each in, out, or ref parameter, the parameter type in D is the same as the parameter type in M.
+   - One of the following is true:
+     - D and M are both returns-no-value
+     - D and M are returns-by-value (§15.6.1, §20.2), and an identity or implicit reference conversion exists from the return type of M to the return type of D.
+     - D and M are both returns-by-ref, an identity conversion exists between the return type of M and the return type of D, and both have the same ref_kind.

This definition of compatibility allows covariance in return type and contravariance in parameter types.

Example:

```
delegate int D1(int i, double d);
delegate int D2(int c, double d);
delegate object D3(string s);

class A
{
    public static int M1(int a, double b) {...}
}

class B
{
    public static int M1(int f, double g) {...}
    public static void M2(int k, double l) {...}
    public static int M3(int g) {...}
    public static void M4(int g) {...}
```