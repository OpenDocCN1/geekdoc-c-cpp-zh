
## 表 5.2 _(继续)_

| 智能指针 | 描述 | 示例 |
|---|---|---|
| **unique_ptr** | `unique_ptr` 是一个模板类，用于独占所有权（对象或对象数组），因此会自动删除其持有的对象。`unique_ptr` 行为就像指向持有对象的指针。其属性如下：

- 不能复制；只允许移动操作。
- `unique_ptr` 必须使用 `make_unique` 函数初始化。
- 可以设置自定义删除函数，以便在对象删除前执行额外操作。
- 可以轻松复制为 `shared_ptr`。

一个 `unique_ptr<T>` 负责单个对象 `T` 的生命周期。

`auto up_0 = std::make_unique<T>();` | `// 在堆上分配一个 double 对象，初始化为 0.0，并创建一个 unique_ptr`
`unique_ptr<double> real_val_0(new double(0.0)); // 正确`
`// 在堆上分配一个 double 对象，初始化为 0.0，并通过 make_unique 创建 unique_ptr，更好，可以使用 auto。`
`auto real_val_1 = make_unique<double>(0.0); // 更好`
`assert(real_val_1.get() != nullptr); // 检查分配的指针是否为 nullptr`
`*real_val_1 = 3.14; // 使用方式与普通指针相同`
`// 在堆上分配一个包含 16 个 double 的数组 – 通过 unique_ptr 访问`
`unique_ptr<double[]> real_array_0(new double[16]);`
`// 但 real_array_0 指向的元素不进行初始化！ // 正确` |

**图示：** `std::unique_ptr<T>` 指向类型 `T` 的对象；示例中 `up_0` 为指向该对象的指针，所有权用虚线边框表示。

## class AClass

```cpp
class AClass
{
    string fStr;
public:
    AClass( const string & s = "" ) : fStr(s) {}
    ~AClass() { cout << "AClass destructor" << endl; }
    const string GetStr( void ) const { return fStr; }
    void SetStr( const string & s ) { fStr = s; }
};
```

// 堆上创建的 AClass 对象，p_d_1 负责其生命周期
`unique_ptr< AClass > p_d_1( new AClass( "Good" ) );`
// 更好的做法是使用 make_unique 辅助函数
`auto p_d_2( make_unique< AClass >( "Better" ) );`

```cpp
if( p_d_2 )
{
    cout << p_d_2->GetStr() << endl;    // 通过指针访问
    cout << ( * p_d_2 ).GetStr() << endl; // 通过对象访问
}

//unique_ptr< AClass > p_d_3 = p_d_2;  // 不能复制，会编译错误
unique_ptr< AClass > p_d_3 = std::move( p_d_2 );    // 可以移动
// 其他智能指针

// 在堆上创建一个 AClass 数组对象，p_d_4
const int kAClassElems = 4;
auto p_d_4( make_unique< AClass [] >( kAClassElems ));// 调用默认构造函数
// 每个元素都会调用构造函数
```

`make_unique` 让我们能够传递构造对象所需的任意参数。另一个优势是可以直接使用 `auto` 而无需显式写出完整的类型名称。需要注意的是，`unique_ptr` 不能复制，因为两个智能指针不能共同删除同一个对象。不过，可以使用 `std::move` 将一个 `unique_ptr` 的内容轻松移动到另一个智能指针 —  — 在本例中，`p_d_2` 通过这种方式被移动到 `p_d_3`。

## shared_ptr 成员函数表

| 成员 | 描述 |
|---|---|
| `shared_ptr` | 默认构造函数和模板构造函数 |
| `operator *` | 解引用，获取持有的对象 |
| `operator ->` | 指针访问持有的对象 |
| `operator bool` | 检查是否关联了对象（是否为空） |
| `get` | 返回指向对象的原始指针 |
| `reset` | 获取新对象并删除旧对象 |
| `use_count` | 返回与同一对象关联的 `shared_ptr` 数量 |

## shared_ptr 示例

下面是一个对象 `T` 及其关联的 `shared_ptr`（分配了控制块）的示例：

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_376_0.png)

在大多数情况下，使用 `make_shared` 辅助函数创建 `shared_ptr` 是最佳选择。它可以让我们使用 `auto` 来推断类型，并且是线程安全的（例如在 (Meyers 2014) 中描述的异常处理）。它还允许我们传递任意参数列表来构造对象。如果堆内存不足等情况，最好检查 `shared_ptr` 是否仍持有有效的对象指针。这可以通过下面两个 `assert` 实现：第一个使用重载的布尔类型进行检查，第二个调用 `get` 与 `nullptr` 比较。

创建 `shared_ptr` 后，引用计数会递增。与 `unique_ptr` 不同，复制 `shared_ptr`（例如从 `sp_0` 复制到 `sp_1`）是完全可以的，此时公共引用计数会增加到 2。这个值可以通过任意 `shared_ptr` 调用 `use_count` 成员读取。类似于 `unique_ptr`，`shared_ptr` 也可以像普通指针一样访问持有的对象。

下面的代码输出如下：

```
Hold by shared = Hold by shared
sp_0 count = 2, sp_1 count = 2
after reset sp_0 count = 0, sp_1 count = 1
```

`shared_ptr` 可以从 `unique_ptr` 中创建：

```cpp
auto up_0 = make_unique< AClass >( "Created by unique" );
shared_ptr< AClass > sp_2 = move( up_0 );
auto sp_3 = sp_2;
cout << sp_2->GetStr() << " " << " ( *sp_3 ).GetStr() << endl;   // 访问
// 同一个对象
cout << "sp_2 count = " << sp_2.use_count() << " " , sp_3 count = 
<< sp_3.use_count() << endl;
```

`shared_ptr` 还可以管理数组对象的生命周期。它重载了构造函数，以允许普通指针指向此类数组。同样，可以有多个 `shared_ptr` 指向同一数组对象 —  — 在前面的示例中有两个：`sp_4` 和 `sp_5`。此时输出如下：

```
sp_4 count = 1
sp_4 = 4, 2, sp_5 count = 2

AClass destructor
AClass destructor
AClass destructor
AClass destructor
AClass destructor
AClass destructor
AClass destructor
AClass destructor
AClass destructor
AClass destructor
AClass destructor
AClass destructor
AClass destructor
```

起初 `sp_4` 的引用计数为 1。随后通过 `sp_4` 访问的八个空字符串被显示。随后 `sp_4` 与 `sp_5` 合并，引用计数增至 2，如下一行所示。最终，所有 `shared_ptr` 离开作用域并被销毁，导致所有 `AClass` 对象被销毁，如 `AClass` 构造函数中显示的析构函数消息所示。这里包括两个单独的 `AClass` 对象以及数组中的八个对象。

`shared_ptr` 常用成员函数：

| 成员 | 描述 |
|---|---|
| `shared_ptr` | 默认构造函数和模板构造函数 |
| `operator *` | 解引用，获取持有的对象 |
| `operator ->` | 指针访问持有的对象 |
| `operator bool` | 检查是否关联了对象（是否为空） |
| `get` | 返回指向对象的原始指针 |
| `reset` | 获取新对象并删除旧对象 |
| `use_count` | 返回与同一对象关联的 `shared_ptr` 数量 |
