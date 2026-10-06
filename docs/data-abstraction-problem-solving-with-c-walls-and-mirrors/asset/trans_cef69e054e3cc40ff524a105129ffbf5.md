

```cpp
@param s 要反序写入的字符串。
void writeBackward(string s)
{
    int length = s.size(); // 字符串的长度
    if (length > 0) {
        // 写入最后一个字符
        cout << s.substr(length - 1, 1);

        // 反序写入字符串剩余部分
        writeBackward(s.substr(0, length - 1)); // Point A
    } // end if
    // length == 0 是基础情况 - 什么都不做
} // end writeBackward
```

注意，对 `writeBackward` 的递归调用连续使用更短的字符串版本，确保能够到达基础情况。该函数在到达基础情况时并没有返回，它没有显式地处理基础情况。基础情况是隐式的。正如之前的情况一样

你可以使用框图追踪（box trace）来追踪 `writeBackward` 的执行过程。正如函数 `fact`一样，每个框都包含递归调用的局部环境——在这种情况下，即输入参数和局部变量。该追踪与图 2-5 所示的 `fact` 追踪有所不同，因为作为一个 `void` 函数，`writeBackward` 没有使用 `return` 语句来返回计算值。图 2-7 追踪了带有字符串 "cat" 的函数 `writeBackward` 的调用。

writeBackward 不返回计算值

# 图 2-7 writeBackward("cat") 的框图

发起了初始调用，函数开始执行：

| s = "cat" |
| length = 3 |

输出行：t
到达 Point A (writeBackward(s))，并发起了递归调用。
新的调用开始执行：

| s = "cat" |
| length = 3 | -> | s = "ca" |
| length = 2 |

输出行：ta
到达 Point A，并发起了递归调用。
新的调用开始执行：

| s = "cat" |
| length = 3 | -> | s = "ca" |
| length = 2 | -> -> | s = "c" |
| length = 1 |

（继续）

# 图 2-7 writeBackward("cat") 的框图（续）

输出行：tac

到达 Point A，并发起了递归调用。

新的调用开始执行：

| s = "cat" | A | s = "ca" | A | s = "c" | A | s = "" |
| length = 3 | | length = 2 | | length = 1 | | length = 0 |

这是基础情况，因此该调用完成。

控制权返回到调用框，它继续执行：

| s = "cat" | A | s = "ca" | A | s = "c" | A | s = "" |
| length = 3 | | length = 2 | | length = 1 | | length = 0 |

该调用完成。控制权返回到调用框，它继续执行：

| s = "cat" | A | s = "ca" | A | s = "c" | A | s = "" |
| length = 3 | | length = 2 | | length = 1 | | length = 0 |

该调用完成。控制权返回到调用框，它继续执行：

| s = "cat" | A | s = "ca" | A | s = "c" | A | s = "" |
| length = 3 | | length = 2 | | length = 1 | | length = 0 |

该调用完成。控制权返回到初始调用之后的语句。

另一种解决方案。现在考虑一种解决该问题的稍微不同的方法。回想从字符串中去掉字符的两种选择：最后一个字符或第一个字符。该解决方案仅剥离字符串的最后一个字符。现在，从第二种选择构造一个解决方案将非常有趣：

### 剥离第一个字符

首先，考虑之前伪代码中的一种简单方法，将“最后一个”的出现替换为“第一个”。因此，函数写入第一个字符而不是最后一个，并递归地写入字符串的剩余部分。

```
writeBackward1(s: string)
if (string s为空)
    什么都不做——这是基础情况
else{
    写入 s 的第一个字符
    writeBackward1(s 减去它的第一个字符)
}
```

这个解决方案符合你的预期吗？如果你思考这个函数，你会发现它是按照从左到右的顺序写入字符串的，而不是反序。毕竟，伪代码中的步骤仅仅是写入了字符串。将函数命名为 `writeBackward` 并不能保证它实际上会反序写入字符串——递归真的是魔法！你可以使用以下递归公式来反序写入 `s`：

换句话说，只有在你写入了 `s` 的剩余部分之后，才写入第一个字符。这种方法导致了以下伪代码：

```
writeBackward(s: string)
  if (string为空)
    什么都不做——这是基础情况
  else
    writeBackward(s 减去它的第一个字符)
```

将 `writeBackward` 翻译成 C++ 与原始的 `writeBackward` 函数类似，并留作一个练习题。仔细追踪两个伪代码函数 `writeBackward` 和 `write2` 的动作是有益益的。首先，在每个函数中添加语句以产生有助于追踪的输出，例如：

```
writeBackward(s: string)
cout << "writeBackward with string: " << s << endl;
if (string为空)
    什么都不做——这是基础情况
else
    cout << "About to write last character of string: " << s << endl;
    writeBackward(s 减去它的最后一个字符) // Point A
cout << "Leave writeBackward with string: " << s << endl;
```

```
writeBackward2(s: string)
cout << "writeBackward2 with string: " << s << endl;
if (string为空)
    什么都不做——这是基础情况
else
    cout << "About to write first character of string: " << s << endl;
    writeBackward2(s 减去它的第一个字符)
cout << "Leave writeBackward2 with string: " << s << endl;
```

图 2-8 和 2-9 显示了修改后的伪代码函数 `writeBackward` 和 `write2` 的输出，它们带有字符串 "cat"。

# 图 2-8 writeBackward("cat") 的框图

发起了初始调用，函数开始执行：

| s = "cat" |
| length = 3 |

输出行：t
到达 Point A (writeBackward(s))，并发起了递归调用。
新的调用开始执行：

| s = "cat" |
| length = 3 | -> | s = "ca" |
| length = 2 |

输出行：ta
到达 Point A，并发起了递归调用。
新的调用开始执行：

| s = "cat" |
| length = 3 | -> | s = "ca" |
| length = 2 | -> -> | s = "c" |
| length = 1 |

（继续）

# 图 2-7 writeBackward("cat") 的框图（续）

输出行：tac

到达 Point A，并发起了递归调用。

新的调用开始执行：

| s = "cat" | A | s = "ca" | A | s = "c" | A | s = "" |
| length = 3 | | length = 2 | | length = 1 | | length = 0 |

这是基础情况，因此该调用完成。

控制权返回到调用框，它继续执行：

| s = "cat" | A | s = "ca" | A | s = "c" | A | s = "" |
| length = 3 | | length = 2 | | length = 1 | | length = 0 |

该调用完成。控制权返回到调用框，它继续执行：

| s = "cat" | A | s = "ca" | A | s = "c" | A | s = "" |
| length = 3 | | length = 2 | | length = 1 | | length = 0 |

该调用完成。控制权返回到调用框，它继续执行：

| s = "cat" | A | s = "ca" | A | s = "c" | A | s = "" |
| length = 3 | | length = 2 | | length = 1 | | length = 0 |

该调用完成。控制权返回到初始调用之后的语句。

writeBackward 不返回计算值

