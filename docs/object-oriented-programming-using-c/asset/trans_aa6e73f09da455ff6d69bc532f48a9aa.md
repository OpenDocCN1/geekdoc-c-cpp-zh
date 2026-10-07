

# 使用 C# 进行面向对象编程

# 通用集合以及如何序列化它们

列表（Lists）和集合（Sets）在添加项时会自动调整大小。

![](img/e143b38d00f95425fa4f3efca0527189_135_0.png)

List 提供的许多操作也适用于 Set，但是：

- 我们由于元素不按任何顺序排列，因此我们**无法**在特定位置添加对象
- 出同样的原因，我们**无法**“替换”项目（尽管我们可以添加一个项目并删除另一个）
- 获取所有项是可行的，但顺序是不确定的
- 查找某个元素位于什么位置是没有意义的。

# 7.6 字典 (Dictionaries)

字典与列表和集合不同，因为它们存储的不是单个对象，而是对象对。该键值对由一个“键”（key）和一个“值”（value）组成。键是用于标识该对的标识符。值是与键关联的某个或对象。

在语言字典中，我们都很熟悉，“键”是你查阅的单词，而“值”是该单词的含义。当然，在我们所熟悉的字典中，条目是按字母（或键）顺序排序的。如果不是这样，在字典中查找一个单词将非常困难。

另一个例子是地址簿：在地址簿中，键是人的名字，值是他们的地址、电话、电子邮箱等。每个键只有一个对应的值，但由于值是对象，它们可以包含几条数据。

不允许存在重复的键，但允许存在重复的值。因此，在前面的的例子中，如果你在地址簿中查找两个人，可能会发现他们住在同一个地址——但一个人不会有两家房子。

和集合一样，字典不会按顺序排列项（但 SortedDictionary 按键的顺序排列），并且像列表和集合一样，字典在添加或删除项时会自动调整大小。

# 使用 C# 进行面向对象编程

# 通用集合以及如何序列化它们

![](img/e143b38d00f95425fa4f3efca0527189_136_0.png)

# 活动 2

对于以下每个问题，请写下哪种最合适：列表、集合或字典。

- 1) 我们想记录俱乐部的成员。
2) 我们想记录我们花费的钱（以及花在了什么地方）。
3) 我们想记录银行账户详情——每个账户由银行账户号码识别。

# 反馈 2

- 1) 对于此，我们使用集合（Set）。可以根据需要添加和删除成员，且成员没有特定的顺序。
- 2) 对于此，我们使用列表（List）——这将按照购买的顺序记录所购买的项目。重要的是，由于列表允许重复项，我们可以购买两个相同的玩具（也许是给两个不同孩子的生日礼物）。
- 3) 我们不会有两个完全相同的银行账户，所以集合（Set）似乎是合适的，但由于每个账户由唯一的账户号码识别，字典（Dictionary）将是最合适的选择。

# 7.7 一个简单的列表示例

在书的这一部分，我们将演示 List 集合类的简单用法。

| 活动 3 |
| :--- |
| 访问 msdn.microsoft.com。查找在 `System.Collections.Generic` 命名空间定义的 List 类的 API。 |
| 列出你认为最有用的三个方法。 |

| 反馈 3 |
| :--- |
| 一些明显有用的方法包括...
- Add() – 将对象添加到列表的末尾，
- Clear() – 从列表中删除所有元素，
- Contains() – 如果此列表包含指定的对象，则返回 true，
- Insert() – 在指定位置插入元素，
- Remove() – 从列表中移除对象的首次出现项，以及
- Sort() – 对列表的元素进行排序。
注意，某些方法是重载的，例如 Sort()，它可以对整个列表进行排序，也可以只对指定范围的部分排序。 |

![](img/e143b38d00f95425fa4f3efca0527189_137_0.png)

你充满了活力和想法。这正是我们所寻找的。

正在寻找一个可以让你你的想法真正产生影响的职业吗？瑞银（UBS）的毕业生计划和实习是一个让你体验成为全球团队一份的机会，这个团队会奖励你的投入，并相信共同成功。

无论你正处于学术生涯的什么种阶段，请通过访问 www.ubs.com/graduates 让你的未来成为我们未来的一部分。

www.ubs.com/graduates

![](img/e143b38d00f95425fa4f3efca0527189_137_1.png)

# C# 面向对象编程

# 通用集合以及如何如何序列化



下面的代码展示了创建列表的示例。在这种情况下是名称列表，即字符串（Strings）。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace ListOfNames
{
    class Program
    {
        // 创建将存储名称列表的名称
        private static List<String> names;

        static void Main(string[] args)
        {
            names = new List<String>(); // 创建空列表

            string name;
            for (int i = 0; i < 3; i++) // 迭代地向列表添加三个名称
            {
                name = Console.ReadLine();
                names.Add(name);
            }

            foreach (String n in names) // 遍历列表
            {
                Console.WriteLine(n);
            }

            Console.WriteLine("请输入要查找的名称");
            String searchname = Console.ReadLine();
            if (names.Contains(searchname)) // 使用 Contains 方法查找
            {
                Console.WriteLine("找到名称");
            }
            else
            {
                Console.WriteLine("未找到名称");
            }
        }
    }
}
```

上面的代码是非常言自自明的，但有些部分值得解释，特别是列表的创建。首先，由于我们使用了 `System.Collections.Generic`，在创建列表时（调用 List 的构造函数）必须指定列表的类型。

# C# 面向对象编程

# 通用集合以及如何序列化它们

下面的代码展示了创建列表的示例。在这种情况下是名称列表，即字符串（Strings）。

```csharp
private static List<String> names;
```

这种创建是因为直接在 `Main` 中使用了静态变量。当我们调用 List 的构造函数时，必须再次指定类型。

```csharp
names = new List<String>(); // 创建空列表
```

在代码的剩余部分，a) 迭代地向列表添加三个名称，b) 显示列表，c) 使用 `Contains()` 方法查找名称。列表的每个元素都可以像数组元素一样访问（例如 `names[0]`），并且 C# 提供了一个改进的 `for` 循环结构来遍历列表的元素。因此，下面的代码将 `n` 设置为每个元素。

```csharp
foreach (String n in names)
{
    Console.WriteLine(n);
}
```

注意列表中的元素是按顺序存储的，因此在显示列表时顺序保持不变。

此程序存储并处理一个字符串列表，该程序也可以轻松存储从我们创建的类中构建的 Publication列表。

# 7.8 使用列表的更真实的示例

更真实的列表示例将出现在存储更复杂的对象（而不仅仅是字符串）。

考虑下面的 UML 类图。

| Bank | Account |
| :--- | :--- |
| | 1 accounts * - name: String
>-dateBirth: String
>-balance: int |
| +AddAccount(account: Account)
+GetAccount(name: String) | +Account(name: String)
+DepositMoney(increase int)
+ToString() String |

上面的图表代表了银行系统的基础（固然是一个非常简化的银行系统）。在这个系统中，使用一个类来模拟银行并维护一个账户集合……目前我们使用 List 来管理此集合。

此列表的每个元素将代表一个单独的对象账户。一个银行对象将维护所有账户的列表。

每当创建一个账户时，初始余额为零，但所有者可以在需要时存款。因此，我们可以专注于本次练习的核心目的，即演示 List 的用法，我们不会费力添加明显需要的功能（如取款等）。

![](img/e143b38d00f95425fa4f3efca0527189_140_0.png)

141

在 bookboom.com 下载免费电子书

