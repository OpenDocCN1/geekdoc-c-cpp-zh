

本代码中的重点：

- 静态 String 方法 IsNullOrEmpty 用于确定字符串是否为空或包含 null 值。这是测试字符串是否包含值的首选方法。如果字符串包含 null 值或为空字符串，则返回 true；否则返回 false。
- 语句中用于填充表单上 phoneNumber 文本框的 Text 属性的 ? : 运算符的作用类似于表达式的内联 if...else 语句。它是一个三元运算符，接受以下三个操作数：一个布尔表达式、如果布尔表达式为 true 则求值并返回的表达式，以及如果布尔表达式为 false 则求值并返回的另一个表达式。在前面的代码中，如果表达式 String.IsNullOrEmpty(personsPhoneNumber.Text) 为 true，则在电话簿中未找到匹配项，并且在表单上显示文本“Not Found”；否则，将 personsPhoneNumber 变量的 Text 属性中保存的值显示出来。

? : 运算符的一般形式如下：

Click here to view code image

```
Result = <Boolean Expression> ? <Evaluate if true> :
<Evaluate if false>
```

## 2. 在 MainPage.xaml.cs 文件中定位 findByPhoneNumberClick 方法。

它位于 findByNameClick 方法下方。

findByPhoneNumberClick 方法在单击 Find By Phone Number 按钮时被调用。此方法目前除了一个 // TODO: 注释外为空。你需要按如下方式实现它（完成后代码在以下示例中以粗体显示）：

- a. 从表单上的 phoneNumber 框读取 Text 属性的值。这是一个包含用户输入的电话号码的字符串。
- b. 如果字符串不为空，则使用索引器在 PhoneBook 中搜索与该电话号码对应的名称。
- c. 将索引器返回的 Name 结构体的 Text 属性写入表单上的 name 框。

完成的方法应如下所示：

Click here to view code image

```
private void findByPhoneNumberClick(object sender,
RoutedEventArgs e)
{
    string text = phoneNumber.Text;
    if (!String.IsNullOrEmpty(text))
    {
```

```
PhoneNumber personsPhoneNumber = new PhoneNumber(text);
Name personsName = this.phoneBook[personsPhoneNumber];
name.Text = String.IsNullOrEmpty(personsName.Text) ?
    "Not Found" : personsName.Text;
```

3. 在 Build 菜单上，单击 Build Solution，然后更正出现的任何错误。

## 测试应用程序

- 1. 在 Debug 菜单上，单击 Start Debugging。
- 2. 在适当的框中输入你的姓名和电话号码，然后展开命令栏并单击 Add。 （你可以通过单击省略号来展开命令栏。）

当你单击 Add 按钮时，Add 方法会将信息存储在电话簿中并清除文本框，以便准备进行搜索。

- 3. 使用一些不同的姓名和电话号码重复步骤 2 多次，以便电话簿包含一组条目。请注意，应用程序不对你输入的姓名和电话号码进行任何检查，你可以多次输入相同的姓名和电话号码。为了本次演示的目的，为了避免混淆，请确保你提供不同的姓名和电话号码。
- 4. 在 Name 框中输入你在步骤 3 中使用过的姓名，然后单击 Find By Name。

在步骤 3 中为此联系人添加的电话号码将从电话簿中检索并显示在 Phone Number 文本框中。

- 5. 在 Phone Number 框中输入不同联系人的电话号码，然后单击 Find By Phone Number。

联系人姓名将从电话簿中检索并显示在 Name 框中。

- 6. 在 Name 框中输入一个你未在电话簿中输入的姓名，然后单击 Find By Name。

这次，Phone Number 框将显示消息“Not Found”。

- 7. 关闭表单并返回 Visual Studio 2015。

## 摘要

在本章中，你了解了如何使用索引器以类比数组的方式访问类中的数据。你学习了如何创建可以接受索引并使用 get 访问器定义的逻辑返回相应值的索引器，并且你看到了

如何使用 set 访问器和索引来填充索引器中的值。

- 如果你想继续下一章，请保持 Visual Studio 2015 运行并转到第 17 章，“Introducing generics。”
- 如果你现在想退出 Visual Studio 2015，请在 File 菜单上单击 Exit。如果出现 Save 对话框，请单击 Yes 并保存项目。

