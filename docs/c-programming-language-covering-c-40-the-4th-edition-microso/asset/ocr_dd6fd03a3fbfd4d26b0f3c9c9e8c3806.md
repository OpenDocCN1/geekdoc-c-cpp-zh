The set of methods encapsulated by a delegate instance is called an invocation list. When a delegate instance is created (§15.2) from a single method, it encapsulates that method, and its invocation list contains only one entry. However, when two non-null delegate instances are combined, their invocation lists are concatenated—in the order left operand then right operand—to form a new invocation list, which contains two or more entries.

> > **JON SKEET** This single-cast/multicast duality is terribly awkward in some ways—and wonderfully useful in others. For example, it makes sense to talk about “the target” of a single-cast delegate, whereas each entry in the invocation list for a multicast delegate may have a separate target. This rarely presents a practical problem, but can make hard to describe delegates both simply and accurately.

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