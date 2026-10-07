
让我们从将背景图像创建为标签开始。我们可以使用 Tkinter 中的 `ImageTk()` 函数来实现。我们现在可以先将其留空，因为我们将在函数中更新它。然后，我们用图像对象创建一个 `Label`。请将以下代码放在构建 Tkinter 应用程序代码中“canvas”和“frame”部分之间。

```python
background_image = tk.PhotoImage()
background_label = tk.Label(root, image=background_image)
background_label.place(relwidth=1, relheight=1)
```

我们需要挑选一些图像来表示我们感兴趣的各种天气状态（在本演示中，我们只使用三种：雨天、雪天、晴天）。你可以去 Pixabay 等免费图片网站搜索符合这些标准的图片，并使用你喜欢的任何图片。将它们保存为 `.jpg` 格式，并保存到与你的应用程序相同的文件夹中。现在，我们需要创建一个函数，检查天气描述中是否包含某些字符串。如果找到了这些字符串，我们将背景图像更新为与描述匹配的图像。

让我们从该函数开始，检查描述中是否存在某些字符串，如果找到了该字符串，则将其赋值给变量。函数将查找描述中是否存在“rain（雨）”或“snow（雪）”，否则将选择一张晴天的图像。

```python
def get_image_type(description):
    if "rain" in description:
        image_type = "rain.jpg"
    elif "snow" in description:
        image_type = "snow.jpg"
    else:
        image_type = "sunny.jpg"
    return image_type
```

回到我们的 `get_data` 函数，我们应该创建一个 `image_type` 变量来存储我们函数的返回值。在此同时，让我们也选择一个默认图像并将其设置为 `image_type` 的默认值。这样，总有一个默认图像可以回退，而不会发生错误。请选择另一张你想要作为默认图像的图片。我们将如下所示在 `get_data` 函数顶部创建 `image_type` 变量：

```python
image_type = "default.jpg"
```

现在我们必须调用 `get_image_type` 函数。我们想要获取天气数据 JSON 的描述，我们将其保存为名为 `desc` 的变量。我们需要将其放在 `try` 关键字下，以便函数可以访问 `desc` 变量。在 `try` 条件下的 `full_string` 变量正下方放置以下行代码：

```python
image_type = get_image_type(desc)
```

现在我们已经指定了 `image_type` 并允许它根据我们接收到的天气数据发生变化，我们需要做的只是更新 `background_label` 变量。我们将在 `get_data` 函数中执行此操作，这样在点击“天气如何？”按钮时就会更新。我们可以通过创建一个新的图像对象来更新图像，这最简单的方法是使用 PIL 中的 `Image.open()` 和 `ImageTk.PhotoImage()` 函数。`ImageTk` 是 PIL 内置的一个特殊模块，专为与 Tkinter 配合而设计。首先，让我们导入需要的模块。

```python
from PIL import ImageTk, Image
```

现在我们只需要创建一个新的图像对象，并将 `image_type` 作为其参数。然后我们在 `background_label` 上使用 `.configure()` 函数，并告诉函数我们要配置标签接受新图像。最后，通过将标签的 `image` 属性设置为新图像来更新标签。

```python
new_image = ImageTk.PhotoImage(Image.open(image_type))
background_label.configure(image=new_image)
background_label.image = new_image
```

现在我们的 `get_data` 函数看起来应该是这样的：

```python
def get_data(city):
    api_key = "YOUR API KEY HERE"
    url = "https://api.openweathermap.org/data/2.5/weather/"
    arguments = {"APPID": api_key, "q": city, "units": "imperial"}
    data = requests.get(url, params=arguments).json()
    image_type = 'default.jpg'

    try:
        name = data['name']
        desc = data['weather'][0]['description']
        temp = data['main']['temp']
        wind = data['wind']['speed']
        feels_like = data['main']['feels_like']
        full_string = 'Location: {} \n Conditions: {} \n' 'Temperature \n(F): {} \n' 'Wind (MPH): {} \n' 'Feels Like (F): {}.'.format(desc, temp, wind, feels_like)
        image_type = get_image_type(desc)
    except:
        full_string = "No matching location found. \n Please check location and try again."

    label['text'] = full_string
    new_image = ImageTk.PhotoImage(Image.open(image_type))
    background_label.configure(image=new_image)
    background_label.image = new_image
```

现在我们的应用程序更好看了。

