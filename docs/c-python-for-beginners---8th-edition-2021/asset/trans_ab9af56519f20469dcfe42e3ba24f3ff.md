

# 为什么选择 Python？

操作系统如 Windows、macOS 和 Linux，通常是 C++、C# 以及某些形式的可视化语言组合。游戏通常使用 C++ 并配合内存管理，而它是如 HTML、Java、Python 等可用语言的开发平台之一。

Python 诞生于二十多年前，现已发展成为学习计算机编程的理想初学者语言。对于爱好者、学生、教师，以及那些只需要在自己或外部硬件与电脑之间创建简单交互的人来说，它都是完美的。

更通用的编程被用于创建程序、应用程序、软件或无论他们如何称呼这些东西。它们被广泛应用于所有平台和几乎每一个可以想象的应用程序。某些语言比其他语言更快，某些比其他语言更容易学习。Python 就是这样一种通用型语言。

Python 免费下载和安装，并适用于 Linux、Windows、macOS、MS-DOS、OS2、IBM 系列机器。它被选为世界前五语言之一，并不断走在硬件和互联网的发展曲线前沿。

Python 被称为“高级语言”，因为它通过你的变量、对象、属性、子程序、循环和无数次交互与硬件及操作系统进行“对话”。它不像低级语言那样精简（低级语言可以直接与内存地址、调用和寄存器交互），但它是随处可访问且易于的。

所以回答这个问题：为什么选择 Python？简单来说，它是免费的、易学的、极其强大的、全球通用的，并且是一项卓越的学习和教育工具。

```java
// Import Java
import java.lang.reflect.*;
class Invoke {
    public static void main(String[] args) {
        try {
            Class c = Class.forName(args[0]);
            Method m = c.getMethod(args[1], new Class[]);
            Object ret = m.invoke(null, null);
            System.out.println("Invoked static method " + args[1] + " with no arguments results: " + ret);
        } catch (ClassNotFoundException e) {
            System.out.println("Class not found: " + args[0]);
        } catch (NoSuchMethodException e) {
            System.out.println("Method not found: " + args[1]);
        } catch (IllegalAccessException e) {
            System.out.println("You don't have permission to invoke that method");
        } catch (Exception e) {
            System.out.println("An exception occurred while invoking that method");
        }
        System.out.println("Method error: " + e.getMessage());
    }
}
```

```basic
50 LET py=15
60 FOR y=1 TO 10
70 LET BY=Y=Y+(RND*28)
80 LET bx=0
90 FOR d=1 TO 20
100 PRINT bx,py,"U"
110 PRINT bx,py,"V"
120 LET py=py-5
130 IF py<0 THEN LET py=30
140 FOR n=1 TO 10: NEXT n
150 IF py=27 THEN LET py=27
160 bx=bx+2
170 PRINT AT, 5,py,"B"
180 LET s=s+1
190 PRINT AT, 10,"score:",s
200 FOR v=1 TO 1000: NEXT v
210 NEXT
```

BASIC 是一种早期 8 位计算机用户开始学习的、非常简单的语言。

Java 是一种强大的语言，用于网页、机顶设备、电视甚至外壳。

![](img/588364e02a77f179099fae91a1713f0a_8_0.png)

```python
def play_game():
    attempts = 0
    while (guess = input("Enter a letter: ")) != "quote":
        attempts += 1
        if not guess.isalpha():
            print("Invalid, try again.")
            continue
        if guess not in alphabet:
            print("The letter is not in the alphabet. Try again.")
            continue
        if guess in secret_letters:
            print("Correct!")
            secret_letters.remove(guess)
            if len(secret_letters) == 0:
                print("You have found all letters. Congratulations!")
                break
        else:
            print("Already found that letter. Try again.")
    print(f"You failed in {attempts} attempts.")
```

Python 是一种基于 BASIC 的现代语言，它易于学习，是理想的初学者语言。

# 向 Python 问好

## 你需要的设备
你只需要很少的硬件或初始投入就可以学习 Python。你不需要极其强大的计算机，而且任何需要的软件都是免费提供的。坦率地说，Python 是一种多平台语言，适用于 Windows、macOS、Linux、树莓派等更多平台。如果你拥有其中一种系统，就可以轻松地开始使用 Python。

![](img/588364e02a77f179099fae91a1713f0a_9_0.png)

