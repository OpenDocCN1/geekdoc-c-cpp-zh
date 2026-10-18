

正如你所看到的，除非我们知道公式，否则每一个连续的值看起来都是随机的。这就是它们被称为伪随机数的原因。这个特定的函数并不是一个很好的伪随机数生成器，因为它很快就会重复出现相同的数字。C++中的随机数生成器会根据库的实现而有所不同，但它与我们简单的生成器使用相同的基本思想，并在此基础上进行了一些增强，以实现随机的均匀分布。

如果我们从不同的种子值开始，就可以得到不同的随机数序列。在示例中，种子总是从1开始。然而，如果用一个会变化的数字来初始化种子，比如计算机时钟上的时间，那么每次运行程序时，我们很可能会得到不同的随机数序列。

要为C++的随机数生成器设定种子，可以使用预定义方法srand。它不返回任何值，而是接受一个无符号整数作为输入，即初始种子值。若要始终以35作为随机数生成器的种子，我们可以使用：

```
srand(35);
```

为了让每次执行程序时随机数序列都不同，我们可以用一天中的时间来设定随机数生成器的种子。调用预定义函数time(0)会返回自1970年1月1日¹以来经过的秒数（在大多数系统上）。使用time函数需要包含ctime库。

```
#include <cstdlib>
#include <ctime>
...
srand(time(0));
```

我们可以通过调用rand函数来获得一个随机数，它返回一个0到RAND_MAX范围内的整数。RAND_MAX是在cstdlib中定义的常量，保证为32767或更高。通常，0到RAND_MAX之间的数字并不是我们想要的，这种情况下可以通过取模和加法来缩放随机数。例如，要模拟掷一个六面骰子，我们可以使用以下代码：

```
int die = (rand() % 6) + 1;
```

随机数对6取模后得到0到5之间的数字。加1后得到一个1到6范围内的随机整数。

重要的是，随机数生成器只需设定一次种子。一个常见的错误是在每次生成随机数时都调用srand。如果srand和rand都被放在循环中，那么很可能产生一系列相同的数字，因为计算机运行得足够快，重复调用srand时时间值很可能不会改变。

¹自1970年1月1日以来经过的秒数被称为Unix时间。

## 类型转换

除法可能需要double类型

回想一下，9/2是整数除法，计算结果为4，而不是4.5。如果你希望除法产生double类型的结果（即包含小数点后面的小数部分），那么除法中的两个数字至少有一个必须是double类型。例如，9/2.0的计算结果是4.5。如果两个数字之一是常量，你可以简单地在其中一个（或两个）数字后面加上小数点和一个零，这样除法就会产生一个包含小数点后数字的值。

但是如果除法中的两个操作数都是变量呢，如下所示？

```
int totalCandy, numberOfPeople;
double candyPerPerson;
<The program somehow sets the value of totalCandy to 9
and the value of numberOfPeople to 2.
It does not matter how the program does this.>
candyPerPerson = totalCandy/numberOfPeople;
```

除非你将变量totalCandy或numberOfPeople中的某一个值转换为double类型的值，否则除法的结果将是4，而不是应有的4.5。变量candyPerPerson是double类型这一事实并没有帮助。除法得到的值4在存储到变量candyPerPerson之前会被转换为double类型的值，但那时已经太迟了。4会被转换为4.0，candyPerPerson的最终值将是4.0，而不是4.5。如果除法中的某个量是常量，你可以通过添加小数点和一个零来将该常量转换为double类型，但在这个例子中两个量都是变量。幸运的是，有一种方法可以将int类型转换为double类型，而且无论是常量还是变量都可以使用。

在C++中，你可以告诉计算机将int类型的值转换为double类型的值。你写出“将值9转换为double类型的值”的方式如下：

```
static_cast<double>(9)
```

