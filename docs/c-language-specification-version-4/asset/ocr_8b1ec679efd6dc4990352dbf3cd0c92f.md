The set of methods encapsulated by a delegate instance is called an invocation list. When a delegate instance is created (§15.2) from a single method, it encapsulates that method, and its invocation list contains only one entry. However, when two non-null delegate instances are combined, their invocation lists are concatenated—in the order left operand then right operand—to form a new invocation list, which contains two or more entries.

Delegates are combined using the binary + (§7.8.4) and += operators (§7.17.2). A delegate can be removed from a combination of delegates, using the binary - (§7.8.5) and -= operators (§7.17.2). Delegates can be compared for equality (§7.10.8).

The following example shows the instantiation of a number of delegates, and their corresponding invocation lists:

```
delegate void D(int x);
class C
{
    public static void M1(int i) {...}
    public static void M2(int i) {...}
}
class Test
{
    static void Main() {
        D cd1 = new D(C.M1);      // M1
        D cd2 = new D(C.M2);      // M2
        D cd3 = cd1 + cd2;        // M1 + M2
        D cd4 = cd3 + cd1;        // M1 + M2 + M1
        D cd5 = cd4 + cd3;        // M1 + M2 + M1 + M1 + M2
    }
}
```

When cd1 and cd2 are instantiated, they each encapsulate one method. When cd3 is instantiated, it has an invocation list of two methods, M1 and M2, in that order. cd4’s invocation list contains M1, M2, and M1, in that order. Finally, cd5’s invocation list contains M1, M2, M1, M1, and M2, in that order. For more examples of combining (as well as removing) delegates, see §15.4.

# 15.2 Delegate compatibility

A method or delegate M is *compatible* with a delegate type D if all of the following are true:

+   * D and M have the same number of parameters, and each parameter in D has the same `ref` or `out` modifiers as the corresponding parameter in M.
+   * For each value parameter (a parameter with no `ref` or `out` modifier), an identity conversion (§6.1.1) or implicit reference conversion (§6.1.6) exists from the parameter type in D to the corresponding parameter type in M.
+   * For each `ref` or `out` parameter, the parameter type in D is the same as the parameter type in M.
+   * An identity or implicit reference conversion exists from the return type of M to the return type of D.

# 15.3 Delegate instantiation

An instance of a delegate is created by a *delegate-creation-expression* (§7.6.10.5) or a conversion to a delegate type. The newly created delegate instance then refers to either:

+   * The static method referenced in the *delegate-creation-expression*, or
+   * The target object (which cannot be `null`) and instance method referenced in the *delegate-creation-expression*, or