
// uncheckedelement access // add c at end
// for the short string optimization

模板<typename C> 前缀指定正在声明一个模板，并且类型参数 C 将在声明中使用。引入之后，C 就像其他类型名一样使用。C 的作用域延伸到以 template<typename C> 为前缀的声明的末尾。你可能更喜欢更短且等价的形式 template<class C>。在任何一种情况下，C 都是一个类型名；它不必是类的名字。数学家会把 template<typename C> 认作传统“对所有 C” 的变体，更具体地说就是“对所有类型 C” 或甚至“对所有 C，使得 C 是一个类型”。如果你按这种思路思考，你会注意到 C++ 缺乏一个完全通用的机制来指定模板参数 C 的所需属性。也就是说，我们不能说“对所有 C，使得 ...” 其中“...” 是 C 的一组需求。换句话说，C++ 没有直接的方式来说明模板参数 C 应该是什么类型的 (§24.3)。

类模板的名字后跟一个被 <> 括起来的类型，是由模板定义的类的名字，可以像其他类名一样使用。例如：

```
String<char> cs;
String<unsigned char> us;
String<wchar_t> ws;
struct Jchar { /*...*/ }; // Japanese character
```

```
String<Jchar> js;
```

## Section 23.2 A Simple String Template

除了其名字的特殊语法外，String<char> 的工作方式就好像它是用 §19.3 中 String 类的定义定义的。把 String 做成模板允许我们为 char 的 String 提供的设施也提供给任何种类字符的 String。例如，如果我们使用标准库的 map 和 String 模板，那么 §19.2.1 中的词计数示例就变成：

```
int main() // count the occurrences of each word on input
{
map<String<char>,int> m;
for (String<char> buf; cin>>buf;)
++m[buf];
// ... write out result ...
}
```

对于我们的日文字符类型 Jchar 的版本是：

```
int main() // count the occurrences of each word on input {
map<String<Jchar>,int> m;
for (String<Jchar> buf; cin>>buf;)
++m[buf];
// ... write out result ...
}
```

标准库提供了模板类 **basic_string**，它与模板化的 **String** 类似 (§19.3, §36.3)。在标准库中，**string** 是 **basic_string<char>** 的同义词 (§36.3)： **using string = std::basic_string<char>;**
这使我们能够像这样编写词计数程序：

```
int main() // count the occurrences of each word on input
{
map<string,int> m;
for (string buf; cin>>buf;)
++m[buf];
// ... write out result ...
}
```

通常，类型别名 (§6.5) 对于缩短由模板生成的类的长名字很有用。此外，我们通常不希望知道类型的定义细节，而别名允许我们隐藏一个类型是由模板生成的这一事实。

### 23.2.1 Defining a Template

由类模板生成的类是一个完全普通的类。因此，使用模板并不意味着除了等价的“手写”类所使用的之外还有任何运行期机制。事实上，使用模板可以导致生成的代码减少，因为类模板的成员函数代码只有在该成员被使用时才会被生成 (§26.2.1)。

除了类模板之外，C++ 还提供函数模板 (§3.4.2, §23.5)。我将在类模板的上下文中介绍模板的大部分“机制”，并将函数模板的详细讨论推迟到 §23.5。模板是给定合适的模板参数如何生成某物的规范；进行该生成的语言机制（实例化 (§26.2) 和特化 (§25.3)）并不关心是生成类还是函数。因此，除非另有说明，模板的规则同样适用于类模板和函数模板。模板也可以作为别名定义 (§23.6)，但其他合理的构造，例如命名空间模板，并未提供。

有些人会在术语 *class template* 和 *template class* 之间做语义区分；我不这么做；那太微妙了：请把这两个术语视为可互换的。同样，我把 *function template* 视为与 *template function* 可互换。

在设计类模板时，通常先调试一个特定的类，例如 **String**，然后再把它变成像 **String<C>** 这样的模板是明智的。通过这样做，我们在具体示例的上下文中处理了许多设计问题和大部分代码错误。这种调试对所有程序员都很熟悉，大多数人在处理具体示例时比处理抽象概念更好。之后，我们可以在不被更常规错误分散注意力的情况下处理可能出现的泛化问题。同样，在尝试理解一个模板时，想象它对某个特定类型参数例如 **char** 的行为，然后再尝试理解模板的全部一般性，通常是有用的。这也符合这样一种哲学：通用组件应作为一个或多个具体示例的泛化来开发，而不是仅仅从第一性原理设计 (§24.2)。