- Awasthi, A. (2018, 6月28日). Python 中的递归思考. 检索于2019年12月，来自 https://realpython.com/python-thinking-recursively。
- GeeksForGeeks, Python 中的 max() 和 min()。 (2019,11月29日). 检索于2019年12月，来自 https://www.geeksforgeeks.org/max-min-python/
- Schafer, C. (2019,9月). Python 多线程教程：使用 Threading 模块并发运行代码. 检索于2019年12月，来自 https://www.youtube.com/v=IEEhzQoKtQU。
- Rodriguez, I. (2019,4月4日). 什么是 Pip？针对 Python 新手的者的指南. 检索于2019年12月，来自 https://realpython.com/what-is-pip/
- Pipenv 与虚拟环境 - Python 旅行者指南. (无日期). 检索于2019年12月，来自 https://docs.python-guide.org/dev/virtualenvs/
- Pillow, 教程. (无日期). 检索于2019年12月，来自 https://pillow.readthedocs.io/en/3.0/handler/tutorial.html。
- Schafer, C. (2017,10月). Python 教程：re 模块 - 如何编写和匹配正则表达式 (Regex). 检索于2019年12月，来自 https://www.youtube.com/watch?v=K8L6KVGG-7o。
- SQLite Python：创建新数据库. (无日期). 检索于2020年1月，来自 https://www.sqlutorial.net/sqlite-python/creating-database/。
- Lofaro, L. (2019,4月19日). 在 Python 中处理 JSON 数据. 检索于2020年1月6日，来自 https://realpythonpython.com/python-json/
- Kinsley, H. (2014,7月18日). Python 3 编程教程 - Sys 模块. 检索于2020年1月6日，来自 https://www.youtube.com/watch?v=rLG7Tz6db0w
- Chitipothu, A. (2019). 5. 迭代器与生成器. 检索于2020年1月6日，来自 https://anandology.com/python-practice-book/iterators.html
- Weber, B. (2019,6月18日). 在 Python 中定义主函数. 检索于2020年1月6日，来自 https://realpythonpython.com/python-main-function/。
- Pryke, B. (2019,9月11日). 初学者 Jupyter Notebook 教程. 检索于2020年1月8日，来自 https://www.dataquest.io/blog/jupyter-notebook-tutorial/
- Schafer, C. (2017,8月16日). Python 教程：使用 unittest 模块对代码进行单元测试. 检索于2020年1月8日，来自 https://www.youtube.com/watch?v=6tNS--WetLI
- Galli, K. (2019,2月1日). Ad in 5 53:38 / 1:05:13 如何编写 GUI 应用（使用 Python Tkinter）. 检索于2020年1月14日，来自 https://www.youtube.com/watch?v=D8-snVfekto
- Sharma, A. (2019,12月10日). (教程) 使用 PYTHON 中的 TKINTER 介绍 GUI. 检索于2020年1月12日，来自 https://www.datacamp.com/community/tutorials/gui-tkinter-python

# 快速学习 JavaScript

# 第1章：什么是编程？

## 引言

你曾经为你的电脑写过程序吗？如果你写过，那么你有一个良好的开始。你可能想快速浏览这一章，但如果你愿意，也可以直接跳到下一章。

简单来说，程序是一组告诉计算机做什么的指令。这听起来足够简单，对吧？你想让计算机发送电子邮件、画一个圆或打开烤箱。遗憾的是，计算机，即使是你手机里那个超级强大的芯片，也不理解这些指令。你必须将它们分解为非常简单的步骤。

## 算法

计算机需要执行的步骤以算法的形式表示。这只是对步骤进行详细描述的华丽词汇。假设你想写一个制作咖啡杯咖啡的算法。这可能看起来很傻，因为它非常简单。你所做的就是：

- 制作咖啡

但要制作咖啡（使用常见的家用机器），你实际上需要：

- 拿出咖啡豆
- 打开罐头
- 向机器里加水
- 向机器里加入咖啡
- 开启机器
- 等待完成
- 拿一个杯子
- 倒入杯子中
- 加入奶奶油和糖

这变得复杂了！我们要加多少水？加多少咖啡？在最低层面，为了让程序易于理解，计算机需要所有这些细节以及更多。计算机程序中最基本的步骤可能像某些示例：

- 将水加载到寄存器 1
- 将内存复制到寄存器 2
- 从寄存器 1 中减去寄存器 2
- 如果结果小于零，跳转

这些步骤中的每一步都可能由单个机器指令表示。存储在内存中时，这些指令以原始语言表示，以便计算机理解。一个典型的机器指令可能像这样：

```
LDI R1
LD R2
SUB R2
BLZ 4
```

这世界到底是什么意思？坦率说，除非你是计算机架构师，否则你不需要知道。

## 编程语言

早期程序员必须以机器指令的形式来编写程序。随着程序变得越来越大、越来越复杂，这种方法变得几乎是不可能的。新的语言尝试用一种程序员和计算机都能于理解的格式来表达算法。然而，程序员仍然需要学习很多才能编写出这样的程序。许多其他语言出现了，它们被称为汇编语言。

第一个广泛使用的编程语言是 FORTRAN，全称是公式翻译。这种语言由 IBM 开发，用于执行数值计算。这里是一个测试数字是偶还是老的简短 FORTRAN 程序：

