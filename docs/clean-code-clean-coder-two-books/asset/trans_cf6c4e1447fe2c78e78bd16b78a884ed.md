
这个函数的名字有点奇怪 [N7]。虽然它确实会压缩字符串，但如果 `canBeCompacted` 返回 `false`，它实际上可能不会压缩字符串。所以将函数命名为 `compact` 会隐藏错误检查的副作用。还要注意，该函数返回的是一个格式化后的消息，而不仅仅是压缩后的字符串。因此，这个函数实际上应该命名为 `formatCompactedComparison`。当与函数参数放在一起时，这样读起来会好得多：

```java
public String formatCompactedComparison(String message) {
```

`if` 语句体里做的才是真正压缩 expected 和 actual 字符串的工作。我们应该将其提取为一个名为 `compactExpectedAndActual` 的方法。然而，我们希望 `formatCompactedComparison` 函数完成所有格式化。`compact...` 函数应该只做压缩这件事，不做其他 [G30]。所以让我们把它拆分成如下形式：

```java
...

private String compactExpected;
private String compactActual;

...

public String formatCompactedComparison(String message) {
  if (canBeCompacted()) {
    compactExpectedAndActual();
    return Assert.format(message, compactExpected, compactActual);
  } else {
    return Assert.format(message, expected, actual);
  }
}
private void compactExpectedAndActual() {
  findCommonPrefix();
  findCommonSuffix();
  compactExpected = compactString(expected);
  compactActual = compactString(actual);
}
```

注意，这要求我们将 `compactExpected` 和 `compactActual` 提升为成员变量。我不喜欢这个新函数最后两行返回变量，而前两行却没有。它们

```java
private void compactExpectedAndActual() {
    prefixIndex = findCommonPrefix();
    suffixIndex = findCommonSuffix(prefixIndex);
    compactExpected = compactString(expected);
    compactActual = compactString(actual);
}
private int findCommonSuffix(int prefixIndex) {
    int expectedSuffix = expected.length() - 1;
    int actualSuffix = actual.length() - 1;
    for (; actualSuffix >= prefixIndex && expectedSuffix >= prefixIndex;
            actualSuffix--, expectedSuffix--) {
        if (expected.charAt(expectedSuffix) != actual.charAt(actualSuffix))
            break;
    }
    return expected.length() - expectedSuffix;
}
```

我对此并不满意。`prefixIndex` 参数的传递有点随意 [G32]。它确实能建立顺序，但完全没有解释为什么需要这种顺序。另一位程序员可能会撤销我们刚才所做的工作，因为没有任何迹象表明这个参数是真正需要的。所以我们换一种思路。

```java
private void compactExpectedAndActual() {
    findCommonPrefixAndSuffix();
    compactExpected = compactString(expected);
    compactActual = compactString(actual);
}
private void findCommonPrefixAndSuffix() {
    findCommonPrefix();
    int expectedSuffix = expected.length() - 1;
    int actualSuffix = actual.length() - 1;
    for (
        actualSuffix >= prefixIndex && expectedSuffix >= prefixIndex;
        actualSuffix--, expectedSuffix--
    ) {
        if (expected.charAt(expectedSuffix) != actual.charAt(actualSuffix))
            break;
    }
    suffixIndex = expected.length() - expectedSuffix;
}
private void findCommonPrefix() {
    prefixIndex = 0;
    int end = Math.min(expected.length(), actual.length());
    for (; prefixIndex < end; prefixIndex++)
        if (expected.charAt(prefixIndex) != actual.charAt(prefixIndex))
            break;
}
```

我们让 `findCommonPrefix` 和 `findCommonSuffix` 恢复原样，将 `findCommonSuffix` 改名为 `findCommonPrefixAndSuffix`，并让它先调用 `findCommonPrefix` 再执行其他操作。与之前的解决方案相比，这更显著地确立了两个函数之间的先后关系。这也暴露了 `findCommonPrefixAndSuffix` 的丑陋之处。现在我们来清理一下。

