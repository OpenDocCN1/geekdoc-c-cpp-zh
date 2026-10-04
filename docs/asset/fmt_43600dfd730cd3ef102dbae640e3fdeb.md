
`MAX_KEY_SIZE` 是一个存储整数 26 的变量。`MAX_KEY_SIZE` 提醒我们程序中使用的密钥在 1 到 26 之间。

```python
def getMode():
    while True:
        print('你想加密还是解密消息？')
        mode = input().lower()
        if mode in ['encrypt', 'decrypt']:
            return mode[0]
        else:
            print('请输入加密(encrypt) 或解密(decrypt)')
```

`getMode()` 函数让用户输入是想加密还是解密消息。`raw_input()` 的返回值调用了 `lower()` 方法，返回小写形式的结果。

```python
def getMessage():
    print('输入消息:')
    return input()

def getKey():
    key = 0
    while True:
        print('请输入密钥数字 (1-%d):' % MAX_KEY_SIZE)
        key = int(input())
        if 1 <= key <= MAX_KEY_SIZE:
            return key
        else:
            print('密钥必须在 1-%d 之间' % MAX_KEY_SIZE)
```

`getMessage()` 函数只是从用户处获取要加密或解密的消息。

`getKey()` 确保函数只返回有效的密钥。有效的密钥是整数值 1 到 26 之间的（记住 `MAX_KEY_SIZE` 的值只有 26）。它返回这个密钥。

```python
def getTranslatedMessage(mode, message, key):
    translated = ''
    if mode == 'd':
        key = -key
    for symbol in message:
        if symbol.isalpha():
            num = ord(symbol)
            if symbol.isupper():
                if num > ord('Z'):
                    num -= 26
                elif num < ord('A'):
                    num += 26
            elif symbol.islower():
                if num > ord('z'):
                    num -= 26
                elif num < ord('a'):
                    num += 26
            translated += chr(num)
        else:
            translated += symbol
    return translated

mode = getMode()
message = getMessage()
key = getKey()
print('你的翻译结果是：')
print(getTranslatedMessage(mode, message, key))
```

（正在解密）。我们只会向此变量拼接字符串，因此我们首先将 `translated` 设置为空空字符串。（你不能将字符串拼接到尚未设置过值的变量上。这是因为你只能将字符串拼接到其他字符串上。如果变量没有值，它就不属于字符串数据类型。）

```
31.   for symbol in message:
32.     if symbol.isalpha():
33.       num = ord(symbol)
34.       num += key
```

我们将对消息字符串中的每个字母（记住在密码学中，它们被称为符号）运行 `for` 循环。字符串被处理为单字符字符串的列表。如果 `message` 包含字符串 'Hello'，那么 `for symbol in 'Hello'` 与 `for symbol in ['H', 'e', 'l', 'l', 'o']` 是一样的。在此循环的每次迭代中，`symbol` 将具有 `message` 中某个字母的值。

## isalpha() 字符串方法

`isalpha()` 字符串方法如果字符串是 A 到 Z 的大写或小写字母，将返回 `True`。如果字符串包含任何非字母字符，`MAX_KEY_SIZE` 将返回 `MAX_KEY_SIZE`。尝试将以下内容输入交互式 shell 中：

```
'Hello'.isalpha()
'Forty two'.isalpha()
'Fortytwo'.isalpha()
'42'.isalpha()
'.isalpha()
```

```
>>> 'Hello'.isalpha()
True
>>> 'Forty two'.isalpha()
False
>>> 'Fortytwo'.isalpha()
True
>>> '42'.isalpha()
False
>>> '.'.isalpha()
False
>>> |
```

如你所示，`'Forty two'.isalpha()` 将返回 `False`，因为 'Forty two' 中包含空格，这是一个非字母字符。`'Fortytwo'.isalpha()` 返回 `True`，因为它没有这个空格。

`'42'.isalpha()` 返回 `False`，因为 '4' 和 '2' 是非字母字符。而 `''.isalpha()` 为 `False`，因为 `isalpha()` 只在字符串仅包含字母字符时返回 `True`，而空字符串并非如此。

我们在第 32 行使用 `if` 语句的原因是因为我们只加密/解密消息中的字母。数字、符号、标点和其他所有其他内容都保持未翻译的形式。

`num` 变量将保存存储在 `symbol` 中的字母的整数序数值。第 34 行通过 `key` 中的值对值进行“偏移”。

## upper() 和 islower() 字符串方法

