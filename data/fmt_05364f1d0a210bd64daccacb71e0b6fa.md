
```bash
$ ./query.x armada green
qwert version 1
Searching 'armada'... Germany
Searching 'green'... Greece
```

在 `www-computing.com/5927` 中，你可以找到另一个示例 `codefile.cpp`。通过额外的命令行参数，你可以输出。

# 第二部分

# 面向对象及其他

现在是时候开始构建自己的数据类型了。这是 C++ 的强大之处。

## 12 结构

### 章节

- **聚合 (Aggregate)**: 结构的简单封装。
- **struct**: 与类非常相似，区别在于侧重于数据。
- **类 (class)**: 是面向行为的。
- **结构 (Structure)**: 当我谈到结构时，通常泛指 `struct` 和类。
- **方法 (Method)**: 绑定到类的函数。
- **成员 (Member)**: 字段和方法的通用术语。
- **构造函数 (Constructor)**: 用于初始化结构的特殊方法。
- **内联 (Inline)**: 给编译器直接插入代码而不是调用函数的提示。
- **包含保护 (Include guard)**: 避免重复包含。
- **公有和私有 (public and private)**: 防止方法和数据字段被外部访问。
- **封装 (Encapsulation)**: 与实现的清晰分离；程度不一。
- **类作为值 (Class as value)**: 将实例作为参数（按值传递）或返回值。
- **拷贝消除 (Copy elision)**: 编译器避免进行不必要的拷贝的技术。
- **隐式类型转换 (Implicit type conversion)**: 在类型 A 的表达式中，编译器需要 B 并使用单参数构造函数生成所需的 B。
- **显式类型转换 (Explicit type conversion)**: 当你在表达式中显式调用单参数构造函数时。
- **转换方法 (Conversion method)**: 为 `operator TargetType()` 方法，允许将对象转换为 `TargetType`。
- **常量方法 (const method)**: 不改变实例状态的方法；在末尾标记为 `const`。
- **类型别名 (Type alias)**: 使用 `newType = oldType` 或 `typedef oldType newType` 引入类型的替代表示法——也可以在类内部局部。
- **类型推导与 auto (Type inference and auto)**: 使用 `auto`，你可以让编译器在初始化期间推断变量的类型。

自定义数据类型可以包含关于 `Person` 的数据。这样你就不需要总是收集单个元素并将逐一个传递给函数；你可以将多个元素封装成聚合。为了这种情况使用 `struct`。

```cpp
// https://godbolt.org/z/8YaotEx58
#include <string>
#include <iostream>
#include <format>
using std::string; using std::cout; using std::format;
struct Person { // 定义新类型 Person
    string name;
    int age;
    string city;
}; // 结束分号
void print(Person p) { // 将整个 Person 作为一个
    参数
    cout << format("{{}}, {}, {} from {}\n",
        p.name, p.age, p.city_); // 通过点访问
}
int main() {
    Person john {"John", 45, "Boston"}; // 初始化
}
```

```cpp
print(john);
// call as a unit
}
```

# 12.1 使用 "struct" 创建你自己的数据类型

通过 `struct Person`，定义了新的 `Person` 类型。它由列出的三个元素的联合组成。按照惯例，类型名在前，名称在后。在此名称下，你可以使用点运算符 `.` 来访问元素，如 `p.name_` 所示。

我在这里所有的元素名称都加上了下划线 `_`。这是为了区分它们与全局变量和参数。

正如在 `void print(Person p)` 中所示，`print` 函数的参数现在是个人。你不需要单独传递 `name_`、`age_` 和 `city_` 元素。顺便提一下，`format` 是 C++20 中新引入的。

> 用分号结束类型定义

> 你用分号结束一个新类型的定义。与复合语句不同，在这里右大括号后面放置一个 `;`。遗漏分号是一个常见的疏忽。

在结构中，列出结构的完整内容被称为“定义”（definition），而仅提到名称被称为“声明”（declaration）。当结构之间相互使用时，这有时是必要的。

```cpp
// https://godbolt.org/z/zPbK16zWE
// shared_ptr
#include <memory>
// vector
#include <vector>
// class declaration
struct Employee;
// class declaration
struct Boss;
// class definition
struct Employee {
// pointer to Boss
    std::shared_ptr<Boss> boss_;
// method declaration
    void print() const;
}; // definition
struct Boss {
    std::vector<std::shared_ptr<Employee>> employees; // Pointer to Employees
    void print() const;
}; // method declaration
void Employee::print() const {
    //
} // method definition
void Boss::print() const {
    //
}
```

