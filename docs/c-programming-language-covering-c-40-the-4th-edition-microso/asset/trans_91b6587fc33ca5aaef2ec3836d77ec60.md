
### 10.14.4.3 Dispose 方法

`Dispose` 方法用于通过将枚举器对象置于 *之后* 状态来清理迭代。

- 如果枚举器对象的状态为 *之前*，则调用 `Dispose` 会将状态更改为 *之后*。
- 如果枚举器对象的状态为 *运行中*，则调用 `Dispose` 的结果未指定。
- 如果枚举器对象的状态为 *挂起*，则调用 `Dispose`：
  - 将状态更改为 *运行中*。
  - 执行任何 `finally` 块，就像最后执行的 `yield return` 语句是 `yield break` 语句一样。如果这导致异常被抛出并传播到迭代器主体之外，则枚举器对象的状态被设置为 *之后*，并且该异常被传播到 `Dispose` 方法的调用方。
  - 将状态更改为 *之后*。
- 如果枚举器对象的状态为 *之后*，则调用 `Dispose` 没有任何效果。

## 10.14.5 可枚举对象

当使用迭代器块实现返回可枚举接口类型的函数成员时，调用该函数成员不会立即执行迭代器块中的代码。相反，会创建并返回一个 *可枚举对象*。可枚举对象的 `GetEnumerator` 方法返回一个枚举器对象，该对象封装迭代器块中指定的代码；迭代器块中代码的执行发生在调用枚举器对象的 `MoveNext` 方法时。可枚举对象具有以下特征：

- 它实现 `IEnumerable` 和 `IEnumerable<T>`，其中 `T` 是迭代器的 yield 类型。
- 它使用传递给该函数成员的参数值（如果有）和实例值的副本进行初始化。

可枚举对象通常是编译器生成的可枚举类的实例，该类封装迭代器块中的代码并实现可枚举接口，但也可以采用其他实现方式。如果可枚举类由编译器生成，则该类将直接或间接嵌套在包含该函数成员的类中，具有私有可访问性，并具有为编译器使用保留的名称（§2.4.2）。

可枚举对象可能实现比上面指定的更多的接口。特别地，可枚举对象还可以实现 IEnumerator 和 IEnumerator<T>，使其既能充当可枚举对象又能充当枚举器。在这种实现类型中，首次调用可枚举对象的 GetEnumerator 方法时，返回可枚举对象本身。之后对可枚举对象的 GetEnumerator 的任何调用都会返回该可枚举对象的副本。因此，每个返回的枚举器都有自己的状态，一个枚举器中的更改不会影响另一个。

### 10.14.5.1 GetEnumerator 方法

可枚举对象提供 IEnumerable 和 IEnumerable<T> 接口的 GetEnumerator 方法的实现。这两个 GetEnumerator 方法共享一个公共实现，该实现获取并返回一个可用的枚举器对象。枚举器对象使用初始化可枚举对象时保存的参数值和实例值进行初始化，但除此之外，枚举器对象的功能如 §10.14.4 所述。

## 10.14.6 实现示例

本节描述基于标准 C# 构造的迭代器的一种可能实现。这里描述的实现基于 Microsoft C# 编译器所使用的相同原则，但它绝不是强制实现，也不是唯一可能的实现。

> BILL WAGNER 当你查看此示例时，请注意，编译器只是创建了你在创建自己的嵌套枚举器类时会生成的所有代码。迭代器方法使你免于大量重复工作，并提高了代码的可读性。

下面的 Stack<T> 类使用迭代器实现其 GetEnumerator 方法。该迭代器按从栈顶到栈底的顺序枚举栈中的元素。

```
using System;
using System.Collections;
using System.Collections.Generic;

class Stack<T> : IEnumerable<T>
{
    T[] items;
    int count;

public void Push(T item)
{
    if (items == null)
    {
        items = new T[4];
    }
    else if (items.Length == count)
    {
        T[] newItems = new T[count * 2];
        Array.Copy(items, 0, newItems, 0, count);
        items = newItems;
    }
    items[count++] = item;
}
public T Pop()
{
    T result = items[--count];
    items[count] = default(T);
    return result;
}
public IEnumerator<T> GetEnumerator()
{
    for (int i = count - 1; i >= 0; --i) yield return items[i];
}
```

GetEnumerator 方法可以转换为编译器生成的枚举器类的实例化，该类封装迭代器块中的代码，如下例所示：

```
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
```

在前面的转换中，迭代器块中的代码被转换为状态机，并放入枚举器类的 MoveNext 方法中。此外，局部变量 i 被转换为枚举器对象中的字段，以便它可以在多次调用 MoveNext 之间继续存在。

以下示例打印整数 1 到 10 的简单乘法表。示例中的 FromTo 方法返回一个可枚举对象，并使用迭代器实现。

```
using System;
using System.Collections.Generic;

class Test
{
    static IEnumerable<int> FromTo(int from, int to)
    {
        while (from <= to) yield return from++;
    }
}
```

```csharp
static void Main()
{
    IEnumerable<int> e = FromTo(1, 10);
    foreach (int x in e)
    {
        foreach (int y in e)
        {
            Console.Write("{0,3}", x * y);
        }
        Console.WriteLine();
    }
}
```

FromTo 方法可以转换为编译器生成的可枚举类的实例化，该类封装迭代器块中的代码，如下例所示：

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
    }
}
```

```
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
```

该可枚举类同时实现可枚举接口和枚举器接口，使其既能充当可枚举对象又能充当枚举器。首次调用 GetEnumerator 方法时，返回可枚举对象本身。之后对可枚举对象的 GetEnumerator 的任何调用都会返回该可枚举对象的副本。因此，每个返回的枚举器都有自己的状态，一个枚举器中的更改不会影响另一个。Interlocked.CompareExchange 方法用于确保线程安全的操作。

from 和 to 参数被转换为可枚举类中的字段。由于 from 在迭代器块中被修改，因此引入了一个额外的 __from 字段，以保存每个枚举器中赋给 from 的初始值。

如果在 __state 为 0 时调用 MoveNext 方法，则它会抛出 InvalidOperationException。这可以防止在未首先调用 GetEnumerator 的情况下将可枚举对象用作枚举器对象。

