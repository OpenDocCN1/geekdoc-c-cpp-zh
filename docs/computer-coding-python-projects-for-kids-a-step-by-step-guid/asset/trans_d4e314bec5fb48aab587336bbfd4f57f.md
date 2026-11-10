
### 17 获取事件

现在你已经编写了所有函数，可以使用它们来编写程序的主体部分。将下面两行代码放到文件底部。第一行调用（运行）get_events() 函数，并将日历事件列表存储到名为 events 的变量中。第二行使用 datetime 模块获取今天的日期，并将其存储到名为 today 的变量中。

```python
c.create_text(100, 50, anchor='w', fill='orange', \
              font='Arial 28 bold underline', text='My Countdown Calendar')

events = get_events()
today = date.today()
```

如果要将一行长代码拆分成两行，请使用反斜杠字符。

![](img/1bd24ab186f69fb18194b4174ca15178_116_0.png)

别忘了保存你的工作。

### 18 显示结果

接下来计算距离每个事件还有多少天，并将结果显示在屏幕上。你需要对列表中的每个事件都执行此操作，因此使用 for 循环。对于列表中的每个事件，调用 days_between_dates() 函数，并将结果存储到名为 days_until 的变量中。然后使用 tkinter 的 create_text() 函数在屏幕上显示结果。将这段代码紧接在步骤 17 的代码之后。

哇！我在班里得了第一名！

![](img/1bd24ab186f69fb18194b4174ca15178_116_1.png)

这段代码会针对事件列表中存储的每个事件运行。

获取事件的名称。

使用 days_between_dates() 函数计算事件与今天日期之间的天数。

```python
for event in events:
    event_name = event[0]
    days_until = days_between_dates(event[1], today)
    display = 'It is %s days until %s' % (days_until, event_name)
    c.create_text(100, 100, anchor='w', fill='lightblue', \
                  font='Arial 28 bold', text=display)
```

创建一个字符串，用来保存我们想要显示在屏幕上的内容。

这个字符使代码跨到两行。

在屏幕上的位置 (100, 100) 处显示文本。

### 19 测试程序

现在尝试运行代码。看起来所有文本行都叠在一起了。你能找出哪里出错了吗？你会如何解决？

![](img/1bd24ab186f69fb18194b4174ca15178_116_2.png)

### 排序！

你可以调整代码，让事件按照它们将要发生的顺序排序。在 for 循环之前添加下面这行代码。它使用 sort() 函数按升序排列事件，从剩余天数最少到最多。

```python
    vertical_space = 100
    events.sort(key=lambda x: x[1])
    for event in events:
```

按剩余天数排序，而不是按事件名称排序。

选择你最喜欢的颜色。

![](img/1bd24ab186f69fb18194b4174ca15178_118_0.png)

### 重新设置文本样式

通过更改标题文本的大小、颜色和样式，让你的用户界面焕然一新。

```python
    c.create_text(100, 50, anchor='w', fill='pink', font='Courier 36 bold underline', \
          text='Sanjay\'s Diary Dates')
```

如果你愿意，也可以更改标题。

试试其他字体，例如 Courier。

### 设置提醒

高亮显示即将发生的事件可能会很有用。修改你的代码，让接下来一周内发生的任何事件都以红色显示。

伙计们，你们10分钟后上场！

![](img/1bd24ab186f69fb18194b4174ca15178_118_1.png)

```python
    for event in events:
        event_name = event[0]
        days_until = days_between_dates(event[1], today)
        display = 'It is %s days until %s' % (days_until, event_name)
        if (int(days_until) <= 7):
            text_col = 'red'
        else:
            text_col = 'lightblue'
        c.create_text(100, vertical_space, anchor='w', fill=text_col, \
                      font='Arial 28 bold', text=display)
```

符号 <= 表示“小于或等于”。

使用正确的颜色显示文本。

int() 函数将字符串转换为数字。例如，它将字符串 '5' 转换为数字 5。

## 请教专家