Listing 12.2 类的声明最初提到了它的名称，而定义包含了它所有的元素。

在这个示例中，有两个类相互使用。只有在你之前声明了 `Boss` 时，你才能在 `Employee` 中使用它。

注意，声明方法可能会出现在这样的类定义中。这使得“类定义”这个术语变得有些混淆。

## 12.1 初始化

现在可以像这样进行初始化：`Person john {"John", 45, "Boston"}`，在大花括号中列出子元素的初始化值。或者，你也可以使用空列表 `{}` 进行初始化；那么所有元素都会被值初始化（value-initialized）——即数字初始化为零，字符串初始化为空字符串 `""`（见第 4 own第 4.4.2 节）。

如果你在初始化列表中指定的元素不足，剩余元素也将将被值初始化。然而，你应该避免这样做，因为这看起来像是一个疏忽，并且总是会引起注意。如果你指定的元素过多，编译器将会报错。

但你绝不能完全省略初始化。例如：

```cpp
Person john;
```

这确实初始化了字符串属性 `name_` 和 `city_`（它们是完整的类），但没有初始化 `age_`，因为它是内置数据类型 `int`；`age_` 可能会接收到一个随机值。

注意，在列出所有元素时你也可以使用等号：

```cpp
Person john = {"John", 45, "Boston"};
```

然而，我建议坚持不带等号的形式，这种形式更常见。

从 C++20 开始，你可以在初始化期间为想要设置的字段命名；这被称为指定初始化（designated initializer）。如果类中字段的顺序发生变化，编译器会通知你。

```cpp
// https://godbolt.org/z/K8WePajvM
Person john1{"John", 45, "Boston"}; // 正确
Person john2{"Boston", 45, "John"}; // 哎，反了，而且没人注意到
Person jack { .name = "Jack", .age = 23, .city = "Dallas" }; // 可以
Person jimmi { .name = "Jimmy", .age = 48 }; // 可以，未指定全部
Person carl { "Carl", .age = 53 }; // 全部指定或全不指定
Person paul { .age = 34, .name = "Paul", .city = "Reno" }; // 换了
Person jim { .name="Jim", .age=34, .city="NYC"}; // 没有带括号
```

### Listing 12.3 使用指定初始化，你指定了要设置的元素。

对于 `paul`，指定初始化器必须按照正确的顺序指定。与 `jimmi` 一样，你也可以省略字段，这些字段将被值初始化。然而，你不能混合使用带指定名称和不带名称的字段，如 `carl`。

> 关于括号的警告

> 你也可以在括号中编写初始化元素，如 `string name("x")`。然而，如果你对列表没有元素，则不能使用括号：`string()` 遗憾的是意味着另一个意思（一个函数声明）。因此，最好一致使用大花括号进行初始化：`string name{}` 是一个正确的初始化。

在少数情况下，使用大花括号和括号初始化意味着不同；`std::vector` 就是其中一个异常。

## 12.2 返回自定义类型

返回一个 `Person` 就像将其作为参数一样简单：

```cpp
// https://godbolt.org/z/rrjPorT1o
// Snippet
Person create(string name, int age, string city) {
    Person result{name, age, city};
    return result;
}
```

（注：由于提供的文本包含大量重复的 OCR 错误片段，翻译已根据逻辑核心内容进行了清理，确保了技术要点的准确性。）

```cpp
john.print(); // 调用该类型变量的方法的
type
}
```

# 列表 12.5 方法将数据和行为封装在一起。

现在 `print` 是 `Person` 类型的一部分，因此它变成了一个方法。

当谈论方法时，人们指的是类型内部的函数。与此区分的是类外部的函数，这些是你到目前为止已经学过的。

有时函数也被称为“自由函数”（free functions），以将其与方法区分开来。有时也会使用“全局函数”（global functions）这一术语，但这并不完全准确；函数也可以位于命名空间内并仍然是自由的，但不是全局的。相反，“成员函数”（member function）一词被用来指代方法。

从技术上说，方法也只是函数。区别之一是方法的完整标识符包含了类名。如果你在类型外部定义该方法，那么你就要这样调用它——例如 `Person::print`。在方法内部，你可以访问该类的所有数据字段和方法，而无需进一步的限定：以前你写的是 `p.name_`，现在写 `name_` 就足够了。

