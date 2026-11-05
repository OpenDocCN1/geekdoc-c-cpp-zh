Because a yield break statement unconditionally transfers control elsewhere, the end point of a yield break statement is never reachable.

> **CHRIS SELLS** I sometimes forget that yield return is not the same as return, in that the code after a yield return can be executed. For example, the code after the first return here can never be executed:

```
int F() {
    return 1;
    return 2; // Can never be executed
}
```

In contrast, the code after the first yield return here can be executed:

```
IEnumerable<int> F() {
    yield return 1;
    yield return 2; // Can be executed
}
```

This often bites me in an if statement:

```
IEnumerable<int> F() {
    if(...) { yield return 1; } // I mean this to be the only
    // thing returned
    yield return 2;           // Oops!
}
```

In these cases, remembering that yield return is not “final” like return is helpful.

> **CHRISTIAN NAGEL** Since C# 1.0, it has been easy to use iterators (the foreach statement). Since C# 2.0, it has been easy to create iterators (the yield statement).