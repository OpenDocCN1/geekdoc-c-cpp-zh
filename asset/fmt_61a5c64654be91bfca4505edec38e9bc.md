
第一个`print`语句将显示面板。`HANGMANPICS`是每个可能的面板的字符串列表。`HANGMANPICS[0]`显示一个空绞架，`HANGMANPICS[1]`显示头部（这在玩家猜错一个字母时发生），`HANGMANPICS[2]`显示头部和身体（这在玩家猜错两个字母时发生），以此类推，直到`HANGMANPICS[6]`显示完整的挂人且玩家输了。

`missedLetters`中的字母数量告诉我们猜了多少次。我们可以通过`len(missedLetters)`来知道这一点。如果`missedLetters`是`'a'`，那么`len('a')`将返回整数 4，这显示了`HANGMANPICS[4]`。

```python
109.     print 'Missed letters:',
110. for letter in missedLetters:
111.     print letter,
112.
```

第 110 行的`for`循环是一个新的类型。

# range 函数

`range()`函数是一个非常有用的函数，因为我们经常在循环中使用它（类似于我们已经见过的`while`循环）。

`range()`函数当带有一个参数时，会返回从 0 到不包含该参数的整数列表。尝试在 shell 中输入`range(10)`：

```python
>>> range(10)
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

使用`range()`函数很容易生成巨大的列表。但我们可以把列表保存到变量中，例如输入`span = range(10)`：

```python
>>> span = range(10)
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

如果你向`range()`传递两个参数，它返回的整数列表是从第一个参数到不包含第二个参数。尝试在 shell 中输入`range(10, 20)`：

```python
>>> range(10, 20)
[10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
```

这种循环与`while`循环非常相似，但当你只需要遍历列表中的项时，使用`for`循环需要编写的代码要少得多。你可以通过添加额外的代码，让`while`循环的作用与`for`循环相同：

使用`for`语句会自动为我们完成所有这些额外代码，并且由于我们需要编写的内容更少，使得编程变得更简单。我们的猜字游戏将使用循环，这样你就可以看到它们在实际游戏中有多实用了。

关于循环的另外一点是，`for`语句中包含一个关键字。但当你用`for in`中使用`in`关键字时，Python 并不会将其处理为你在像`42 in [0, 42, 67]`这那里使用的`in`运算符。`for`语句中的`in`关键字仅用于分隔变量和它从中获取取值的列表。

## 代码解释继续...

```python
109. print("Missed letters:")
110. for letter in missedLetters:
111.     print(letter,)
112.     print()
```

这个循环将显示玩家所做的所有错误猜测的字母。在纸上玩猜字游戏时，通常会将这些字母写在侧边，以便知道不要再次猜测。在循环的每次迭代中，`letter`的值将是`missedLetters`中的每一个字母。记住，`print`语句末尾的逗号会让它打印一个空格而不是“换行”字符，因此所有错过的字母都将位于同一行。

如果`missedLetters`是`'ajtw'`，那么这个`for`循环将显示`j t w`。

到此为止，我们已经向玩家展示了猜字板和错过的字母。现在我们想打印秘密单词，但我们希望字母处留有空白。我们可以使用`_`字符（称为下划线字符）来实现。但我们应该打印秘密单词中玩家已猜出的字母，而对未猜的字母使用`_`字符。我们可以先为秘密单词中的每个字母创建一个仅由下划线组成的字符串。然后，我们可以根据`correctLetters`中的每个字母替换空白。如果秘密单词是`'utter'`，那么空白后的字符串将是`'_____'`（五个字符）。如果`correctLetters`是字符串`'rt'`，那么我们就希望将空白字符串改为`'_tt_r_'`。这里是实现该操作的代码：

```python
114.     blanks = '_' * len(word)
115.
116.     for i in range(len(secretWord)): # 替换空白
117.         if word[i] in correctLetters:
118.             blanks = blanks[:i] + word[i] + blanks[i+1:]
```

114 使用字符串复制清除了填充下划线的`blanks`变量。记住，该运算符也可以用于字符串和整数，因此表达式`'hello' * 3`的结果为`'hellohello'`。这将使得`blanks`的下划线数量与`secretWord`的长度相同。

然后，我们使用循环遍历`secretWord`中的每个字母，如果它存在于`correctLetters`中，则将下划线替换为实际字母。第 118 行看起来很困惑。我们似乎对`blanks`和`secretWord`变量使用了方括号。但等一下，`blanks`和`secretWord`是字符串，而不是列表。`len()`函数只接受列表作为参数，但在 Python 中，许多可以在列表上执行的操作也可以在字符串上执行：

## 字符串的行为像列表一样