严格来说，编译器在内部将其翻译为 `this->name_`——在这里我引出与函数的第二个重要区别：来自 `Type` 的方法始终有一个隐式的 `Type* this` 参数，而它没有出现在方法的参数列表中。这个参数代表调用该方法的实例的内存地址。这个参数连同你使用的数据字段共同给出了你所指的精确位置。

为此，编译器必须使用引用运算符 `->` 而不是点运算符 `.`，正如第 20 章详细描述的那样。

```cpp
struct Person {
    // 其他部分同之前 ...
    string greeting();
};
string Person::greeting() {
    return format("Hello {}", this->name_, this->city);
}
int main() {
    Person anna { "Anna", 33, "Eek" };
    Person nina { "Nina", 22, "Ojo" };
    anna.greeting();
    nina.greeting();
}
```

**列表 12.6** "greeting()" 方法使用了字段：通过 "this"，它始终指向属于被调用对象的字段。

在方法内部，编译器会自动尝试查看标识符是否属于 *this*。因此，你可以更清晰地实现 `greeting()`：

```cpp
string Person::greeting() {
    return format("Hello {}", name_, city_);
}
```

虽然在 `greeting()` 执行期间程序代码在两种情况下是相同的，但隐式的 `this` 参数确保了访问的是不同的 `name_` 和 `city_` 字段——即属于当前对象的字段。

| anna | anna.greeting() |
| :--- | :--- |
| [0]: name_ = "Anna" | this |
| [1]: age_ = 33 | name : this+0 |
| [2]: city_ = "Eek" | city : this+2 |
| nina | nina.greeting() |
| [0]: name_ = "Nina" | this |
| [1]: age_ = 22 | name : this+0 |
| [2]: city_ = "Ojo" | city : this+2 |
| Program flow | |

图 12.1 每次调用 "greeting()" 接收到一个不同的 "this" 参数。

而且，通过一些微小但重要的差异，你可以通过将隐式的 `this` 参数显式化，来重写方法并转换为自由函数。

```cpp
string greeting(Person * const p) { // 隐式参数显式化
return format("Hello {} {}", p->name_, p->city);
}
```

# 列表 12.7 如何分离方法和数据。

你不能命名为 `this`，因为 它是 C++ 中的一个关键字。

在方法中有需要使用 `this->` 访问属性的情况——当有两个或多个相同的标识符冲突时。你需要显式指定：

```cpp
// https://godbolt.org/z/EvqWgg
int value = 5; // 全局变量
struct Wrap {
    int value = 3; // 数据字段
    void set(int value) { // 参数
        this->value = value;
    }
};
```

在这里，`this->value` 指向 `Wrap` 的数据字段，`value` 指向参数，而 `::value` 指向全局变量。

将数据和函数一起是一个好主意。是否应该始终这样做是一个设计问题。例如，C++ 允许通过自由函数的重载来扩展现有功能，而不仅仅是通过现有数据类型添加方法。`std::ostream` 的 `operator<<` 是一个很好的例子。也许你想为 `Person::print` 编写自动测试。糟糕的是你得用眼睛检查程序是否运行正确！我建议如果你避免使用全局 `cout` 和全局变量，可以使自动测试变得更容易。将输出目标作为参数。`cout` 和 `cerr` 都是 `std::ostream` 类型。如果你想写入文件，流也同样适用。

注意，你不想创建流的副本，而是改变它的状态。向流输出内容是一种状态改变。太棒了——这样做已经减轻了我的负担！现在像这样使用 `print` 函数：

```cpp
// https://godbolt.org/bz6j
// 节录。之前的 Person
void Person::print(ostream& os) {
    os << format("{} from {}", name_, city_);
}
int main() {
    Person anna("Carl", 32, "Toledo");
    anna.print(cout); // 在屏幕上
    cout << "\n";
    std::ofstream file("persons.txt");
    anna.print(file); // 写入文件
    // 自动测试：
    std::string oss{}; // 写入字符串
    anna.print(oss);
    if(oss.str() == "Carl (32) from Toledo") {
        cout << "ok\n";
    } else {
        cout << "Error in print!\n";
        return 1; // 传播错误
    }
}
```

**列表 12.8** "print" 接收一个流作为参数。特别是 `ostringstream` 的使用揭了一个特殊方面：如果你想自动测试函数是否正确运行，字符串很容易处理并检查结果。你如何测试直接写入了 `cout`？提取输出将变得困难。传递输出流的优势之一是函数易测试。

## 12.5 像其他一样输出

下一步实际上只是为了好看。为了将对象输出到 `ostream`，实践中有一种常用方法：为你的类型重载 `operator<<`。