类模板的成员以与非模板类相同的方式声明和定义。模板成员不必在模板类本身内定义。在这种情况下，其定义必须在别处提供，就像非模板类成员一样 (§16.2.1)。模板类的成员本身就是以其模板类的参数为参数的模板。当这样的成员在类外定义时，必须显式声明为模板。例如：

```
template<typename C>
String<C>::String() // String<C>’s constructor
  :sz{0}, ptr{ch}
{
  ch[0] = {}; // terminating 0 of the appropriate character type }

template<typename C>
String& String<C>::operator+=(C c) {
  // ... add c to the end of this string ...
  return *this;
}
```

模板参数，例如 C，是一个参数而不是特定类型的名字。然而，这并不影响我们使用该名字编写模板代码的方式。在 String<C> 的作用域内，对模板本身的名字使用 <C> 限定是多余的，因此 String<C>::String 是构造函数的名称。

正如程序中只能有一个函数定义类的成员函数一样，程序中也只能有一个函数模板定义类模板的成员函数。然而，特化 (§25.3) 使我们能够为特定的模板参数提供替代实现。对于函数，我们还可以使用重载来为不同参数类型提供不同的定义 (§23.5.3)。

## Section 23.2.1 Defining a Template

类模板名不能被重载，因此如果一个类模板在一个作用域中被声明，就不能在该作用域中用相同名字声明其他实体。例如：

```
template<typename T>
class String { /* ... */ };

class String { /* ... */ }; // error: double definition
```

用作模板参数的类型必须提供模板期望的接口。例如，用作 String 参数的类型必须提供通常的拷贝操作 (§17.5, §36.2.2)。请注意，不同参数对于同一个模板参数不必通过继承相关。另见 §25.2.1（模板类型参数）、§23.5.2（模板参数推导）和 §24.3（模板参数的要求）。

### 23.2.2 Template Instantiation

可能是一个主要问题，我们需要设计程序以最小化其后果。

模板机制的根本弱点是无法直接表达对模板参数的要求。例如，我们不能说：

```
template<Container Cont, typename Elem>
requires Equal_comparable<Cont::value_type,Elem>()
int find_index(Cont& c, Elem e);
```

*// requirements for types Cont and Elem // find the index of e in c*

也就是说，我们在 C++ 本身中没有直接说 **Cont** 应该是一个可以充当容器的类型，并且类型 **Elem** 应该是一个允许我们将值与 **Cont** 的元素进行比较的类型的方法。正在进行工作以使这在未来版本的 C++ 中成为可能（在不损失灵活性、不损失运行期性能且不显著增加编译时间的情况下 [Sutton,2011]），但现在我们不得不没有。

处理与模板参数传递相关问题的第一步是建立一个框架和词汇来讨论需求。把对模板参数的一组需求看作一个谓词。例如，我们可以把“**C** 必须是一个容器”看作一个谓词，它接受一个类型 **C** 作为参数，如果 C 是一个容器（按我们定义的方式），则返回 **true**，如果不是则返回 **false**。例如，**Container<vector<int>>()** 和 **Container<list<string>>()** 应该是 true，而 **Container<int>()** 和 **Container<shared_ptr<string>>()** 应该是 false。我们称这种谓词为 *concept*。概念目前还不是 C++ 中的语言构造；它是我们用来推理模板参数要求、在注释中使用以及有时用我们的代码支持的概念 (§24.3)。

首先，把概念看作设计工具：将 **Container<T>()** 指定为一组注释，说明类型 **T** 必须具有哪些属性才能使 **Container<T>()** 为真。例如：

- **T** 必须有一个下标运算符 (`[]`)。
- **T** 必须有一个 `size()` 成员函数。
- **T** 必须有一个成员类型 **value_type**，它是其元素的类型。

请注意，这个列表是不完整的（例如，`[]` 以什么作为参数并返回什么？）并且未能解决大多数语义问题（例如，`[]` 实际上做什么？）。然而，即使是一部分需求也可能有用；即使非常简单也允许我们手工检查我们的使用

## Section 23.3 Type Checking

并捕获明显的错误。例如，**Container<int>()** 显然为假，因为 **int** 没有下标运算符。我将回到概念的设计 (§24.3)，考虑在代码中支持概念的技术 (§24.4)，并给出一个有用的概念集的示例 (§24.3.2)。现在，只需注意 C++ 不直接支持概念，但这并不意味着概念不存在：对于每一个工作的模板，设计者对其参数都有一些概念在心里。Dennis Ritchie 著名地说过，“C 是一种强类型、弱检查的语言。” 你可以对 C++ 的模板说同样的话，只是模板参数要求（概念）的检查实际上是完成的，但它