```
INTEGER INUM,IREM
50 READ (5) INUM
IREM = INUM/2)*2
IF (IREM.EQ(0) GO TO 200
100 WRITE (6,101) INUM
101 FORMAT(5,7H IS ODD)
200 WRITE (6,201) INUM
300 STOP
```

如果你觉得这看起来复杂且难以理解，你是正确的。但它比直接编写机器指令要好得多。此外，用 FORTRAN 编写的程序可以在许多类型的计算机上运行。我们将很快看到如何。

在 FORTRAN 之后出现了许多其他语言。其中最著名的包括 COBOL、Pascal 和 C。C 语言被证明特别重要，因为它是为 Unix 操作系统（以及后的 Linux）设计的。它还成为了重要的现代语言 C++、Java 和 JavaScript 的灵感。

这是一个用 C 语言编写的程序，与上面的 FORTRAN 程序相同：

```c
#include <stdio.h>
int main() {
    int value;
    printf("Enter a value: ");
    scanf("%d", &value);
    if (value % 2 == 0){
        printf("%d is even\n", value);
    } else {
        printf("%d is odd\n", value);
    }
}
```

已经开发了上千种编程语言，目前有几十种正在广泛使用。为什么不使用自然语言，比如英语呢？写出这样的内容会很好：

- 1. 询问一个数字
- 2. 读取数字
- 3. 将数字除以 2
- 4. 如果有余数，打印“奇数”
- 5. 否则，打印“偶数”

遗憾的是，这对于计算机理解来说已经太复杂了。此外，这种自然语言中的语句可能会产生歧义。考虑这个简单的句子：

> 男人拿着望远镜看到了男孩。

这看起来意义明确，直到你稍加思考一下。谁手里拿着望远镜，是男人还是男孩？也许男人正在通过望远镜观察，也许男孩正提着它。句子没有说明这一点。人类会自动考虑句子的上下文：其他句子说什么？但对计算机来说这并不容易。编程语言的设计是为了避免（或减少）此类问题。

# 语言翻译

用编程语言编写的程序无法被计算机直接理解。相反，我们需要一个翻译程序来读取原始程序，并生成一个计算机可以理解的版本。由于我们增加了一个翻译步骤，因此可以将同一个程序翻译成并运行在不同的计算机上，而对程序本身几乎没有或完全改动。

编程语言的传统翻译程序被称为编译器（compiler）。在最简单的形式下，编译器读取用编程语言编写的程序（通常来自文件），然后以计算机能理解的形式输出程序。原始程序称为源程序，编译器的输出称为可执行程序。可执行程序存储在文件中，直到需要为止。此时，它可以被加载到内存中并运行或执行。

在实践中，编译器通常会将程序翻译成一种中间形式（有时称为目标程序），然后由另一个翻译器进行处理以生成可执行文件。这提供了许多用处，包括将你的程序与操作系统可能提供的其他程序和库结合的能力。

在实践中，程序员通常使用集成开发环境（IDE）来开发程序。IDE 会自动处理许多翻译步骤，因此你可能甚至不知道正在发生什么。你将在下一章学习 JavaScript 中的 IDE。

多年来开发的大多数语言都是为了编译而设计的。这包括 FORTRAN、Pascal、C、C++、Java 以及数百其他语言。

对于最近语言，，不同的翻译过程变得流行。这种过程使用解释器（interpreter）而不是编译器。解释器每次读取一部分源程序并立即执行该部分。它没有独立的中间程序或可执行程序。这种语言的设计必须确保每个小部分都能被立即执行，而无需等待查看整个程序的内容。这种语言有时被称为脚本语言（scripting language）。

最近流行的一种脚本语言是 Python。另一个例子是 JavaScript，这也是我们本书关注的语言。

为了测试一个数字是偶数还是奇数，JavaScript 程序看起来是什么样的？这里有一种可能的方法：

```
var value = prompt("Enter a value: ");
if (value % 2 == 0) {
```

```
document.write(value + " is even\n");
} else {
document.write(value + " is odd\n");
}
```

如你所见，这与 C 程序非常相似，但实际上有一些非常重要的区别。现在你已经对编程本质有了了解，让我们进入下一章，认识 JavaScript 本身吧。

## 第 2 章：什么是 JavaScript？

到目前，你已经对编程是什么有了了解，你可能已经用另一种编程语言编写过程序。计算机程序已经用数百种不同的语言编写。这些语言中的大多数设计用于编写直接在你的计算机（或移动设备）上运行的程序，执行诸如写信、制作视频、计算税费或控制恒温器等任务。

JavaScript 的出现出于不同的需求，与其他大多数编程语言相比有一些重要的区别。让我们来看看 JavaScript 到底是什么。

## 背景
