The Slice method is available on the string[], and the ToInt32 method is available on string, because they have been declared as extension methods. The meaning of the program is the same as the following, using ordinary static method calls:

```
static class Program
{
    static void Main() {
        string[] strings = { "1", "22", "333", "4444" };
        foreach (string s in Extensions.Slice(strings, 1, 2)) {
            Console.WriteLine(Extensions.ToInt32(s));
        }
    }
}
```

end example]

# 15.6.11 Method body

The method-body of a method declaration consists of either a block or a semicolon.

Abstract and external method declarations do not provide a method implementation, so their method bodies simply consist of a semicolon. For any other method, the method body is a block (§13.3) that contains the statements to execute when that method is invoked.

The effective return type of a method is void if the return type is void, or if the method is async and the return type is System.Threading.Tasks.Task. Otherwise, the effective return type of a non-async method is its return type, and the effective return type of an async method with return type System.Threading.Tasks.Task<T> is T.

When the effective return type of a method is void, return statements (§13.10.5) in that method's body are not permitted to specify an expression. If execution of the method body of a void method completes normally (that is, control flows off the end of the method body), that method simply returns to its caller.

When the effective return type of a method is not void, each return statement in that method's body shall specify an expression that is implicitly convertible to the effective return type. The endpoint of the method body of a value-returning method shall not be reachable. In other words, in a value-returning method, control is not permitted to flow off the end of the method body.

[Example: In the following code

```
class A
{
    public int F() {}    // Error, return value required
    public int G() {
        return 1;
    }

    public int H(bool b) {
        if (b) {
            return 1;
        }
        else { return 0; }
    }
}
```

the value-returning F method results in a compile-time error because control can flow off the end of the method body. The G and H methods are correct because all possible execution paths end in a return statement that specifies a return value. end example]