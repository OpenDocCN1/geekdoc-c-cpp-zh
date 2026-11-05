
The set of methods encapsulated by a delegate instance is called an invocation list. When a delegate instance is created (§15.2) from a single method, it encapsulates that method, and its invocation list contains only one entry. However, when two non-null delegate instances are combined, their invocation lists are concatenated—in the order left operand then right operand—to form a new invocation list, which contains two or more entries.

> **JON SKEET** This single-cast/multicast duality is terribly awkward in some ways—and wonderfully useful in others. For example, it makes sense to talk about “the target” of a single-cast delegate, whereas each entry in the invocation list for a multicast delegate may have a separate target. This rarely presents a practical problem, but can make it hard to describe delegates both simply and accurately.

Delegates are combined using the binary + (§7.8.4) and += operators (§7.17.2). A delegate can be removed from a combination of delegates by using the binary - (§7.8.5) and -= operators (§7.17.2). Delegates can also be compared for equality (§7.10.8).

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
    static void Main()
    {
        D cd1 = new D(C.M1);     // M1
        D cd2 = new D(C.M2);     // M2
        D cd3 = cd1 + cd2;       // M1 + M2
        D cd4 = cd3 + cd1;       // M1 + M2 + M1
        D cd5 = cd4 + cd3;       // M1 + M2 + M1 + M1 + M2
    }
}
```

When cd1 and cd2 are instantiated, they each encapsulate one method. When cd3 is instantiated, it has an invocation list of two methods, M1 and M2, in that order. cd4’s invocation list contains M1, M2, and M1, in that order. Finally, cd5’s invocation list contains M1, M2, M1, M1, and M2, in that order. For more examples of combining (as well as removing) delegates, see §15.4.

### 15.2 Delegate Compatibility

A method or delegate M is compatible with a delegate type D if all of the following are true:

- D and M have the same number of parameters, and each parameter in D has the same ref or out modifiers as the corresponding parameter in M.
- For each value parameter (a parameter with no ref or out modifier), an identity conversion (§6.1.1) or implicit reference conversion (§6.1.6) exists from the parameter type in D to the corresponding parameter type in M.
- For each ref or out parameter, the parameter type in D is the same as the parameter type in M.
- An identity or implicit reference conversion exists from the return type of M to the return type of D.

### 15.3 Delegate Instantiation

An instance of a delegate is created by a delegate-creation-expression (§7.6.10.5) or a conversion to a delegate type. The newly created delegate instance then refers to either

- The static method referenced in the delegate-creation-expression, or
- The target object (which cannot be null) and instance method referenced in the delegate-creation-expression, or
- Another delegate.

For example:

```
delegate void D(int x);
class C
{
    public static void M1(int i) {...}
    public void M2(int i) {...}
}
class Test
{
    static void Main()
    {
        D cd1 = new D(C.M1);      // Static method
        C t = new C();
        D cd2 = new D(t.M2);      // Instance method
        D cd3 = new D(cd2);       // Another delegate
    }
}
```

Once instantiated, delegate instances always refer to the same target object and method. Remember, when two delegates are combined, or one is removed from another, a new delegate results with its own invocation list; the invocation lists of the delegates combined or removed remain unchanged.

### 15.4 Delegate Invocation

C# provides special syntax for invoking a delegate. When a non-null delegate instance whose invocation list contains one entry is invoked, it invokes the one method with the same arguments it was given, and returns the same value as the referred-to method. (See §7.6.5.3 for detailed information on delegate invocation.) If an exception occurs during the invocation of such a delegate, and that exception is not caught within the method that was invoked, the search for an exception catch clause continues in the method that called the delegate, as if that method had directly called the method to which that delegate referred.

Invocation of a delegate instance whose invocation list contains multiple entries proceeds by invoking each of the methods in the invocation list, synchronously, in order. Each method so called is passed the same set of arguments as was given to the delegate instance. If such a delegate invocation includes reference parameters (§10.6.1.2), each method invocation will occur with a reference to the same variable; changes to that variable by one method in the invocation list will be visible to methods further down the invocation list. If the delegate invocation includes output parameters or a return value, their final value will come from the invocation of the last delegate in the list.

If an exception occurs during processing of the invocation of such a delegate, and that exception is not caught within the method that was invoked, the search for an exception catch clause continues in the method that called the delegate, and any methods further down the invocation list are not invoked.

> BILL WAGNER This behavior is why, in the general case, you should strive to create methods that implement delegates that do not throw exceptions under any circumstances. It introduces errors from which you likely cannot safely recover. This consideration is less important when you know your delegate will be used in a single-cast scenario only.

> CHRISTIAN NAGEL There's a way to deal with exceptions that are thrown from handler methods that are referenced by the delegate. Instead of invoking the delegate instance directly, the GetInvocationList method of the delegate can be used to invoke each delegate of the invocation list separately. This invocation can be guarded by a try-catch block. In case of an exception, one way to deal with the failing handler method is to remove it from the invocation list.

Attempting to invoke a delegate instance whose value is null results in an exception of type System.NullReferenceException.

> **JON SKEET** In some ways, this outcome makes perfect sense; in other ways, it’s inconsistent with a null reference’s status as the normal representation of an empty invocation list. This confusion could perhaps have been avoided by each delegate type having a *static* Invoke method—perhaps even an extension method—that could have performed the appropriate nullity check. This solution would be more elegant than the C# compiler automatically performing a null check on each invocation expression. Admittedly, things get more complicated when the delegate type has a non-void return type or uses an out parameter.
>
> Whatever the best solution would have been, it’s undeniably a pain in the neck to have to check for nullity everywhere that you want to invoke a delegate.

> **ERIC LIPPERT** A common pattern for “thread-safe” delegates is to do something like this:
>
> ```
> var temp = this.mydelegate;
> if (temp != null) temp();
> ```
>
> instead of the more obvious solution:
>
> ```
> if (this.mydelegate != null) this.mydelegate();
> ```
>
> The former is safer because if mydelegate can be changed on another thread, then it might be changed to null between the test and the invocation. Moreover, this approach eliminates only one race. Suppose we are using the former code. The temporary caches the current value of mydelegate. On that other thread, mydelegate is set to null, and the global state that the previous contents of mydelegate needs to execute successfully is destroyed. But it is the previous contents that are about to be invoked! If your delegates (particularly delegates associated with events) are susceptible to this problem, then some other mechanism must be implemented to ensure that nothing bad happens if this race occurs. Probably the best thing to do is to write the code to ensure that if a “stale” delegate is invoked, nothing bad happens.

The following example shows how to instantiate, combine, remove, and invoke delegates:

```
using System;
delegate void D(int x);
```