## 电脑
显然，你需要一台电脑来学习如何 Python 编程并测试你的代码。你可以使用 32 位或 64 位处理器的 Windows（从 XP 及以后版本）、Apple Mac 或 Linux。

## IDE
IDE（集成开发环境）被用于输入和执行 Python 代码。它允许你检查程序中的值，并提供高级功能。有许多不同的 IDE，找到适合你并能产生良好结果的那一个。

![](img/588364e02a77f179099fae91a1713f0a_9_1.png)

## Python 软件
macOS 和 Linux 已经预装了 Python，树莓派也是如此。然而，你需要确保运行的是最新版本的 Python。Windows 需要下载并安装 Python。

![](img/588364e02a77f179099fae91a1713f0a_9_2.png)

## 文本编辑器
虽然文本编辑器是输入的理想环境，但并非必须。你可以直接从 IDLE 输入并执行代码，但 Sublime Text 或 Notepad++ 等文本编辑器提供了更高级的功能和代码高亮。

## 网络访问
Python 是一个不断进的环境，新版本经常引入新概念或更改现有代码使其更高效。访问互联网可以在你遇到困难时帮助你，并让你接触到 Python 海量的模块。

## 时间与耐心
其他书籍可能会让你认为 24 小时内就能成为程序员。学习 Python 代码需要时间和耐心。你可能会遇到困难，但那时代码会像水一样流淌。理解你在学习全新的东西，你就能到达。

# 树莓派
为什么使用树莓派？树莓派是一种非常便宜的小型计算机，为用户提供了极佳的学习平台。它的主操作系统 Raspbian 预装了带有许多模块的最新 Python。

# Raspbian
树莓派 3 是最新版本，包含了更强大的 CPU、内存、Wi-Fi 和蓝牙支持。你可以根据感兴趣的套装以 32 英元购买 Pi，或者购买 50 英元以上的套装。

![](img/588364e02a77f179099fae91a1713f0a_10_0.png)

## FUZE 项目
FUZE 是建立在最新型号树莓派上的学习环境。你可以购买带有电子套件甚至机器人手臂的构建和项目。你可以在 fuze.co.uk 更多信息。

# Raspbian
树莓派的主操作系统是一个基于 Debian 的 Linux 发行版，包含了你所需的所有简单易用包。它为 Pi 进行了优化，是硬件软件项目、编程甚至作为桌面电脑的理想平台。

![](img/588364e02a77f179099fae91a1713f0a_10_1.png)

## 书籍
我们在 bdmpublications.com 有许多优秀的编程书籍。我们的 Pi 书涵盖了如何购买你的第一台树莓派、设置和使用它；还有一些很好的项目示例和指南让你从树莓派中获得最大收益。

![](img/588364e02a77f179099fae91a1713f0a_10_2.png)

![](img/588364e02a77f179099fae91a1713f0a_10_3.png)

# 认识 Python

## 了解 Python
Python 是创造以来最强大的计算机编程语言。它让你以一种简洁且易于理解的语言充分利用计算机的力量。

## 什么是编程？
在尝试学习编程语言之前，了解什么是编程语言是有帮助的，让我们看看 Python 是如何产生的以及它与其他语言的关系。

![](img/588364e02a77f179099fae91a1713f0a_11_0.png)

# 编程食谱
程序就像计算机的食谱。

- 在碗里放入 100 克泡松粉。
- 在碗里加入 100 克奶油。
- 加入 100 毫升牛奶。
- 烘烤半小时。

编程语言是计算机遵循的指令列表。这些指令可以简单到保存或播放文件，也可以复杂到构建一个世界。Python 在 20 世纪 80 年代后期由 Guido Rossum 在荷兰 Centrum Wiskunde 想出，作为 ABC 语言的继承者。

> Guido Rossum，Python 之父。

就像食谱一样，程序由你顺序遵循的指令组成。程序描述了蛋糕运行可能像什么：

```python
cake = []
flour = 100
butter = 50
milk = 100
cake.append([flour,butter,milk])
cake.cake()
```

# 程序命令
你可能不理解某些 Python 命令，例如 `append` 和 `cake.cake(bowl)`。第一个列表是第二个；我们将在书中查看两者。主要知道的一点是，Python 中读取命令是很容易的。当你学习了命令时，很容易弄清楚程序是如何工作的。

```python
def cake(self):
    for ingredient in self:
        print(ingredient)
```

```python
cake = []
flour = 100
butter = 50
milk = 100
cake.append([flour,butter,milk])
```