`upper()` 和 `islower()` 字符串方法（位于第 36 行和 41 行）的工作方式与 `isdigit()` 和 `isalpha()` 方法非常相似。如果调用的字符串包含至少一个大写字母且没有小写字母，`upper()` 将返回 `True`。如果调用的字符串包含至少一个小写字母且没有大写字母，`islower()` 返回 `True`。否则，这些方法返回 `False`。数字和空格等非字母字符的存在不影响结果。尽管，不包含任何字母的字符串（包括空字符串）也会返回 `False`。尝试将以下内容输入交互式 shell 中：

```
'HELLO'.upper()
'hello'.upper()
'hello'.islower()
'Hello'.islower()
'LOOK OUT BEHIND YOU!'.upper()
'42'.upper()
'42'.islower()
''.upper()
''.islower()
```

```
>>> 'HELLO'.isupper()
True
>>> 'hello'.isupper()
False
>>> 'hello'.islower()
True
>>> 'Hello'.islower()
False
>>> 'LOOK OUT YOU!'.isupper()
True
>>> '42'.isupper()
False
>>> '42'.islower()
False
>>> ''.isupper()
False
>>> ''.islower()
False
>>> |
```

## 代码解释继续..

```
36.    if symbol.isupper():
37.        if num > ord('Z'):
38.            num -= 26
39.        elif num < ord('A'):
40.            num += 26
```

这段代码检查符号是否是大写字母。如果是，我们需要考虑两种特殊情况。如果 `symbol` 是 'z' 且 `key` 是 47 呢？如果是这种情况，这里的 `num` 值将是 '^'。这完全不是一个字母。我们希望密文“回到”字母表的开头。我们的方法是检查 `key` 是否大于最大字母的值（即 "Z"）。如果是，我们就从 `num` 中减去 26（因为总共有 26 个字母）。在此之后，`num` 的值为 68，即 'D' 的 ASCII 值。

```
36.    if symbol.islower():
37.        if num > ord('z'):
38.            num -= 26
39.        elif num < ord('a'):
40.            num += 26
```

如果符号是小写字母，程序运行与第 36 到 40 行非常相似。唯一的区别是我们使用 `ord('z')` 和 `ord('a')` 而不是 `ord('Z')` 和 `ord('A')`。

如果是解密，那么 `key` 将为负数。这时 `num` 的新值可能小于最小值（即 `ord('A')`，65）。如果是这种情况，我们希望给 `num` 加 26 以“回到”。

```
47.     translated += chr(num)
48.     else:
49.     translated += symbol
```

`translated` 字符串将附加加密/解密的字符。如果符号既不是大写字母也不是小写字母，那么第 48 行的 `else` 块将执行。`else` 块中的代码会将原始符号附加到 `translated` 字符串。这意味着空格、数字、标点符号和其他字符将不会加密（或解密）。

```
50.     return translated
```

`getTranslatedMessage()` 函数的最后一行返回 `translated` 字符串。

```
52. mode = getMode()
53. message = getMessage()
54. key = getKey()
55.
56. print 'Your translated text is:'
57. print getTranslatedMessage(mode, message, key)
```

这是程序的主体。我们依次调用定义的每个函数来获取用户使用的 mode、message 和 key。我们将这三个值作为参数传递给 `getTranslatedMessage()`，其返回值（翻译后的字符串）将打印给用户。

## 暴力破解

这就是凯撒密码。然而，虽然这种密码可能会欺骗一些不懂的人，但它无法防止密码分析专家。密码学是制造密码的科学，而密码分析是破解密码。密码学的意义在于，如果有人拿到了加密的消息，他们无法从中推出原始的未加密消息。因此我们假装成攻击者，我们只有密文。密码分析的一种方法被称为暴力破解（Brute Force）。暴力破解是尝试每一个密钥的技术。如果分析学家知道密码（或者猜到），他们遍历所有可能的密钥。因为只有 26 个可能的密钥，所以分析学家编写一个执行解密并查看输出是否有意义的程序非常容易。让我们为程序添加暴力破解功能。

首先，修改第 7、9 和 12 行（在 `getMode` 中，使其如下加粗所示）：

| 5. def getMode(): |

| 6. while True: |

| 7. print 'Do you wish to encrypt or decrypt or brute force a message?' |

| 8. mode = raw_input().lower() |

| 9. if mode in 'encrypt e d brute b'.split(): |

| 10. return mode[0] |

| 11. else: |

| 12. print 'Enter either "encrypt" or "e" or "decrypt" or "d" or "brute" or "b".' |

这允许我们选择“暴力破解”作为程序的模式。然后修改程序主体部分并添加以下更改：

| 52. mode = getMode() |

| 53. message = getMessage() |