记法static_cast<double>是一种预定义函数，它把某种其他类型的值（例如9）转换为double类型的值，在这里就是9.0。像static_cast<double>(9)这样的表达式被称为类型转换（type cast）。你可以用变量或其他表达式来代替9。除了double之外，你也可以使用其他类型名来获得转换为其他类型的类型转换，但我们将把这个话题推迟到后面再讨论。

例如，在下面的代码中，我们使用类型转换将9的类型从int改为double，因此answer的值被设置为4.5：

```
double answer;
answer = static_cast<double>(9)/2;
```

对常量（例如9）应用类型转换可以使你的代码更容易阅读，因为它让你的预期含义更清晰。但对int类型的常量应用类型转换并不会给你带来额外的能力。当你想把9转换为double类型的值时，可以使用9.0来代替static_cast<double>(9)。然而，如果除法只涉及变量，那么类型转换可能是你唯一明智的选择。使用类型转换，我们可以重写之前的例子，使变量candyPerPerson接收到正确的值4.5，而不是4.0；要做到这一点，我们唯一需要的修改就是把totalCandy替换为static_cast<double>(totalCandy)，如下所示：

```
int totalCandy, numberOfPeople;
double candyPerPerson;
<The program somehow sets the value of totalCandy to 9
and the value of numberOfPeople to 2.
It does not matter how the program does this.>
candyPerPerson =
    static_cast<double>(totalCandy) / numberOfPeople;
```

请注意代码中类型转换里括号的位置。你需要在除法之前进行类型转换，这样除法运算符处理的就是double类型的值。如果你等到除法完成之后再转换，小数点后的数字就已经丢失了。如果你错误地将上一段代码的最后一行写成下面这样，那么candyPerPerson的值将是4.0，而不是4.5：

```
candyPerPerson =
    static_cast<double>(totalCandy / numberOfPeople);  // WRONG!
```

### 将int转换为double的函数

记法static_cast<double>可以像预定义函数一样使用，它将某种其他类型的值转换为double类型的值。例如，static_cast<double>(2)返回2.0。这被称为类型转换。（类型转换也可以使用double以外的类型，但在本书后面的内容之前，我们只使用double类型进行类型转换。）

### 语法

```
static_cast<double>(Expression_of_Type_int)
```

### 示例

```
int totalPot, numberOfWinners;
double yourWinnings;
...
yourWinnings =
    static_cast<double>(totalPot) / numberOfWinners;
```

警告！

函数totalCost的声明以彩色显示在Display 4.3的顶部，并在此处重现如下：

函数声明告诉你编写函数调用所需的全部信息。它告诉你函数的名称，在这个例子中是totalCost。它告诉你函数需要多少个参数以及参数应该是什么类型；在这个例子中，函数totalCost接受两个参数，第一个是int类型，第二个是double类型。标识符numberPar和pricePar被称为形式参数（formal parameter）。形式参数用作一种占位符，代表实际参数。当你编写函数声明时，你还不知道实际参数会是什么，所以使用形式参数来代替实际参数。形式参数的名称可以是任何有效的标识符，但在一段时间内，我们会让形式参数名称以Par结尾，这样更容易将它们与程序中的其他项区分开来。请注意，函数声明以分号结尾。

函数声明中的第一个单词指定了函数返回值的类型。因此，对于函数totalCost，其返回值的类型是double。

正如你所看到的，Display 4.3中的函数调用满足其函数声明给出的所有要求。让我们来看一下。函数调用在下面这一行：

```
bill = totalCost(number, price);
```

函数调用是等号右侧的表达式。函数名是totalCost，并且有两个参数：第一个参数是int类型，第二个参数是double类型；由于变量bill是double类型，看起来该函数返回了double类型的值（事实也确实如此）。所有这些细节都由函数声明决定。

编译器并不关心函数声明旁边是否有注释，但你总是应该加上一条注释，解释该函数返回什么值。

### 函数声明

函数声明告诉你编写函数调用所需的全部信息。对于定义尚未出现的函数，其函数声明必须出现在代码中调用该函数之前。函数声明通常放在程序主体之前。

（续）

