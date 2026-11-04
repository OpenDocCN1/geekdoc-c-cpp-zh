
-   **MoveNext()**: 将枚举器从集合中的当前对象移动到下一个对象。
-   **Current**: 一个属性，而不是方法，用于检索枚举器当前位置存储的数据对象。

以下方法演示了这一原理。MyCollection 类（未显示）的程序员创建了相应的迭代器类——比如 IteratorMyCollection（使用我在本章前面描述的 IteratorX 命名约定）。应用程序程序员已在 MyCollection 中存储了大量 ContainedDataObjects。以下代码段使用三个标准的 IEnumerable 方法将这些对象读出：

```csharp
// The MyCollection class holds ContainedDataObject type objects as data.
void MyMethod(MyCollection myColl)
{
    // The programmer who created the MyCollection class also
    // creates an iterator class IteratorMyCollection;
    // the application program creates an iterator object
    // in order to navigate through the myColl object.
    IEnumerator iterator = new IteratorMyCollection(myColl);
    // Move the enumerator to the 'next location' within the collection.
    while(iterator.MoveNext())
    {
        // Fetch a reference to the data object at the current location
        // in the collection.
        ContainedDataObject contained;  // Data
        contained = (ContainedDataObject)iterator.Current;
        // ...use the contained data object...
    }
}
```

方法 MyMethod() 将 ContainedDataObjects 的集合作为其参数。它首先创建 IteratorMyCollection 类的迭代器。方法通过调用 MoveNext() 开始循环。在此次首次调用中，MoveNext() 将迭代器移动到集合中的第一个元素。在每次后续调用中，MoveNext() 将指针移动“一个位置”。当集合耗尽且迭代器无法再移动时，MoveNext() 返回 false。

Current 属性返回迭代器当前位置的数据对象的引用。程序在将其分配给 contained 之前，将返回的对象转换为 ContainedDataObject。如果 MoveNext() 方法在上一次调用中未返回 true，或者尚未调用 MoveNext()，则对 Current 的调用无效。

## 让 C# 通过 foreach 访问容器数据

IEnumerable 方法足够标准，以至于 C# 会自动使用它们来实现 foreach 语句。foreach 语句可以访问实现 IEnumerable 或 IEnumerable<T> 的任何类。本节我以 IEnumerable<T> 讨论 foreach，如下所示的通用方法能够处理此类任何类，从数组到链表再到栈和队列：

```csharp
void MyMethod(IEnumerable<T> containerOfThings)
{
    foreach(string s in containerOfThings)
    {
        Console.WriteLine("The next thing is {0}", s);
    }
}
```

类通过定义 GetEnumerator() 方法来实现 IEnumerable<T>，该方法返回 IEnumerator<T> 的实例。在内部，foreach 调用 GetEnumerator() 方法来检索迭代器。它使用此迭代器遍历集合。它检索到的每个元素在进入大括号内包含的代码块之前都已适当转换。注意 IEnumerable<T> 和 IEnumerator<T> 是不同但相关的接口。C# 也提供了非泛型版本，但你应优先使用泛型版本以获得更高的类型安全性。

IEnumerable<T> 看起来像这样：

```csharp
interface IEnumerable<T>
{
    IEnumerator<T> GetEnumerator();
}
```

而 IEnumerator<T> 看起来像这样：

```csharp
interface IEnumerator<T>
{
    bool MoveNext();
    T Current { get; }
}
```

非泛型 IEnumerator 接口添加了 Reset() 方法，该方法将迭代器移回集合的开头，其 Current 属性返回类型为 Object。注意 IEnumerator<T> 继承自 IEnumerator——请记住接口继承（在第二册第 8 章中介绍）与普通对象继承不同。

C# 数组（以它们基于的 Array 类体现）和所有 .NET 集合类已经实现了这两个接口。因此，只有在编写自己的自定义集合类时才需要处理实现这些接口。对于内置集合，你可以直接使用它们。参见帮助中的 System.Collections.Generic 命名空间主题。

因此你可以这样编写 foreach 循环：

## 以数组方式访问集合：索引器

访问数组的元素很简单：命令 container[n]（读作“container sub-n”）访问容器数组的第 n 个元素。方括号中的值是下标。如果只能对其他类型的集合进行索引就这么简单就好了。

停止印刷！C# 使你能够编写索引操作的自己的实现。你可以为原本不会拥有此功能的集合提供索引功能。此外，你可以对除 C# 数组所限定的简单整数之外的下标类型进行索引；例如字符串；另一个例子，尝试 container["Joe"]。

### 索引器格式

索引器看起来很像普通的 get/set 属性，只是出现了关键字 this 和索引运算符 [] 而不是属性名，如以下代码所示：

```csharp
class MyArray
{
    public string this[int index]  // Notice the 'this' keyword.
    {
        get
        {
            return array[index];
        }
        set
        {
            array[index] = value;
        }
    }
}
```

在内部，表达式 s = myArray[i]; 调用 get 访问器方法，将 i 的值作为索引传递给它。此外，表达式 myArray[i] = "some string"; 调用 set 访问器方法，将相同的索引 i 和 "some string" 作为值传递给它。

### 索引器程序示例

索引类型不限于 int。你可以选择按房屋所有者的姓名、房屋地址或任何其他索引来索引房屋集合。此外，索引器属性可以用多个索引类型重载，因此你可以在同一集合中的各种元素上进行索引。

以下 Indexer 程序生成虚拟数组类 KeyedArray。此虚拟数组看起来并表现得像数组，只是它使用字符串值作为索引：

![](img/80ff26f06fc9ab951e1cd4257b867366_169_0.png)

```csharp
// Indexer -- This program demonstrates the use of the index operator
// to provide access to an array using a string as an index.
// This version is nongeneric, but see the IndexerGeneric example.
using System;

namespace Indexer
{
    public class KeyedArray
    {
        // The following string provides the "key" into the array --
        // the key is the string used to identify an element.
        private string[] _keys;

        // The object is the actual data associated with that key.
        private object[] _arrayElements;

        // KeyedArray -- Create a fixed-size KeyedArray.
        public KeyedArray(int size)
        {
            _keys = new string[size];
            _arrayElements = new object[size];
        }

        // Find -- Find the index of the element corresponding to the
        // string targetKey (return a negative if it can't be found).
        private int Find(string targetKey)
        {
            for (int i = 0; i < _keys.Length; i++)
            {
                if (String.Compare(_keys[i], targetKey) == 0)
                {
                    return i;
                }
            }
            return -1;
        }

        // FindEmpty -- Find room in the array for a new entry.
        private int FindEmpty()
        {
            for (int i = 0; i < _keys.Length; i++)
            {
                if (_keys[i] == null)
                {
                    return i;
                }
            }

            throw new Exception("Array is full");
        }

        // Look up contents by string key -- this is the indexer.
        public object this[string key]
        {
            set
            {
                // See if the string is already there.
```
