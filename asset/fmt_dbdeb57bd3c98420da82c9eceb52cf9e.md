
# 24.3.2 Concepts and Constraints

A concept is not an arbitrary collection of properties. Most lists of properties of a type (or

一组类型）并不能定义一个连贯且有用的概念。一个需求列表若要作为概念有用，就必须反映一组算法或一个模板类的一组操作的需求。在许多领域中，人们设计或发现了描述该领域基本概念的概念（C++ 中“concept”一词的技术用法正是考虑到这一常见用法而选定的）。有意义的概念似乎出奇地少。例如，代数建立在幺半群、域和环等概念之上，而 STL 则依赖前向迭代器、双向迭代器和随机访问迭代器等概念。在一个领域中发现新概念是一项重大成就；这不是你应当期望每年都能做到的事情。大多数情况下，你通过研读某个研究领域或应用领域的基础文献来发现概念。本书使用的一组概念将在 §24.4.4 中描述。

“概念”是一个非常普遍的想法，本质上与模板没有任何关系。即使是 `K&R C [Kernighan,1978]` 也有概念，例如有符号整型就是该语言对内存中整数概念的一种概括。我们对模板实参的需求就是概念（无论以何种方式表达），因此大多数与概念相关的有趣问题都出现在模板语境中。

我将概念视为一种精心构造的实体，它反映了应用领域的基本属性。因此，概念应该只有少数几个，并且可以作为算法和类型设计的指南。类比物理插头和插座：我们希望数量最少，以简化生活并降低设计和构建成本。这一理想可能会与每个泛型算法（§24.2）和每个参数化类追求最小需求的想法相冲突。此外，这一理想还可能与本应为类提供绝对最小接口（§16.2.3）的想法相冲突，甚至与某些程序员认为自己有权“完全按自己喜欢的方式”编写代码的想法相冲突。然而，没有努力和某种形式的标准，我们无法获得插头兼容性。

我把成为概念的标准定得很高：我要求通用性、一定的稳定性、跨许多算法的可用性、语义一致性，等等。事实上，许多我们希望用于模板实参的简单约束，按照我的标准并不能算作概念。我认为这是不可避免的。特别是，我们编写了许多并不反映通用算法或广泛适用类型的模板。相反，它们是实现细节，其实参只需反映某个模板的必需细节，而该模板只打算在某个东西的某一次实现中单独使用。我将此类模板实参的需求称为约束，或者（如果你愿意）称为特设概念。看待约束的一种方式是，将它们视为接口的不完整（部分）规范。通常，部分规范可能很有用，而且远比没有规范好。

例如，考虑一个用于实验平衡二叉树平衡策略的库。该树将 `Balancer` 作为模板实参：

```
template<typename Node, typename Balancer>
struct node_base { // base of balanced tree
// ...
}
```

`Balancer` 只是一个对节点提供三种操作的类。例如：

```
struct Red_black_balance {
// ...
template<typename Node> static void add_fixup(Node* x);
template<typename Node> static void touch(Node* x);
template<typename Node> static void detach(Node* x);
};
```

显然，我们想说明对 `node_base` 实参的要求，但 `Balancer` 并不旨在成为广泛使用且易于理解的接口；它只打算用作平衡树特定实现的一个细节。这种 balancer 的想法（我犹豫是否使用“概念”一词）不太可能被用于其他地方，甚至不太可能在平衡树实现的大规模重写中原样保留。很难准确界定 balancer 的语义。首先，`Balancer` 的语义将严重依赖于 `Node` 的语义。在这些方面，`Balancer` 不同于真正的概念，例如 `Random_access_iterator`。不过，我们仍然可以将 balancer 的最小规范——“对节点提供这三个函数”——用作 `node_base` 实参的一个约束。

请注意，“语义”一词在概念讨论中反复出现。我发现，在判断某个东西是一个概念，还是仅仅是对某个类型（或一组类型）的特设约束集合时，“我能否写出一种半形式化的语义？”这个问题最有帮助。如果我能写出有意义的语义规范，那我就拥有一个概念。如果不能，我所拥有的只是一个约束；它可能有用，但不应指望它稳定或广泛有用。

# 24.4 使概念具体化

遗憾的是，C++ 没有专门的语言设施来直接表达概念。然而，仅将“概念”作为一种设计观念，并以注释形式非正式地呈现，并不理想。首先，编译器不理解注释，因此仅以注释表达的需求必须由程序员检查，无法帮助编译器提供良好的错误信息。经验表明，即使没有直接的语言支持就无法完美地表示概念，我们仍然可以使用对模板实参属性执行编译期检查的代码来近似地实现概念。

概念是一个谓词；也就是说，我们将概念视为一个编译期函数，它查看一组模板实参，如果它们满足概念的要求则返回 `true`，否则返回 `false`。因此，我们将概念实现为 `constexpr` 函数。在这里，我将使用术语“约束检查”来指代对 `constexpr` 谓词的调用，该谓词针对一组类型和值检查某个概念。与真正的概念不同，约束检查不处理语义问题；它只检查关于语法属性的假设。

考虑我们的 `String`；它的字符类型实参应当是 `Ordered`：

```
template<typename C>
class String {
static_assert(Ordered<C>(), “String’s character type is not ordered”);
// ...
};
```

当 `String<X>` 以类型 `X` 实例化时，编译器将执行 `static_assert`。如果 `Ordered<X>()` 返回 `true`，则编译继续，并生成与没有该断言时完全相同的代码。否则，就会产生错误信息。

乍一看，作为权宜之计，这看起来相当合理。我更愿意这样写：

```
template<Ordered C>
class String {
// ...
};
```

然而，那是将来才能做到的事，所以让我们看看如何定义谓词 `Ordered<T>()`：

```
template<typename T>
constexpr bool Ordered()
{
return Regular<T>() && Totally_ordered<T>();
}
```

也就是说，如果某个类型既是 `Regular` 又是 `Totally_ordered`，那么它就是 `Ordered`。让我们“深入挖掘”一下，看看这意味着什么：

```
template<typename T>
constexpr bool Totally_ordered()
{
return Equality_comparable<T>() // has == and !=
&& Has_less<T>()&& Boolean<Less_result<T>>()
&& Has_greater<T>() && Boolean<Greater_result<T>>() && Has_less_equal<T>()
&& Boolean<Less_equal_result<T>>() && Has_greater_equal<T>() &&
Boolean<Greater_equal_result<T>>();
}
```

```
template<typename T>
constexpr bool Equality_comparable() {
return Has_equal<T>() && Boolean<Equal_result<T>>()
&& Has_not_equal<T>() && Boolean<Not_equal_result<T>>();
}
```

因此，如果类型 `T` 是 `regular`（规则类型），并提供通常的六种比较操作，那么它就是有序的。这些比较操作必须产生可以转换为 `bool` 的结果。比较运算符还应当具有其应有的数学含义。C++ 标准精确地规定了这一点（§31.2.2.1、§iso.25.4）。

`Has_equals` 是使用 `enable_if` 以及 §28.4.4 中描述的技术实现的。我将约束名称大写（例如 `Regular`），尽管这样做违反了我的“排版风格”。

style” of capitalizing type and template names, but not functions. However, concepts are even more fundamental than types, so I feel a need to emphasize them. I also keep them in a separate namespace (`Estd`) in the hope that very similar names will eventually become part of the language or the standard library.

Digging a bit further into the set of useful concepts, we can define `Regular`:

```
template<typename T> constexpr bool Regular() {
  return Semiregular<T>() && Equality_comparable<T>();
}
```

`Equality_comparable` gives us `==` and `!=`. `Semiregular` is the concept that express the notion of a type that doesn’t have unusual technical restrictions:

```
template<typename T>
constexpr bool Semiregular()
{
  return Destructible<T>()
    && Default_constructible<T>()
    && Move_constructible<T>()
    && Move_assignable<T>()
    && Copy_constructible<T>()
    && Copy_assignable<T>();
}
```

A `Semiregular` can be both moved and copied. That describes most types, but there are examples of types that cannot be copied, such as `unique_ptr`. However, I don’t know of useful types that can be copied but not moved. Types that can neither be moved nor copied, such as `type_info` (§22.5), are very rare and tend to reflect system properties.

We can also use constraints checks for functions; for example:

```
template<typename C>
ostream& operator<<(ostream& out, String<C>& s)
{
  static_assert(Streamable<C>(), “String’s character not streamable”);
  out << “'”;
  for (int i=0; i!=s.size(); ++i) cout << s[i];
  out << “'”;
}
```

The concept `Streamable` needed by `String`’s output operator `<<` requires its argument `C` to provide the output operator `<<`:

```
template<typename T>
constexpr bool Streamable()
{
  return Input_streamable<T>() && Output_streamable<T>();
}
```

That is, `Streamable` tests that we can use the standard stream I/O (§4.3, Chapter 38) for a type. Checking concepts through constraints-check templates has obvious weaknesses:

- Constraints checks are placed in definitions, but they really belong in declarations. That is,

- The checking of constraints occurs as part of the instantiation of the constraints-check template. Therefore, the checking may occur later than we would like. In particular, we would have preferred for a constraints check to be guaranteed to be done by the compiler at the point of the first call, but that is impossible without language changes.

- We can forget to insert a constraints check (especially for a function template).

- The compiler does not check that a template implementation uses only the properties specified in its concepts. Thus, a template implementation may pass the constraints check, yet still fail to type check.

- We do not specify semantic properties in a way that a compiler can understand (e.g., we use comments).

a concept is part of the interface to an abstraction, but a constraints check can be used only in its implementation.

Adding constraints checks makes the requirements on template arguments explicit, and if a constraints check is well designed, it leads to more comprehensible error messages. If we forget to insert constraints checks, we are back to the ordinary type checking of the code generated by template instantiation. That can be unfortunate, but it is not disastrous. These constraints checks are a technique for making checking of designs based on concepts more robust, rather than an integral part of the type system.

If we want to, we can place constraints checks almost anywhere. For example, to guarantee that a particular type is checked against a particular concept, we could place constraints checks in a namespace scope (e.g., the global scope). For example:

```
static_assert(Ordered<std::string>, "std::string is not Ordered"); // will succeed
static_assert(Ordered<String<char>>, "String<char> is not Ordered"); // will fail
```