| 54. if mode[0] != 'b': |

| 55. key = getKey() |

| 56. |

| 57. print 'Your translated text is:' |

| 58. if mode[0] != 'b': |

| 59. print getTranslatedMessage(mode, message, key) |

| 60. else: |

| 61.     for key in range(1, MAX_KEY_SIZE + 1): |

| 62.     print key, getTranslatedMessage('decrypt', message, key) |

这些更改为不在“暴力破解”模式的用户提供了强制功能。如果我们不在暴力破解模式下，将调用原始的 `getTranslatedMessage()` 并打印翻译后的字符串。

否则，我们处于暴力破解模式，运行一个 `getTranslatedMessage()` 循环，一直迭代到 `MAX_KEY_SIZE`（即 26）。记住 `range()` 函数返回一个不包含第二个参数的整数列表，这就是为什么我们有 `+1`。该程序将打印消息的所有可能的翻译（包括翻译中的密钥数字）。这里是修改后的程序示例：

14 Nby yiis qcff by bcxyxh ohyl nbu ohnec hby ziolnb gb Dofs.

15 Max whdk dkr pbee ux coadd ta zawvw fljw ngqwx max ftm mgme lzw esfl lzw xmjjlz gx Cner.

16 Lzw uvjj bgy ncco zz zravf fljw lzw esl kyyr cjyc lzw wflly fw Atgb.

17 Kvy teh auo mybb ry yuttxd kdkh ju cjlj kjydb ju vekhjw ev Zkbo.

18 Jth sdt nzn lxaa qt wqsstc jwt bpi cjixa itw udwij gu Yjan.

19 Udt sdtn lxw pwss pr vzrb lrbfs ahz hvs tcfhnv ct Xizm.

20 Gbur qbe xrl jvy or uvqgra haqre gur znzg hvs sghebu gb Whyl.

21 Ftq paqd wjk luux nn pqjaz gzpqd ftq fym gsfux ftq fagdt Ar Vgqk.

22 Lzw vzjj bgy ncco zz zravf fljw we esp gfaozo ry Tejl.

23 Dro nyby uuh frru kn qzrmmw exnob dro wkd edsix dro pyebdr ry Tevi.

24 Cgn mxha uhl gsvv qzrmmw ewna cgn vjcro oxadqx so Sduh.

25 Bpm lwmz smgt eqt jl pqlmlv qlmmz bpm uib wcjwb bpm nwczbp ry Rctg.

观察每一行后，你会发现第 8 行匹配并不是乱码，而是纯正的英语！密码分析学家可以推断出这段加密文本的原始密钥必须是 8。这种暴力破解法在凯撒和罗马帝国时代是非常困难完成的，但今天我们拥有计算机，可以快速地遍历数百万或数十亿个密钥。你甚至可以识别出它何时找到了英文消息，因此你不需要阅读所有的乱码文本。（事实上，我们将在下一本《用 Python 编写自己的电脑游戏》书中这样做！）

## 本章涵盖的内容：

- 密码学与密码
- 加密与解密
- 密文、明文、密钥和符号
- 凯撒密码
- ASCII 序数值
- `chr()` 和 `ord()` 函数
- `isalpha()` 字符串方法
- `isupper()` 和 `islower()` 字符串方法
- 密码分析
- 暴力破解技术

## 第 10 章 - 黑白（Reversi）

### 如何玩黑白

黑白（也称为奥棋）是一种在网格上玩的棋盘游戏（因此我们将使用带有 XY 坐标的笛卡尔坐标系，就像我们在 Sonar 中那样）。这是一个双玩家的游戏。我们版本的游戏将有一个计算机 AI，它比我们为井棋制作的 AI 更复杂。事实上，这个 AI 非常强大，以至于你每次玩时都可能击败你（我知道当我对它玩时会输！）

黑白有一个 8 x 8 的棋盘，棋子一面为黑，一面为白（不过我们的游戏将使用 O 和 X）。起始布局看起来如下：

| | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---|---|---|---|---|---|---|---|---|
| 1 | | | | | | | | | |
| 2 | | | | | | | | | |
| 3 | | | | | | | | | |
| 4 | | | | | ● ● | | | | |
| 5 | | | | | ● ● | | | | |
| 6 | | | | | | | | | |
| 7 | | | | | | | | | |
| 8 | | | | | | | | | |

玩家轮流放置自己的棋子。位于新棋子和另一个同色棋子之间的任何对手棋子都会被翻转。例如，假设白玩家在 5, 6 处放置一个新的白色棋子：

![](img/0ec7b2ca84b1d9fde876176e88584c95_266_0)
