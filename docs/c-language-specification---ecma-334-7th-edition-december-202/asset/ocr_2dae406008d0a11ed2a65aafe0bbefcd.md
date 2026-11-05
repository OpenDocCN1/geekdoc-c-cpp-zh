+   - It contains an out or ref parameter
+   - It contains a dynamically bound expression

end note

# 10.8 Method group conversions

An implicit conversion exists from a method group (§12.2) to a compatible delegate type (§20.4). If D is a delegate type, and E is an expression that is classified as a method group, then D is compatible with E if and only if E contains at least one method that is applicable in its normal form (§12.6.4.2) to any argument list (§12.6.2) having types and modifiers matching the parameter types and modifiers of D, as described in the following.

The compile-time application of the conversion from a method group E to a delegate type D is described in the following.

+   - A single method M is selected corresponding to a method invocation (§12.8.9.2) of the form E(A), with the following modifications:
+     - The argument list A is a list of expressions, each classified as a variable and with the type and modifier (in, out, or ref) of the corresponding parameter in the formal_parameter_list of D — excepting parameters of type dynamic, where the corresponding expression has the type object instead of dynamic.
+     - The candidate methods considered are only those methods that are applicable in their normal form and do not omit any optional parameters (§12.6.4.2). Thus, candidate methods are ignored if they are applicable only in their expanded form, or if one or more of their optional parameters do not have a corresponding parameter in D.
+   - A conversion is considered to exist if the algorithm of §12.8.9.2 produces a single best method M which is compatible (§20.4) with D.
+   - If the selected method M is an instance method, the instance expression associated with E determines the target object of the delegate.
+   - If the selected method M is an extension method which is denoted by means of a member access on an instance expression, that instance expression determines the target object of the delegate.
+   - The result of the conversion is a value of type D, namely a delegate that refers to the selected method and target object.

Example: The following demonstrates method group conversions:

```
delegate string D1(object o);
delegate object D2(string s);
delegate object D3();
delegate string D4(object o, params object[] a);
delegate string D5(int i);
class Test
{
    static string F(object o) {...}
    static void G()
    {
        D1 d1 = F;      // Ok
        D2 d2 = F;      // Ok
    }
}
```