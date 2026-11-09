```
public String compact(String message) {
    if (shouldNotCompact())
        return Assert.format(message, expected, actual);
    findCommonPrefix();
    findCommonSuffix();
    String expected = compactString(this.expected);
    String actual = compactString(this.actual);
    return Assert.format(message, expected, actual);
}
private boolean shouldNotCompact() {
    return expected == null || actual == null || areStringsEqual();
}
```

I don’t much care for the `this.expected` and `this.actual` notation in the `compact` function. This happened when we changed the name of `fExpected` to expected. Why are there variables in this function that have the same names as the member variables? Don’t they represent something else [N4]? We should make the names unambiguous.

```
String compactExpected = compactString(expected);    String
compactActual = compactString(actual);
```

Negatives are slightly harder to understand than positives [G29]. So let’s turn that `if` statement on its head and invert the sense of the conditional.

```
public String compact(String message) {
    if (canBeCompacted()) {
        findCommonPrefix();
        findCommonSuffix();
        String compactExpected = compactString(expected);
        String compactActual = compactString(actual);
        return Assert.format(message, compactExpected, compactActual);
    } else {
        return Assert.format(message, expected, actual);
    }
}
private boolean canBeCompacted() {
    return expected != null && actual != null && ! areStringsEqual();
}
```