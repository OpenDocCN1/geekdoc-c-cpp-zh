
现在，碰巧我们的解决方案已经知道如何对包含两个元素的列表进行排序。而 `greaters` 正是这样一个列表，因此我们可以通过对 `greaters` 列表调用 `sort` 来让这个测试通过：

点击此处查看代码图像

```java
List<Integer> result = new ArrayList<>();
result.addAll(lessers);
result.add(middle);
result.addAll(sort(greaters));
return result;
```

这使 `[1,3,2]` 测试通过了，但 `[3,2,1]` 测试失败了，因为 `lessers` 列表无序。不过这是一个很容易的修复：

点击此处查看代码图像

```java
List<Integer> result = new ArrayList<>();
result.addAll(sort(lessers));
result.add(middle);
result.addAll(sort(greaters));
return result;
```

所以，是的，我们应该在继续处理四元素列表之前，先尝试三个元素剩下的两种情况。

> 规则 7：在测试下一个更复杂的情况之前，先穷尽当前较简单的情况。

总之，现在我们需要让那个四元素列表的测试通过。于是，我们取消注释该测试，并看到它失败了（未展示）。

我们目前用于对三元素列表排序的算法可以推广，尤其是现在 `middle` 变量是列表的第一个元素。要构建 `lessers` 和 `greaters` 列表，我们只需应用过滤器：

点击此处查看代码图像

```java
else {
    int middle = list.get(0);
    List<Integer> lessers =
        list.stream().filter(x -> x < middle).collect(toList());
    List<Integer> greaters =
        list.stream().filter(x -> x > middle).collect(toList());
    List<Integer> result = new ArrayList<>();
    result.addAll(sort(lessers));
    result.add(middle);
    result.addAll(sort(greaters));
    return result;
    }
```

毫不意外，这通过了，并且也通过了接下来的两个测试：

[点击此处查看代码图像]()

```java
assertEquals(asList(1, 2, 3, 4), sort(asList(2, 1, 3, 4)));
assertEquals(asList(1, 2, 3, 4), sort(asList(4, 3, 2, 1)));
```

但现在你可能会疑惑那个 `middle`。如果 `middle` 元素在列表中不唯一呢？我们来试试：

[点击此处查看代码图像]()

```java
assertEquals(asList(1, 1, 2, 3), sort(asList(1, 3, 1, 2)));
```

是的，它失败了。这只是意味着我们不应该再把 `middle` 当作特殊的东西：

[点击此处查看代码图像]()

```java
else {
    int middle = list.get(0);
    List<Integer> middles =
        list.stream().filter(x -> x == middle).collect(toList());
    List<Integer> lessers =
        list.stream().filter(x -> x < middle).collect(toList());
    List<Integer> greaters =
        list.stream().filter(x -> x > middle).collect(toList());


    List<Integer> result = new ArrayList<>();
    result.addAll(sort(lessers));
    result.addAll(middles);
    result.addAll(sort(greaters));
    return result;
}
```

这通过了。不过，看看上面那个 `else`。还记得它上面是什么吗？来，我展示给你看：

[点击此处查看代码图像]

```java
if (list.size() <= 1)
    return list;
else if (list.size() == 2){
    int first = list.get(0);
    int second = list.get(1);
    if (first > second)
        return asList(second, first);
    else
        return asList(first, second);
}
```

那个 == 2 的情况现在真的还有必要吗？没有必要。移除它后，所有测试仍然通过。

好，那么第一个 `if` 语句呢？它还有必要吗？实际上，它可以改成更好的写法。而且，事实上，让我直接给你看最终算法：

[点击此处查看代码图像]

```java
private List<Integer> sort(List<Integer> list) {
    List<Integer> result = new ArrayList<>();

    if (list.size() == 0)
        return result;
    else {
        int middle = list.get(0);
        List<Integer> middles =
            list.stream().filter(x -> x == middle).collect(toList());
        List<Integer> lessers =
            list.stream().filter(x -> x < middle).collect(toList());
        List<Integer> greaters =
            list.stream().filter(x -> x > middle).collect(toList());

        result.addAll(sort(lessers));
        result.addAll(middles);
        result.addAll(sort(greaters));
        return result;
    }
}
```

