
-   它实现了 `IEnumerable` 和 `IEnumerable<T>`，其中 `T` 是迭代器的 yield 类型。
-   它使用参数值（如果有）的副本以及传递给函数成员的实例值进行初始化。

可枚举对象通常是编译器生成的可枚举类的实例，该类封装了迭代器块中的代码并实现了可枚举接口，但也存在其他实现方法。如果可枚举类由编译器生成，则该类将直接或间接嵌套在包含函数成员的类中，它将具有私有访问权限，并且其名称将保留供编译器使用（§2.4.2）。

可枚举对象可能实现比上述指定的更多接口。特别是，可枚举对象还可能实现 `IEnumerator` 和 `IEnumerator<T>`，使其既可作为可枚举对象又可作为枚举器。在这种类型的实现中，可枚举对象的 `GetEnumerator` 方法首次被调用时，返回可枚举对象本身。随后对可枚举对象的 `GetEnumerator` 的调用（如有）将返回可枚举对象的副本。因此，每个返回的枚举器都有自己的状态，一个枚举器的更改不会影响另一个。

### 10.14.5.1 GetEnumerator 方法

可枚举对象提供了 `IEnumerable` 和 `IEnumerable<T>` 接口的 `GetEnumerator` 方法的实现。两个 `GetEnumerator` 方法共享一个公共实现，该实现获取并返回一个可用的枚举器对象。枚举器对象使用在可枚举对象初始化时保存的参数值和实例值进行初始化，但除此之外，枚举器对象按 §10.14.4 中所述运行。

### 10.14.6 实现示例

本节描述了使用标准 C# 结构实现迭代器的一种可能方法。此处描述的实现基于 Microsoft C# 编译器使用的相同原理，但它绝不是强制性的实现，也不是唯一可能的实现。

以下 `Stack<T>` 类使用迭代器实现其 `GetEnumerator` 方法。迭代器按从栈顶到底的顺序枚举栈中的元素。

```csharp
using System;
using System.Collections;
using System.Collections.Generic;

class Stack<T>: IEnumerable<T>
{
    T[] items;
    int count;

    public void Push(T item) {
        if (items == null) {
            items = new T[4];
        }
        else if (items.Length == count) {
            T[] newItems = new T[count * 2];
            Array.Copy(items, 0, newItems, 0, count);
            items = newItems;
        }
        items[count++] = item;
    }

    public T Pop() {
        T result = items[--count];
        items[count] = default(T);
        return result;
    }

    public IEnumerator<T> GetEnumerator() {
        for (int i = count - 1; i >= 0; --i) yield return items[i];
    }
}
```

GetEnumerator 方法可以被翻译为编译器生成的枚举器类的实例化，该类封装了迭代器块中的代码，如下所示。

```csharp
class Stack<T>: IEnumerable<T>
{
    ...
    public IEnumerator<T> GetEnumerator() {
        return new __Enumerator1(this);
    }
    class __Enumerator1: IEnumerator<T>, IEnumerator
    {
        int __state;
        T __current;
        Stack<T> __this;
        int i;
        public __Enumerator1(Stack<T> __this) {
            this.__this = __this;
        }
        public T Current {
            get { return __current; }
        }
        object IEnumerator.Current {
            get { return __current; }
        }
        public bool MoveNext() {
            switch (__state) {
                case 1: goto __state1;
                case 2: goto __state2;
            }
            i = __this.count - 1;
        __loop:
            if (i < 0) goto __state2;
            __current = __this.items[i];
            __state = 1;
            return true;
        __state1:
            --i;
            goto __loop;
        __state2:
            __state = 2;
            return false;
        }
        public void Dispose() {
            __state = 2;
        }
        void IEnumerator.Reset() {
            throw new NotSupportedException();
        }
    }
}
```

在前面的转换中，迭代器块中的代码被转换为状态机并放置在枚举器类的 MoveNext 方法中。此外，局部变量 i 被转换为枚举器对象中的字段，以便它可以在 MoveNext 的多次调用之间继续存在。

以下示例打印 1 到 10 的整数的简单乘法表。示例中的 FromTo 方法返回一个可枚举对象，并使用迭代器实现。

```csharp
using System;
using System.Collections.Generic;
class Test
{
    static IEnumerable<int> FromTo(int from, int to) {
        while (from <= to) yield return from++;
    }

    static void Main() {
        IEnumerable<int> e = FromTo(1, 10);
        foreach (int x in e) {
            foreach (int y in e) {
                Console.Write("{0,3} ", x * y);
            }
            Console.WriteLine();
        }
    }
}
```

FromTo 方法可以被翻译为编译器生成的可枚举类的实例化，该类封装了迭代器块中的代码，如下所示。

```csharp
using System;
using System.Threading;
using System.Collections;
using System.Collections.Generic;
class Test
{
    ...
    static IEnumerable<int> FromTo(int from, int to) {
        return new __Enumerable1(from, to);
    }

    class __Enumerable1:
        IEnumerable<int>, IEnumerable,
        IEnumerator<int>, IEnumerator
    {
        int __state;
        int __current;
        int __from;
        int from;
        int to;
        int i;

        public __Enumerable1(int __from, int to) {
            this.__from = __from;
            this.to = to;
        }

        public IEnumerator<int> GetEnumerator() {
            __Enumerable1 result = this;
            if (Interlocked.CompareExchange(ref __state, 1, 0) != 0) {
                result = new __Enumerable1(__from, to);
                result.__state = 1;
            }
            result.from = result.__from;
            return result;
        }

        IEnumerator IEnumerable.GetEnumerator() {
            return (IEnumerator)GetEnumerator();
        }

        public int Current {
            get { return __current; }
        }
        object IEnumerator.Current {
            get { return __current; }
        }
        public bool MoveNext() {
            switch (__state) {
                case 1:
                    if (from > to) goto case 2;
                    __current = from++;
                    __state = 1;
                    return true;
                case 2:
                    __state = 2;
                    return false;
                default:
                    throw new InvalidOperationException();
            }
        }
        public void Dispose() {
            __state = 2;
        }
        void IEnumerator.Reset() {
            throw new NotSupportedException();
        }
    }
}
```

可枚举类同时实现了可枚举接口和枚举器接口，使其既可作为可枚举对象又可作为枚举器。首次调用 GetEnumerator 方法时，返回可枚举对象本身。随后对可枚举对象的 GetEnumerator 的调用（如有）将返回可枚举对象的副本。因此，每个返回的枚举器都有自己的状态，一个枚举器的更改不会影响另一个。Interlocked.CompareExchange 方法用于确保线程安全操作。

from 和 to 参数被转换为可枚举类中的字段。由于 from 在迭代器块中被修改，因此引入了额外的 __from 字段来保存为每个枚举器提供的 from 的初始值。

如果在 __state 为 0 时调用 MoveNext 方法，则会抛出 InvalidOperationException。这可防止在未先调用 GetEnumerator 的情况下将可枚举对象用作枚举器对象。

以下示例展示了一个简单的树类。Tree<T> 类使用迭代器实现其 GetEnumerator 方法。迭代器以中缀顺序枚举树中的元素。

```csharp
using System;
using System.Collections.Generic;
class Tree<T>: IEnumerable<T>
{
    T value;
    Tree<T> left;
    Tree<T> right;
    public Tree(T value, Tree<T> left, Tree<T> right) {
        this.value = value;
        this.left = left;
        this.right = right;
    }
```
