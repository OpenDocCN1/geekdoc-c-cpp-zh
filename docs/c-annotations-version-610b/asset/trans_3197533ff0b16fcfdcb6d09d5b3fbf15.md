
定义模板成员函数时，不能指定默认模板参数值（无论是类型模板参数还是非类型模板参数）。一般来说：函数模板定义（因而也包括类模板成员函数）不能给定默认模板（非）类型实参。如果类模板成员要使用默认模板实参，它们*必须*由类接口指定。

与函数模板的非类型参数类似，非类型类模板参数的默认实参值只能指定为常量：

- 全局变量具有常量地址，可用作非类型参数的实参。
- 局部变量和动态分配的变量具有编译器在编译源文件时*不*知道的地址。因此这些地址*不能*用作非类型参数的实参。
- 允许左值变换：如果将指针定义为非类型参数，则可以指定数组名。
- 允许限定转换：指向非 const 对象的指针可以与定义为 const 指针的非类型参数一起使用。
- 允许提升：在为“更宽”类型的非类型参数指定默认实参时，可以使用“更窄”数据类型的常量（例如，需要 `int` 时可以使用 `short`，需要 `double` 时可以使用 `long`）。
- 允许整型转换：如果指定了 `size_t` 参数，也可以使用 `int`。
- 变量不能用于指定模板非类型参数，因为它们的值不是常量表达式。然而，使用 `const` 修饰符定义的变量可以使用，因为它们的值永远不会改变。

尽管我们此前尝试为类 `CirQue` 定义一个接受数组作为实参的构造函数至今尚未成功，但我们仍有选择。下一节将描述一种*确实*能让我们达成目标的方法。

### 21.1.3 成员模板

我们之前尝试定义一个由编译器初始化为数组元素数量的模板非类型参数，但失败了，因为调用构造函数时不会隐式推导模板参数。相反，在定义类模板对象时必须显式指定它们。由于模板实参是在调用模板构造函数之前刚刚指定的，编译器不必推导任何内容，只需使用显式指定的模板实参即可。

相比之下，当使用*函数*模板时，实际模板参数会根据调用函数时使用的实参推导出来。这开辟了一条通向问题解决方案的途径。如果构造函数本身被转换为函数模板（拥有自己的模板头），那么编译器*将*能够推导非类型参数的值，并且不再需要使用类模板非类型参数来显式指定它。

本身是模板的类模板成员（函数或嵌套类）称为*成员模板*。

成员模板像任何其他模板一样定义，包括其自己的模板头。

当把我们之前的 `CirQue(Data const (&array)[Size])` 构造函数转换为成员模板时，类模板的 `Data` 类型参数仍然可以使用，但我们必须为该成员模板提供一个自己的非类型参数。它在（部分展示的）类接口中的声明如下所示：

```cpp
template <typename Data>
class CirQue
{
    public:
        template <size_t Size>
        explicit CirQue(Data const (&arr)[Size]);
};
```

其实现变为：

```cpp
template <typename Data>
template <size_t Size>
CirQue<Data>::CirQue(Data const (&arr)[Size])
:
    d_size(0),
    d_maxSize(Size),
    d_data(static_cast<Data *>(operator new(sizeof(arr)))),
    d_front(d_data),
    d_back(d_data)
{
    std::copy(arr, arr + Size, back_inserter(*this));
}
```

该实现使用 STL 的 `copy` 算法和 `back_inserter` 适配器将数组元素插入 `CirQue`。要使用 `back_inserter`，`CirQue` 必须定义两个（公有）typedef（参见第 [18.2.1](#) 节）。

```cpp
typedef Data value_type;
typedef value_type const & const_reference;
```

成员模板具有以下特征：

- 必须使用两个模板头：先指定类模板的 `template` 头，然后指定成员模板的模板头；
- 适用常规访问规则：程序可以使用该成员模板构造给定数据类型的 `CirQue` 对象。像类模板通常那样，在构造对象时必须指定数据类型。要从数组 `array[30]` 构造一个 `CirQue` 对象，我们定义：

  ```cpp
  CirQue<int> object(array);
  ```

- 任何成员都可以定义为成员模板，而不仅仅是构造函数；
- 当模板成员在其类接口下方实现时，模板类头必须位于该成员模板的函数模板头之前；
- 成员模板的实现必须指定其正确的辖域。该成员模板被定义为类 `CirQue` 的成员，并针对形式模板参数类型 `Data` 进行实例化；
- 声明和实现中的模板参数名称必须相同；
- 成员模板应定义在其正确的命名空间环境中。因此，在命名空间内定义类模板的文件组织方式应为：

```cpp
namespace SomeName
{
    template <typename Type, ...>  // class template definition
    class ClassName
    {
        ...
    };

    template <typename Type, ...>    // non-inline member definition(s)
    ClassName<Type, ...>::member(...)
    {
        ...
    }
}                                  // namespace closes
```

还有一个可能出现的问题。假设除了上述成员模板之外，还定义了 `CirQue<Data>::CirQue(Data const *data)`。可以定义某种（此前未详述的）协议，使该构造函数能够确定应存储在 `CirQue` 对象中的元素数量。现在当我们定义

```cpp
CirQue<int> object(array);
```

编译器将使用后一个构造函数，而不是该成员模板。

编译器选择后一个构造函数，因为与成员模板相比，它是类 `CirQue` 的构造函数更特化的版本（参见第 20.14 节）。此类问题可以通过将构造函数 `CirQue(Data const *data)` 也定义为成员模板来解决，或者通过定义一个使用两个参数的构造函数来解决，其中第二个参数定义要复制的元素数量。

当使用前一个构造函数（即成员模板）时，它必须定义一个模板类型参数 `Data2`。这里不能使用“Data”，因为成员模板的模板参数不能遮蔽其类的模板参数。使用 `Data2` 代替 `Data` 可以处理这个细节。以下构造函数 `CirQue(Data2 const *)` 的声明可以出现在 CirQue 的头文件中：

```cpp
template <typename Data>
class CirQue
{
    template <typename Data2>
    explicit CirQue(Data2 const *data);
};
```

以下代码定义两个 `CirQue` 对象，展示了这两个构造函数是如何被选择的：

```cpp
int main()
{
    int array[30];
    int *iPtr = array;

    CirQue<int> ac(array);       // calls CirQue(Data const (&arr)[Size])
    CirQue<int> acPtr(iPtr);     // calls CirQue(Data2 const *)
}
```

### 21.1.4 CirQue 的构造函数和成员函数

现在该再次回到 CirQue 的设计和构造了。

类 `CirQue` 提供了各种成员函数。在构造类模板成员时应遵循常规设计原则。类模板类型参数最好定义为 `Type const &`，而不是 `Type`，以防止不必要地复制大型数据结构。模板类构造函数应使用成员初始化器，而不是在构造函数体内进行成员赋值。成员函数定义最好不在类内提供
