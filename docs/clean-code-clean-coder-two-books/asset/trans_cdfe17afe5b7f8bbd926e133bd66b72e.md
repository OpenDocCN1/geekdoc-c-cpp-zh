
```java
String failure= new ComparisonCompactor(1, "ab",
"ab").compact(null);
assertEquals("expected:<ab> but was:<ab>", failure);
}

public void testNoContextStartAndEndSame() {
    String    failure=   new ComparisonCompactor(0, "abc",
"adc").compact(null);
    assertEquals("expected:<...[b]...> but was:<...[d]...>", failure);
}
public void testStartAndEndContext() {
    String    failure=   new ComparisonCompactor(1, "abc",
"adc").compact(null);
    assertEquals("expected:<a[b]c> but was:<a[d]c>", failure);
}

public void testStartAndEndContextWithEllipses() {
    String failure=
new ComparisonCompactor(1, "abcde", "abfde").compact(null);
    assertEquals("expected:<...b[c]d...> but was:<...b[f]d...>", failure);
}

public void testComparisonErrorStartSameComplete() {
    String    failure=   new ComparisonCompactor(2, "ab",
"abc").compact(null);
    assertEquals("expected:<ab[]> but was:<ab[c]>", failure);
}

public void testComparisonErrorEndSameComplete() {
    String    failure=   new ComparisonCompactor(0, "bc",
"abc").compact(null);
    assertEquals("expected:<[]...> but was:<[a]...>", failure);
}

public void testComparisonErrorEndSameCompleteContext() {
    String    failure=   new ComparisonCompactor(2, "bc",
"abc").compact(null);
    assertEquals("expected:<[]bc> but was:<[a]bc>", failure);
}

public void testComparisonErrorOverlappingMatches() {
    String  failure=  new  ComparisonCompactor(0,  "abc",
"abbc").compact(null);
    assertEquals("expected:<...[]...> but was:<...[b]...>", failure);
}

public void testComparisonErrorOverlappingMatchesContext() {
    String  failure=  new  ComparisonCompactor(2,  "abc",
"abbc").compact(null);
    assertEquals("expected:<ab[]c> but was:<ab[b]c>", failure);
}

public void testComparisonErrorOverlappingMatches2() {
    String failure= new ComparisonCompactor(0, "abcde",
"abcde").compact(null);
    assertEquals("expected:<...[d]...> but was:<...[]...>", failure);
}
public void testComparisonErrorOverlappingMatches2Context() {
    String failure=
    new ComparisonCompactor(2, "abcde", "abcde").compact(null);
    assertEquals("expected:<...cd[d]e> but was:<...cd[]e>", failure);
}

public void testComparisonErrorWithActualNull() {
    String failure= new ComparisonCompactor(0, "a", null).compact(null);
    assertEquals("expected:<a> but was:<null>", failure);
}

public void testComparisonErrorWithActualNullContext() {
    String failure= new ComparisonCompactor(2, "a", null).compact(null);
    assertEquals("expected:<a> but was:<null>", failure);
}

public void testComparisonErrorWithExpectedNull() {
```

```java
break;
}
}
```

你可能会对这个模块有些抱怨。这里有一些冗长的表达式，还有一些奇怪的+1等等。但总的来说，这个模块相当不错。毕竟，它可能看起来像[清单 15-3](#)。

## 清单 15-3 ComparisonCompactor.java（未重构版本）

```java
package junit.framework;

public class ComparisonCompactor {
    private int ctxt;
    private String s1;
    private String s2;
    private int pfx;
    private int sfx;

    public ComparisonCompactor(int ctxt, String s1, String s2) {
        this.ctxt = ctxt;
        this.s1 = s1;
        this.s2 = s2;
    }

    public String compact(String msg) {
        if (s1 == null || s2 == null || s1.equals(s2))
            return Assert.format(msg, s1, s2);

        pfx = 0;
        for (; pfx < Math.min(s1.length(), s2.length()); pfx++) {
            if (s1.charAt(pfx) != s2.charAt(pfx))
                break;
        }

        int sfx1 = s1.length() - 1;
        int sfx2 = s2.length() - 1;
        for (; sfx2 >= pfx && sfx1 >= pfx; sfx2--, sfx1--) {
            if (s1.charAt(sfx1) != s2.charAt(sfx2))
                break;
        }

        sfx = s1.length() - sfx1;
        String cmp1 = compactString(s1);
        String cmp2 = compactString(s2);
        return Assert.format(msg, cmp1, cmp2);
    }

    private String compactString(String s) {
        String result =
            "[" + s.substring(pfx, s.length() - sfx + 1) + "]";
        if (pfx > 0)
            result = (pfx > ctxt ? "..." : "") +
                s1.substring(Math.max(0, pfx - ctxt), pfx) + result;
        if (sfx > 0) {
            int end = Math.min(s1.length() - sfx + 1 + ctxt, s1.length());
            result = result + (s1.substring(s1.length() - sfx + 1, end) +
                (s1.length() - sfx + 1 < s1.length() - ctxt ? "..." : ""));
        }
        return result;
    }
}
```

尽管作者已经将这个模块维护得很好，但*童子军规则*²告诉我们，我们应该让它比我们发现时更干净。那么，我们该如何改进清单 15-2 中的原始代码呢？

我不太喜欢的第一点是成员变量上的`f`前缀[N6]。如今的环境已经让这种作用域编码变得多余。所以让我们去掉所有的`f`。

```java
private int contextLength;
private String expected;
private String actual;
private int prefix;
private int suffix;
```

接下来，`compact`函数开头有一个未封装的条件判断[G28]。

```java
public String compact(String message) {
    if (expected == null || actual == null || areStringsEqual())
        return Assert.format(message, expected, actual);
    findCommonPrefix();
    findCommonSuffix();
    String expected = compactString(this.expected);
    String actual = compactString(this.actual);
    return Assert.format(message, expected, actual);
}
```

这个条件判断应该被封装，以明确我们的意图。所以让我们提取一个方法来解释它。

```java
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

我不太喜欢`compact`函数中的`this.expected`和`this.actual`写法。这是因为我们把`fExpected`改名为expected时造成的。为什么这个函数中会有与成员变量同名的变量？它们难道不代表其他含义吗[N4]？我们应该让这些名称无歧义。

```java
String compactExpected = compactString(expected);
String compactActual = compactString(actual);
```

否定形式比肯定形式更难理解[G29]。所以让我们把那个`if`语句颠倒过来，反转条件判断的含义。

```java
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
    return expected != null && actual != null && !areStringsEqual();
}
```