惊喜吧！字符串的行为就像列表一样。事实上，你可以在列表上做的一切事情你也可以在字符串上做。只需要把它们看作单字母字符串的“列表”即可。所以`'Hello'`的行为类似于`['H', 'e', 'l', 'l', 'o']`。（它们都是不同的字符串并具有不同的数据类型。）方括号也可以从字符串中挑出单个字符，就像我们从列表中挑出单个项目一样。在交互式 shell 程序中，输入`fizz = 'Hello!'`然后输入`fizz[0]`：

```python
>>> fizz = 'Hello!'
>>> fizz[0]
'H'
>>>
```

你还可以用`len()`函数找到字符串中有多少个字符。在 shell 程序中输入`len(fizz)`：

```python
>>> fizz = 'Hello world!'
>>> fizz[0]
'H'
>>> len(fizz)
12
>>>
```

然而，你不能通过`del`语句更改字符串中的字符或删除字符。这是因为列表是**可变序列**，而字符串是**不可变序列**。“可变”是“可改变”的另一个词。“不可变”意味着“不能更改”。序列是一系列连续的步骤。字符串是不可变而列表是可变的原因对我们来说并不重要。如果我们想更改字符串，可以像第 18 行那样，通过切片创建字符串的副本。

## 列表切片与子字符串

**切片**就像使用多个索引而不是仅仅一个索引进行索引。我们不是在方括号之间放入一个索引，而是放入两个用冒号分隔的索引。为了从我们的列表`animals[0:3]`获取前三个项，这表示获取从 0 到（不包含）3 的项。

```python
>>> animals = ['dog', 'cat', 'bird', 'fish']
>>> animals[0:3]
['dog', 'cat', 'bird']
```

获取`animals`中的第 2 和 3 项使用`animals[2:4]`。

```python
>>> animals = ['dog', 'cat', 'bird', 'fish']
>>> animals[2:4]
['bird', 'fish']
```

尝试在 shell 程序中输入`animals[2]`：

```python
>>> animals = ['dog', 'cat', 'bird', 'fish']
>>> animals[2]
'bird'
```

切片也可以提取字符串的一部分（即子字符串）。

```python
>>> s = 'Hello world'
>>> s[0:5]
'Hello'
>>> s[6:]
'world'
>>> s[-5:]
'world'
```

切片还可以通过步长来提取项。

```python
>>> s = 'Hello world'
>>> s[::2]
'Hloolrd'
>>> s[1::2]
'el wr'
```

切片还可以用于反转序列。

```python
>>> s = 'Hello world'
>>> s[::-1]
'dlrow olleH'
```

接几行代码将显示字母之间带有空格的`blanks`的新值。

```python
120. for letter in blanks: # 显示字母之间带有空格的秘密单词
121.     print letter,
122. print
```

这个`for`循环将打印字符串`blanks`中的每个字符。请记住，到此时为止，`blanks`中的某些下划线可能已经被替换为`secretWord`中的字母。`print`语句末尾的逗号会导致它显示一个空格而不是换行符。

这是`displayBoard()`函数的结束。

```python
124. def getGuess(alreadyGuessed):
125.     # 返回玩家输入的字母。此函数确保玩家输入的是单个字母，而不是其他内容。
```

`getGuess()`函数有一个名为`alreadyGuessed`的字符串参数，其中包含了玩家已经猜过的字母，并要求玩家猜一个字母。这个单字母将作为该函数的返回值。

```python
126. while True:
127.     print 'Guess a letter.'
128.     guess = raw_input()
129.     guess = guess.lower()
```

我们将使用`while`循环，因为我们想一直询问玩家一个字母，直到他们输入一个之前没有猜过的单个字母。注意，`while`循环的条件简单就是布尔值`True`。这意味着执行离开此循环的唯一方法是执行`break`语句（退出循环）或执行`return`语句（退出整个函数）。

循环内部的代码要求玩家输入一个字母，该字母被存储在变量`guess`中。如果玩家输入的是大写字母，它将在第 129 行被转换为小写。

## elif ("否则，如果") 语句

请看以下代码：

```python
if catName == 'Fuzzball':
    print 'Your cat is fuzzy.'
else:
    print 'Your cat is not very fuzzy at all.'
```

我们以前见过这种写法，它相当简单。如果变量`catName`等于字符串`'Fuzzball'`，那么语句的条件就为`True`，我们告诉用户她的猫是毛茸茸的。如果`catName`是其他任何，我们就告诉用户她的猫并不毛茸茸。

但如果我们想要除了“毛茸茸”和“不毛茸茸”之外的其他内容，我们可以在第一个`else`块内部放入另一个`if else`语句，如下：

