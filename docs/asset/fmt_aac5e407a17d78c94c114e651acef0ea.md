
```csharp
public void Enqueue(T item) // 使用 T 作为方法参数
{
}
public T Dequeue() // 使用 T 作为返回值
{
    ...
    T queueItem = this.data[this.tail]; // 数组中的数据类型为 T
    return queueItem;
}
```
```csharp
Queue<int> intQueue = new Queue<int>();
Queue<Horse> horseQueue = new Queue<Horse>();
intQueue.Enqueue(99);
int myInt = intQueue.Dequeue(); // 不需要转换
Horse myHorse = intQueue.Dequeue(); // 编译器错误：无法隐式将 'int' 转换为 'Horse'
```
```csharp
struct Person
{
    ...
}
Queue<int> intQueue = new Queue<int>();
Queue<Person> personQueue = new Queue<Person>();
public void Enqueue(Person item);
public Person Dequeue();
Queue<Queue<int>> queuequeue = new Queue<Queue<int>>();
public class PrintableCollection<T> where T : IPrintable
{
    // 如果树 B 为空
    // 构建一个新树 B，以新元素 I 为节点，左右子树均为空
    // 否则
    // 检查树 B 当前节点 N 的值
    // 如果 N 的值大于新元素 I
    // 如果 B 的左子树为空
    // 构建 B 的新左子树，以元素 I 为节点，左右子树均为空
    // 将 I 插入 B 的左子树
    // 如果 B 的右子树为空
    // 构建 B 的新右子树，以元素 I 为节点，左右子树均为空
    // 将 I 插入 B 的右子树
    // 如果左子树不为空
    // 显示左子树的内容
    // 显示节点的值
    // 如果右子树不为空
    // 显示右子树的内容
}
```
```csharp
class Circle
{
    public Circle(int initialRadius)
    {
        radius = initialRadius;
    }
    public double Area()
    {
        return Math.PI * radius * radius;
    }
    private double radius;
}
```
```csharp
class Circle : System.IComparable
{
    public int CompareTo(object obj)
    {
        Circle circObj = (Circle)obj; // 将参数转换为其真实类型
        if (this.Area() == circObj.Area())
            return 0;
        if (this.Area() > circObj.Area())
            return -1;
    }
}
```
```csharp
class Circle : System.IComparable<Circle>
{
    public int CompareTo(Circle other)
    {
        if (this.Area() == other.Area())
            return 0;
        if (this.Area() > other.Area())
            return -1;
    }
}
```
```csharp
public class Tree<TItem> where TItem : IComparable<TItem>
{
}
```
```csharp
public void Insert(TItem newItem)
{
    TItem currentNodeValue = this.nodeData;
    if (currentNodeValue.compareTo(newItem) > 0)
    {
        // 将新项插入到左子树
    }
    else
    {
        // 将新项插入到右子树
    }
    if (this.LeftTree == null)
    {
        this.LeftTree = new Tree<TItem>(newItem);
    }
    else
    {
        this.LeftTree.Insert(newItem);
    }
    if (this.RightTree == null)
    {
            this.RightTree = new Tree<TItem>(newItem);
    }
    else
    {
        this.RightTree.Insert(newItem);
    }
}
```
```csharp
static void Main(string[] args)
{
    Tree<int> treel = new Tree<int>(10);
    treel.Insert(5);
    treel.Insert(11);
    treel.Insert(5);
    treel.Insert(-12);
    treel.Insert(15);
    treel.Insert(0);
    treel.Insert(14);
    treel.Insert(-8);
    treel.Insert(10);
    treel.Insert(8);
    treel.Insert(8);
    string sortedData = treel.WalkTree();
    Console.WriteLine($"Sorted data is: {sortedData}");
}
```
```csharp
static void Main(string[] args)
{
    Tree<string> tree2 = new Tree<string>("Hello");
    tree2.Insert("World");
    tree2.Insert("How");
    tree2.Insert("Are");
    tree2.Insert("You");
    tree2.Insert("Today");
    tree2.Insert("I");
    tree2.Insert("Hope");
    tree2.Insert("You");
    tree2.Insert("Are");
    tree2.Insert("Feeling");
    tree2.Insert("Well");
    tree2.Insert("!");
    sortedData = tree2.WalkTree();
    Console.WriteLine($"Sorted data is: {sortedData}");
}
static void Swap<T>(ref T first, ref T second)
{
    T temp = first;
    first = second;
    second = temp;
}
int a = 1, b = 2;
Swap<int>(ref a, ref b);
...
string s1 = "Hello", s2 = "World";
Swap<string>(ref s1, ref s2);
static void InsertIntoTree<TItem>(ref Tree<TItem> tree, params TItem[] data)
{}
static void InsertIntoTree<TItem>(ref Tree<TItem> tree, params TItem[] data) where TItem : IComparable<TItem>
{
    foreach (TItem datum in data)
    {
        if (tree == null)
        {
            tree = new Tree<TItem>(datum);
        }
        else
        {
            tree.Insert(datum);
        }
    }
}
static void Main(string[] args)
{
    Tree<char> charTree = null;
    InsertIntoTree<char>(ref charTree, 'M', 'X', 'A', 'M', 'Z', 'Z', 'N');
    string sortedData = charTree.WalkTree();
    Console.WriteLine($"Sorted data is: {sortedData}");
}
string myString = "Hello";
object myObjectWrapper = myString;
interface IWrapper<T>
{
    void SetData(T data);
    T GetData();
}
class Wrapper<T> : IWrapper<T>
{
    private T storedData;
    void IWrapper<T>.SetData(T data)
    {
        this.storedData = data;
    }
    T IWrapper<T>.GetData()
    {
        return this.storedData;
    }
}
Wrapper<string> stringWrapper = new Wrapper<string>();
IWrapper<string> storedStringWrapper = stringWrapper;
storedStringWrapper.SetData("Hello");
Console.WriteLine($"stored value is {storedStringWrapper.GetData()}");
IWrapper<object> storedObjectWrapper = (IWrapper<object>)stringWrapper;
Circle myCircle = new Circle();
storedObjectWrapper.SetData(myCircle);
interface IRetrieveWrapper<T>
{
    T GetData();
}
class Wrapper<T> : IStoreWrapper<T>, IRetrieveWrapper<T>
{
    private T storedData;
    void IStoreWrapper<T>.SetData(T data)
    {
        this.storedData = data;
    }
    T IRetrieveWrapper<T>.GetData()
    {
        return this.storedData;
    }
}
Wrapper<string> stringWrapper = new Wrapper<string>();
IStoreWrapper<string> storedStringWrapper = stringWrapper;
storedStringWrapper.SetData("Hello");
IRrievalWrapper<string> retrievedStringWrapper = stringWrapper;
Console.WriteLine($"retrieved value is {retrievedStringWrapper.GetData()}");
IRrievalWrapper<object> retrievedObjectWrapper = (IRrievalWrapper<object>)stringWrapper;
// string 派自 object，所以这是合法的
IRrievalWrapper<object> retrievedObjectWrapper = (IRrievalWrapper<object>)stringWrapper;
interface IRetrieveWrapper<out T>
{
    T GetData();
}
```
```csharp
using System;
using System.Collections.Generic;
...
Queue<int> numbers = new Queue<int>();
// 填充队列
Console.WriteLine("Populating the queue:");
```
```csharp
using System;
using System.Collections.Generic;
...
Stack<int> numbers = new Stack<int>();
// 填充栈
Console.WriteLine("Pushing items onto the stack:");
foreach (int number in new int[4]{9, 3, 7, 2})
{
    numbers.Push(number);
    Console.WriteLine($"{number} has been pushed onto the stack");
}
// 遍历栈
Console.WriteLine("\nThe stack now contains:");
foreach (int number in numbers)
{
    Console.WriteLine(number);
}
// 清空栈
Console.WriteLine("\npping items from the stack:");
while (numbers.Count > 0)
{
    int number = numbers.Pop();
    Console.WriteLine($"{number} has been popped off the stack");
}
```
向栈中推送元素：
9 has been pushed on the stack
3 has been pushed on the stack
7 has been pushed on the stack
2 has been pushed on the stack
栈现在包含：
2
7
3
9
从栈中弹出元素：
2 has been popped off the stack
7 has been popped off the stack
3 has been popped off the stack
9 has been popped off the stack
```csharp
using System;
using System.Collections.Generic;
...
Dictionary<string, int> ages = new Dictionary<string, int>();
// 填充字典
ages.Add("John", 53); // 使用 Add 方法
ages.Add("Diana", 53);
ages["James"] = 26; // 使用数组索引法
ages["Francesca"] = 23;
// 使用 foreach 语句进行遍历
// 迭代器生成 KeyValuePair 项
Console.WriteLine("The Dictionary contains:");\foreach (KeyValuePair<string, int> element in ages)
{
    string name = element.Key;
    int age = element.Value;
    Console.WriteLine($"{name}: Age: {age}");
}
```
字典包含：
Name: John, Age: 53
Name: Diana, Age: 53
Name: James, Age: 26
Name: Francesca, Age: 23
```csharp
using System;
using System.Collections.Generic;
...
SortedList<string, int> ages = new SortedList<string, int>();
// 填充 SortedList
ages.Add("John", 53); // 使用 Add 方法
ages.Add("Diana", 53); // 使用数组索引法
ages["James"] = 26; // 使用数组索引法
```
