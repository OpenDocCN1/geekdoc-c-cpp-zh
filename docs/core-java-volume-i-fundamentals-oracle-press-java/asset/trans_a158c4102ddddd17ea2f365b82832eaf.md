
`size` 方法返回数组列表中元素的实际数量。例如，

```
staff.size()
```

返回 `staff` 数组列表中当前元素的数量。这等价于

```
a.length
```

对于数组 a 而言。

一旦你相当确定数组列表已达到其最终大小，就可以调用 `trimToSize` 方法。此方法会调整内存块的大小，使其正好使用容纳当前元素数量所需的存储空间。垃圾回收器将回收任何多余的内存。

一旦修剪了数组列表的大小，添加新元素将再次移动该内存块，这需要时间。只有当你确定不会再向数组列表添加任何元素时，才应使用 `trimToSize`。

### C++ 注意：

`ArrayList` 类与 C++ 的 vector 模板类似。ArrayList 和 vector 都是泛型类型。但 C++ 的 vector 模板重载了 `[]` 运算符，以便于访问元素。Java 不支持运算符重载，因此必须改用显式方法调用。此外，C++ 的 vector 是按值复制的。如果 a 和 b 是两个 vector，那么赋值 a = b 会使 a 成为一个新 vector，其长度与 b 相同，并且所有元素都从 b 复制到 a。而在 Java 中，同样的赋值会使 a 和 b 都引用同一个数组列表。

## `java.util.ArrayList<E>` 1.2

- `ArrayList<E>()`
  构造一个空数组列表。
- `ArrayList<E>(int initialCapacity)`
  构造一个具有指定容量的空数组列表。
- `boolean add(E obj)`
  将 obj 追加到数组列表末尾。始终返回 true。
- `int size()`
  返回当前存储在数组列表中的元素数量。（当然，这永远不会大于数组列表的容量。）
- `void ensureCapacity(int capacity)`
  确保数组列表具有存储给定数量元素的能力，而无需重新分配其内部存储数组。
- `void trimToSize()`
  将数组列表的存储容量减少到其当前大小。

### 5.3.2 访问数组列表元素

不幸的是，天下没有免费的午餐。数组列表自动增长的便利性要求使用更复杂的语法来访问元素。原因是 `ArrayList` 类并不是 Java 编程语言的一部分；它只是一个由某人编写并随标准库提供的实用类。

不能使用令人愉快的 `[ ]` 语法来访问或修改数组元素，而应使用 get 和 set 方法。

例如，要设置第 i 个元素，请使用

```
staff.set(i, harry);
```

这等价于

```
a[i] = harry;
```

对于数组 a 而言。（与数组一样，索引值从零开始。）

### 警告：

在数组列表的*大小*大于*i*之前，不要调用 `list.set(i, x)`。例如，以下代码是错误的：

```
var list = new ArrayList<Employee>(100); // capacity 100, size 0
list.set(0, x); // no element 0 yet
```

使用 add 方法而不是 set 方法来填充数组，并且仅使用 set 来替换先前添加的元素。

要获取数组列表元素，请使用

```
Employee e = staff.get(i);
```

这等价于

```
Employee e = a[i];
```

### 注意：

当还没有泛型类时，原始 `ArrayList` 类的 `get` 方法别无选择，只能返回 `Object`。因此，`get` 的调用者必须将返回值强制转换为所需类型：

```
Employee e = (Employee) staff.get(i);
```

原始 `ArrayList` 也有点危险。它的 add 和 set 方法接受任何类型的对象。调用

```
staff.set(i, "Harry Hacker");
```

编译时甚至连警告都不会有，只有当你取出该对象并尝试强制转换时才会遇到麻烦。如果改用 `ArrayList<Employee>`，编译器将检测到此错误。

有时，你可以通过以下技巧兼得两者之长——灵活的增长和方便的元素访问。首先，创建一个数组列表并添加所有元素：

```
var list = new ArrayList<X>();
while (. . .)
{
    x = . . .;
    list.add(x);
}
```

完成后，使用 `toArray` 方法将元素复制到数组中：

```
var a = new X[list.size()];
list.toArray(a);
```

有时，你需要在数组列表中间添加元素。使用带索引参数的 add 方法：

```
int n = staff.size() / 2;
staff.add(n, e);
```

位置 n 及以上的元素会向上移动，为新条目腾出空间。如果插入后数组列表的新大小超过容量，数组列表将重新分配其存储数组。

类似地，你可以从数组列表中间删除一个元素：

```
Employee e = staff.remove(n);
```

位于其上的元素会向下复制，数组列表的大小减一。

插入和删除元素的效率并不是很高。对于小型数组列表，可能不值得担心。但如果你存储许多元素并频繁在集合中间插入和删除，请考虑改用链表。我将在第 9 章解释如何使用链表编程。

你可以使用“for each”循环遍历数组列表的内容：

```
for (Employee e : staff)
    do something with e
```

此循环与以下代码效果相同：

```
for (int i = 0; i < staff.size(); i++)
{
    Employee e = staff.get(i);
    do something with e
}
```

程序清单 5.7 是第 4 章 `EmployeeTest` 程序的修改版。`Employee[]` 数组被替换为 `ArrayList<Employee>`。请注意以下变化：

- 不必指定数组大小。
- 使用 `add` 添加任意数量的元素。
- 使用 `size()` 而不是 `length` 来统计元素数量。

## `java.util.ArrayList<E>` 1.2

- `E set(int index, E obj)`
  将值 obj 放入数组列表中指定索引处，并返回先前的内容。
- `E get(int index)`
  获取存储在指定索引处的值。
- `void add(int index, E obj)`
  向上移动元素，以便在指定索引处插入 obj。
- `E remove(int index)`
  删除给定索引处的元素，并向下移动其上方所有元素。返回被删除的元素。

### 5.3.3 类型化数组列表与原始数组列表的兼容性

在你自己的代码中，为了增加安全性，你总是希望使用类型参数。在本节中，你将看到如何与不使用类型参数的遗留代码进行互操作。

假设你有以下遗留类：

```
public class EmployeeDB
{
    public void update(ArrayList list) { . . . }
    public ArrayList find(String query) { . . . }
}
```

你可以将类型化数组列表传递给 update 方法，而无需任何强制转换。

```
ArrayList<Employee> staff = . . .;
employeeDB.update(staff);
```

staff 对象被直接传递给 update 方法。

### 警告：

即使编译器没有给出错误或警告，此调用也并非完全安全。`update` 方法可能会向数组列表中添加不是 `Employee` 类型的元素。当取出这些元素时，会发生异常。这听起来很可怕，但如果你仔细想想，这种行为与 Java 添加泛型之前完全一样。虚拟机的完整性永远不会受到损害。在这种情况下，你没有失去安全性，但也没有从编译时检查中获益。

相反，当你将原始 `ArrayList` 赋值给类型化 `ArrayList` 时，会收到警告。

```
ArrayList<Employee> result = employeeDB.find(query); // yields warning
```

### 注意：

要查看警告文本，请使用 `-Xlint:unchecked` 选项进行编译。

使用强制转换并不能使警告消失。

```
ArrayList<Employee> result = (ArrayList<Employee>) employeeDB.find(query);
    // yields another warning
```

相反，你会收到另一个警告，告诉你该强制转换具有误导性。