```java
private void findCommonPrefixAndSuffix() {
    findCommonPrefix();
    int suffixLength = 1;
    for (; !suffixOverlapsPrefix(suffixLength); suffixLength++) {
        if (charFromEnd(expected, suffixLength) !=
            charFromEnd(actual, suffixLength))
            break;
    }
    suffixIndex = suffixLength;
}
private char charFromEnd(String s, int i) {
    return s.charAt(s.length()-i);
}
private boolean suffixOverlapsPrefix(int suffixLength) {
    return actual.length() - suffixLength < prefixLength ||
           expected.length() - suffixLength < prefixLength;
}
```

这样好多了。它暴露了 `suffixIndex` 实际上是后缀的长度，命名不佳。`prefixIndex` 也是如此，尽管在那种情况下“index”和“length”是同义词。即便如此，使用 “length” 更为一致。问题在于 `suffixIndex` 变量不是从 0 开始的；它是从 1 开始的，因此并不是真正的长度。这也是 `computeCommonSuffix` 中出现所有那些 +1 的原因 [G33]。所以我们来修复它。结果如[清单15-4](#)所示。

### 清单 15-4 ComparisonCompactor.java（中间版）

```java
public class ComparisonCompactor {
...
    private int suffixLength;
...
    private void findCommonPrefixAndSuffix() {
        findCommonPrefix();
        suffixLength = 0;
        for (; !suffixOverlapsPrefix(suffixLength); suffixLength++) {
            if (charFromEnd(expected, suffixLength) !=
                charFromEnd(actual, suffixLength))
                break;
        }
    }
    private char charFromEnd(String s, int i) {
        return s.charAt(s.length() - i - 1);
    }
    private boolean suffixOverlapsPrefix(int suffixLength) {
        return actual.length() - suffixLength <= prefixLength ||
            expected.length() - suffixLength <= prefixLength;
    }
...
    private String compactString(String source) {
        String result =
            DELTA_START +
            source.substring(prefixLength, source.length() - suffixLength) +
            DELTA_END;
        if (prefixLength > 0)
            result = computeCommonPrefix() + result;
        if (suffixLength > 0)
            result = result + computeCommonSuffix();
        return result;
    }
```

```java
source.substring(prefixLength, source.length() - suffixLength) +
DELTA_END +
computeCommonSuffix();
}
```

这样好多了！现在我们看到 `compactString` 函数只是简单地将各个片段组合在一起。我们也许还能让它更清晰。确实，还有很多小的清理可以做。但与其带你逐一浏览其余的修改，不如直接展示结果，见[清单15-5](#)。

### 清单 15-5 ComparisonCompactor.java（最终版）

```java
package junit.framework;
public class ComparisonCompactor {

    private static final String ELLIPSIS = "...";
    private static final String DELTA_END = "]";
    private static final String DELTA_START = "[";
    private int contextLength;
    private String expected;
    private String actual;
    private int prefixLength;
    private int suffixLength;

    public ComparisonCompactor(
        int contextLength, String expected, String actual
    ) {
        this.contextLength = contextLength;
        this.expected = expected;
        this.actual = actual;
    }

    public String formatCompactedComparison(String message) {
        String compactExpected = expected;
        String compactActual = actual;
        if (shouldBeCompacted()) {
            findCommonPrefixAndSuffix();
            compactExpected = compact(expected);
            compactActual = compact(actual);
        }
        return Assert.format(message, compactExpected, compactActual);
    }

    private boolean shouldBeCompacted() {
        return !shouldNotBeCompacted();
    }

    private boolean shouldNotBeCompacted() {
        return expected == null ||
            actual == null ||
            expected.equals(actual);
    }

    private void findCommonPrefixAndSuffix() {
        findCommonPrefix();
        suffixLength = 0;
        for (; !suffixOverlapsPrefix(); suffixLength++) {
            if (charFromEnd(expected, suffixLength) !=
                charFromEnd(actual, suffixLength))
                break;
        }
    }
    private char charFromEnd(String s, int i) {
        return s.charAt(s.length() - i - 1);
    }
    private boolean suffixOverlapsPrefix() {
        return actual.length() - suffixLength <= prefixLength ||
            expected.length() - suffixLength <= prefixLength;
    }

    private void findCommonPrefix() {
        prefixLength = 0;
        int end = Math.min(expected.length(), actual.length());
```