这个算法有一个名字。它叫做*快速排序*。它是已知最好的排序算法之一。

它好多少呢？这个算法在我的笔记本电脑上，可以在 1.5 秒内对包含 100 万个介于 0 到 100 万之间的随机整数的数组进行排序。上一节中的冒泡排序则大约需要六个月才能对同样的列表完成排序。所以……更好。

这引出了一个令人不安的观察。对于排序一个有两个元素且顺序错误的列表，曾有两种不同的解决方案。一种解决方案直接引导我们走向冒泡排序，另一种解决方案直接引导我们走向快速排序。这意味着识别岔路口并选择正确的路径，有时会相当重要。在这个例子中，一条路径引导我们走向一个相当差的算法，另一条路径则引导我们走向一个非常好的算法。

我们能识别这些岔路口并确定该选择哪条路径吗？也许可以。但那是更高级章节的主题。

### 陷入困境

到这里，我想你已经看了足够多的视频，对 TDD 的节奏有了很好的了解。从现在开始，我们将不再使用视频，只依靠本章的文字。

TDD 新手经常会发现自己陷入困境。他们写了一个非常好的测试，然后发现让该测试通过的唯一方法就是一次性实现整个算法。我把这种情况称为“陷入困境”。

摆脱困境的方法是删除你最后写的测试，并找到一个更简单的测试来通过。

> 规则 8：如果你为了让当前测试通过而必须实现太多内容，那就删除该测试，并写一个你更容易通过的更简单的测试。

在我的课堂练习中，我经常使用下面这个练习来让人陷入困境。它相当可靠。尝试它的人中，远超过一半会发现自己陷入困境，并且也发现很难脱身。

这个问题就是经典的自动换行问题：给定一个没有任何换行符的文本字符串，插入适当的换行符，使文本能适应宽度为 n 个字符的列。如果可能的话，在单词处换行。

学生应该编写以下函数：

点击此处查看代码图像

```
Wrapper.wrap(String s, int w);
```

假设输入字符串是葛底斯堡演说：

点击此处查看代码图像

```
"Four score and seven years ago our fathers brought forth upon this
continent a new nation conceived in liberty and dedicated to the
proposition that all men are created equal"
```

现在，如果期望宽度是 30，那么输出应该是

点击此处查看代码图像

```
=======:=======:=======:=======:=======:
Four score and seven years ago
Our fathers brought forth upon
This continent a new nation
Conceived in liberty and
Dedicated to the proposition
That all men are created equal
=======:=======:=======:=======:=======:
```

你会如何以测试优先的方式编写这个算法？我们可能像往常一样从这个失败的测试开始：

点击此处查看代码图像

```java
public class WrapTest {
    @Test
    public void testWrap() throws Exception {
        assertEquals("Four", wrap("Four", 7));
    }
    private String wrap(String s, int w) {
        return null;
    }
}
```

又是那个模式。我们通过返回退化的常量让第一个测试通过。我们通过返回输入让第二个测试通过。有意思。好，那么下一个最退化的测试是什么？

点击此处查看代码图像

```
assertWrapped("xx", 1, "x\nx");
```

它失败了，因为它返回 "xx"。不过让它通过并不难：

点击此处查看代码图像

```
private String wrap(String s, int w) {
  if (w >= s.length())
    return s;
  else
    return s.substring(0, w) + "\n" + s.substring(w);
}
```

这很容易。那么，下一个最退化的测试是什么？

点击此处查看代码图像

```
assertWrapped("xx", 2, "xx");
```

那个测试已经通过了。很好。那么，下一个测试将是

点击此处查看代码图像

```
assertWrapped("xxx", 1, "x\nx\nx");
```

这个测试失败了。并且它暗示了某种循环。但等等。有一种更简单的方法：

点击此处查看代码图像

```
private String wrap(String s, int w) {
  if (w >= s.length())
    return s;
  else
    return s.substring(0, w) + "\n" + wrap(s.substring(w), w);
}
```