## 快速参考

| To | Do this |
|---|---|
| 为类或结构创建索引器 | 声明索引器的类型，后跟关键字 this，然后在方括号中指定索引器参数。索引器的主体可以包含 get 和/或 set 访问器。例如：
```
struct RawInt
{
    ...
    public bool this [ int index ]
    {
        get { ... }
        set { ... }
    }
    ...
}
``` |
| 在接口中定义索引器 | 使用 get 和/或 set 关键字定义索引器。例如：
```
interface IRawInt
{
    bool this [ int index ] { get;  set; }
}
``` |
| 在类或结构中实现接口索引器 | 在实现接口的类或结构中，定义索引器并实现访问器。例如：
```
struct RawInt : IRawInt
{
    ...
    public bool this [ int index ]
    {
        get { ... }
        set { ... }
    }
    ...
}
``` |
| 在类或结构中使用显式接口实现实现由接口定义的索引器 | 在实现接口的类或结构中，指定接口但不指定索引器的可访问性。例如：
```
struct RawInt : IRawInt
{
    ...
    bool IRawInt.this [ int index ]
    {
        get { ... }
        set { ... }
    }
    ...
}
``` |

## 第 17 章。Introducing generics

完成本章后，你将能够：

- 解释泛型的目的。
- 使用泛型定义类型安全的类。
- 基于指定为类型参数的类型创建泛型类的实例。
- 实现泛型接口。
- 定义一个泛型方法，该方法实现独立于其操作的数据类型的算法。

第 8 章，“Understanding values and references，”向你展示了如何使用 *object* 类型引用任何类的实例。你可以使用 *object* 类型存储任何类型的值，并且当你需要将任何类型的值传递给方法时，可以使用 *object* 类型定义参数。方法还可以通过指定 *object* 作为返回类型来返回任何类型的值。虽然这种做法非常灵活，但它要求程序员记住实际使用的是什么样的数据。如果程序员犯错，这可能导致运行时错误。在本章中，你将学习泛型，这是一种旨在帮助你防止此类错误的功能。

## object 类型的难题

为了理解泛型，值得详细了解它们旨在解决的问题。

假设你需要模拟一个先进先出结构，例如队列。

你可以创建如下的类：

Click here to view code image

```
class Queue
{
    private const int DEFAULTQUEUESIZE = 100;
    private int[] data;
    private int head = 0, tail = 0;
    private int numElements = 0;

    public Queue()
    {
        this.data = new int[DEFAULTQUEUESIZE];
    }
    public Queue(int size)
    {
        if (size > 0)
        {
            this.data = new int[size];
        }
    }
```

```
else
{
    throw new ArgumentOutOfRangeException("size", "Must be greater than zero");
}
}

public void Enqueue(int item)
{
    if (this.numElements == this.data.Length)
    {
        throw new Exception("Queue full");
    }

    this.data[this.head] = item;
    this.head++;
    this.head %= this.data.Length;
    this.numElements++;
}

public int Dequeue()
{
    if (this.numElements == 0)
    {
        throw new Exception("Queue empty");
    }

    int queueItem = this.data[this.tail];
    this.tail++;
    this.tail %= this.data.Length;
    this.numElements--;
    return queueItem;
}
}
```

该类使用数组为保存数据提供循环缓冲区。此数组的大小由构造函数指定。应用程序使用 Enqueue 方法将项目添加到队列，并使用 Dequeue 方法从队列中取出项目。私有的 head 和 tail 字段跟踪在数组中插入项目的位置以及从数组中检索项目的位置。numElements 字段指示数组中有多少项目。Enqueue 和 Dequeue 方法使用这些字段来确定存储或检索项目的位置并执行一些基本的错误检查。应用程序可以创建 Queue 对象并调用这些方法，如以下代码示例所示。请注意，项目是按它们入队的相同顺序出队的：

Click here to view code image

```
Queue queue = new Queue(); // Create a new Queue

queue.Enqueue(100);
queue.Enqueue(-25);
queue.Enqueue(33);
Console.WriteLine($"{queue.Dequeue()}");  // Displays 100
```