你能说出世界上所有首都的名称吗？或者你最喜欢的运动队中的所有球员？每个人都是某个领域的专家。在这个项目中，你将编写一个程序，它不仅能回答你的问题，还能学习新知识并成为专家。

![](img/1bd24ab186f69fb18194b4174ca15178_119_0.png)

![](img/1bd24ab186f69fb18194b4174ca15178_119_1.png)

### 会发生什么

一个输入框会要求你输入一个国家的名称。当你输入答案后，程序会告诉你它的首都。如果程序不知道，它会要求你教它正确答案。使用这个程序的人越多，它就越聪明！

![](img/1bd24ab186f69fb18194b4174ca15178_119_2.png)

![](img/1bd24ab186f69fb18194b4174ca15178_119_3.png)

![](img/1bd24ab186f69fb18194b4174ca15178_119_4.png)

![](img/1bd24ab186f69fb18194b4174ca15178_119_5.png)

![](img/1bd24ab186f69fb18194b4174ca15178_119_6.png)

输入一个国家的名称

如果程序不知道答案，它会问你。

### 4. 导入 Tkinter 工具

要制作这个程序，你需要 Tkinter 模块中的一些小部件。在程序顶部输入下面这一行。

```python
from tkinter import Tk, simpledialog, messagebox
```

从 Tkinter 模块加载这两个小部件。

### 5. 启动 Tkinter

接下来添加以下代码，在 shell 中显示项目标题。Tkinter 会自动创建一个空窗口。这个项目不需要它，所以用一行巧妙的代码把它隐藏起来。

```python
print('Ask the Expert - Capital Cities of the World')
root = Tk()
root.withdraw()
```

隐藏 Tkinter 窗口。

创建一个空的 Tkinter 窗口。

![](img/1bd24ab186f69fb18194b4174ca15178_122_0.png)

### 6. 测试代码

尝试运行你的代码。你应该会在 shell 中看到项目名称。

![](img/1bd24ab186f69fb18194b4174ca15178_122_1.png)

测试中！测试中！

### 7. 设置字典

现在，在步骤 5 编写的代码之后输入下面这行代码。新代码会设置一个字典，用来存储国家名称及其首都。

```python
the_world = {}
```

这会创建一个名为 the_world 的空字典。

使用花括号。

![](img/1bd24ab186f69fb18194b4174ca15178_122_2.png)

我会把所有信息都存储在这里。

### 专家提示

### 使用字典

字典是 Python 中存储信息的另一种方式。它类似于列表，但每个项都有两部分：键和值。你可以在 shell 窗口中输入以下内容来测试它。

```python
favourite_foods = {'Simon': 'pizza', 'Jill': 'pancakes', 'Roger': 'custard'}
```

键后面紧接着使用冒号。这是键。这是值。字典中的每个项用逗号分隔。字典使用花括号。

- 1. 要显示字典的内容，你必须打印它。试着打印 `favourite_foods`。

```python
print(favourite_foods)
```

在 shell 中输入这段内容并按回车/换行。

- 2. 现在向字典中添加一个新项：Julie 和她最喜欢的食物。她喜欢饼干。

```python
favourite_foods['Julie'] = 'biscuits'
```

键

值

- 3. Jill 改变了主意——她现在最喜欢的食物是墨西哥卷饼。你可以在字典中更新这条信息。

```python
favourite_foods['Jill'] = 'tacos'
```

更新后的值

- 4. 最后，你可以通过使用 Roger 的名字作为键，在字典中查找他最喜欢的食物。

```python
print(favourite_foods['Roger'])
```

使用键来查找值。

### 函数时间到！

项目的下一阶段涉及创建程序中需要使用的函数。

![](img/1bd24ab186f69fb18194b4174ca15178_123_0.png)

### 8. 文件输入

你需要一个函数来读取文本文件中存储的所有信息。它将类似于你在“倒计时日历”中用来从事件文件读取数据的函数。将这段代码添加到 Tkinter 导入行之后。

```python
from tkinter import Tk, simpledialog, messagebox

def read_from_file():
    with open('capital_data.txt') as file:
```

这一行会打开文本文件。