```python
if catName == 'Fuzzball':
    print 'Your cat is fuzzy.'
else:
    if catName == 'Spots':
        print 'Your cat is spotted.'
    else:
        print 'Your cat is neither fuzzy nor spotted.'
```

但如果我们想要更多，代码就会有很多缩进：

```python
if catName == 'Fuzzball':
    print 'Your cat is fuzzy.'
else:
    if catName == 'Spots':
        print 'Your cat is spotted.'
    else:
        if catName == 'FattyKitty':
            print 'Your cat is fat.'
        else:
            if catName == 'Puff':
                print 'Your cat is puffy.'
            else:
                print 'Your cat is neither fuzzy nor spotted nor fat nor puffy.'
```

输入所有这些空格意味着你有更多机会在缩进上出错。Python 有一个`elif`关键字。使用`elif`，上面的代码看起来如下：

```python
if catName == 'Fuzzball':
    print 'Your cat is fuzzy.'
elif catName == 'Spots':
    print 'Your cat is spotted.'
elif catName == 'FattyKitty':
    print 'Your cat is fat.'
elif catName == 'Puff':
    print 'Your cat is puffy.'
else:
    print 'Your cat is neither fuzzy nor spotted nor fat nor puffy'
```

如果`if`语句的条件为`False`，程序将检查第一个`elif`语句的条件（即`catName == 'Spots'`）。如果该条件为`False`，程序将检查下一个`elif`语句的条件。如果`if`和`elif`语句的**所有**条件都为`False`，则执行`else`块中的代码。

但如果其中一个`elif`条件为`True`，则执行`elif`块，然后执行跳转到`else`块之后的第一行。因此，这个`if-else`语句中只有一个块会被执行。你也可以在不需要时省去`else`块，只保留`if-elif`语句。

## 代码解释继续...

```python
130.    if len(guess) != 1:
131.        print 'Please enter a single letter.'
132.    elif guess in alreadyGuessed:
133.        print 'You have already guessed that letter. Choose again.'
134.    elif guess not in 'abcdefuvwxyz':
135.        print 'Please enter a single letter.'
136.    else:
137.        return
```

循环内部的代码要求玩家输入一个字母，该字母被存储在变量`guess`中。如果玩家输入的是一个字母，它会在第 132 行。如果是如此，我们应该跳回并再次询问玩家。如果该语句的条件为`True`，则执行`elif`块，然后执行跳转到`else`块之后的第一行。由于`else`块之后没有更多代码，执行将回到 126。如果`if`语句的条件为`False`，程序将检查第一个`elif`语句的条件（即`guess in alreadyGuessed`）。如果该条件为`False`，程序将检查下一个`elif`语句的条件。如果`if`和`elif`语句的**所有**条件都为`False`，则执行`else`块中的代码。

但如果其中一个`elif`条件为`True`，则执行`elif`块，然后执行跳转到`else`块之后的第一行。由于`else`块之后没有更多代码，执行将回到 126。`guess`变量包含了玩家输入的字母。如果玩家输入的是大写字母，它会在第 129 行被转换为小写（抱歉，此处我发现原文文本的逻辑似乎有些错乱，我将根据上下文逻辑重新对齐翻译）。

*纠正：*接几行代码将显示字母之间带有空格的`blanks`的新值。

```python
120. for letter in blanks: # 显示字母之间带有空格的秘密单词
121.     print letter,
122. print
```

这个`for`循环将打印字符串`blanks`中的每个字符。请记住，到此时，`blanks`中的某些下划线可能已经被替换为`secretWord`中的字母。`print`语句末尾的逗号会导致它显示一个空格而不是换行符。

这是`displayBoard()`函数的结束。

```python
124. def getGuess(alreadyGuessed):
125.     # 返回玩家输入的字母。此函数确保玩家输入的是单个字母，而不是其他内容。
```

`getGuess()`函数有一个名为`alreadyGuessed`的字符串参数，其中包含了玩家已经猜过的字母，并要求玩家猜一个字母。这个单字母将作为该函数的返回值。

```python
126. while True:
127.     print 'Guess a letter.'
128.     guess = raw_input()
129.     guess = guess.lower()
```

我们将使用`while`循环，因为我们想一直询问玩家一个字母，直到他们输入一个之前没有猜过的单个字母。注意，`while`循环的条件简单就是布尔值`True`。这意味着执行离开此循环的唯一方法是执行`break`语句（退出循环）或执行`return`语句（退出整个函数）。

循环内部的代码要求玩家输入一个字母，该字母被存储在变量`guess`中。如果玩家输入的是大写字母，它将在第 129 行被转换为小写。
