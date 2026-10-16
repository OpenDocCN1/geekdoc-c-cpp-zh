
The first `static_assert` checks if the standard string is `Ordered` (it is, because it provides `==`, `!=`, and `<`). The second checks if our `String` is `Ordered` (it is not, because I “forgot” to define `<`). Using such a global check will perform the constraints check independently of whether we actually use that particular specialization of a template in the program. Depending on our aims, that can be an advantage or a bother. Such a check forces type checking to be done at a specific point in the program; that is usually good for error isolation. Also, such checks can help unit testing. However, for programs using a number of libraries, explicit checks quickly become unmanageable.

Being `Regular` is an ideal for a type. We can copy objects of regular types, put them into `vector`s and arrays, compare them, etc. If a type is `Ordered`, we can also use its objects in sets, sort sequences of such objects, etc. So, we go back and improve our `String` to make it `Ordered`. In particular, we add `<` to provide a lexicographical ordering:

```
template<typename C>
bool operator<(const String<C>& s1, const String<C>& s2)
{
static_assert(Ordered<C>(),"String’s character type not ordered"); bool eq = true;
for (int i=0; i!=s1.size() && i!=s2.size(); ++i) {
if (s2[i]<s1[i]) return false;
if (s1[i]<s2[i]) eq = false; // not s1==s2 }
if (s2.size()<s1.size()) return false; // s2 is shorter than s1
if (s1.size()==s2.size() && eq) return false; // s1==s2
return true;
```

# 24.4.1 Axioms

As in mathematics, an axiom is something we can’t prove. It is something we assume to be true. In the context of requirements for template arguments, we use “axiom” in that sense to refer to semantic properties. We use an axiom to state what a class or an algorithm assumes about its set of inputs. An axiom, however expressed, represents an algorithm’s or class’s expectations of (assumptions about) its arguments. We cannot in general test to see whether an axiom holds for values of a type (that is one reason we refer to them as axioms). Furthermore, an axiom is only required to hold for the values actually used by an algorithm. For example, an algorithm can carefully avoid dereferencing null pointers or copying a floating-point `NaN`. If so, it could have axioms that require pointers to be dereferenceable and floating-point values to be copyable. Alternatively, axioms can be written with the general assumption that singular values (e.g., `NaN` and `nullptr`) violate some precondition, so that they need not be considered.

C++ does not (currently) have any way of expressing axioms, but as for concepts, we can make our idea of a concept a bit more concrete than a comment or some text in a design document.

Consider how we might express some of the key semantic requirements for a type to be regular:

```
template<typename T>
bool Copy_equality(T x) // semantics of copyconstruction
{
return T{x}==x; // acopycompares equal to what it is a copyof }

template<typename T>
bool Copy_assign_equality(T x, T& y) // semantics of assignment {
return (y=x, y==x); // the result of an assignment compares equal to the source of the assignment }
```

In other words, copy operations make copies.

```
template<typename T>
bool Move_effect(T x, T& y) // semantics of move
{
return (x==y ? T{std::move(x)}==y : true) && can_destroy(y); }

template<typename T>
bool Move_assign_effect(T x, T& y, T& z) // semantics of moveassignment {
return (y==z ? (x=std::move(y), x==z)) : true) && can_destroy(y);
}
```

In other words, a move operation yields a value that compares equal to whatever the source of the move operation compared equal to, and the source of the move can be destroyed.

These axioms are represented as executable code. We might use them for testing, but most importantly, we have to think harder to express them than we would have to simply write a comment. The resulting axioms are more precisely stated than would have been the case in “ordinary English.” Basically, we can express such pseudo axioms using first-order predicate logic.

# 24.4.2 Multi-argument Concepts

When looking at a single-argument concept and applying it to a type, it looks very much as if we are doing conventional type checking and that the concept is the type of a type. That’s part of the story, but only a part. Often, we find that relationships among argument types are essential for correct specification and use. Consider the standard-library `find()` algorithm:

```
template<typename Iter, typename Val>
Iter find(Iter b, Iter e, Val x);
```

The `Iter` template argument must be an input iterator, and we can (relatively) easily define a constraints-check template for that concept.

So far, so good, but `find()` depends critically on comparing `x` to elements of the sequence `[b:e)`. We need to specify that comparison is required; that is, we need to state that `Val` and and the value type of the input iterator are equality comparable. That requires a two-argument version of `Equality_comparable`:

```
template<typename A, typename B>
constexpr bool Equality_comparable(A a, B b)
{
return Common<T, U>()
&& Totally_ordered<T>()
&& Totally_ordered<U>()
&& Totally_ordered<Common_type<T,U>>()
&& Has_less<T,U>() && Boolean<Less_result<T,U>>()
&& Has_less<U,T>() && Boolean<Less_result<U,T>>()
&& Has_greater<T,U>() && Boolean<Greater_result<T,U>>()
&& Has_greater<U,T>() && Boolean<Greater_result<U,T>>()
&& Has_less_equal<T,U>() && Boolean<Less_equal_result<T,U>>()
&& Has_less_equal<U,T>() && Boolean<Less_equal_result<U,T>>()
&& Has_greater_equal<T,U>() && Boolean<Greater_equal_result<T,U>>() &&
Has_greater_equal<U,T>() && Boolean<Greater_equal_result<U,T>>();
```

这对于一个简单的概念来说显得相当冗长。然而，我希望对所有运算符以及它们使用的对称性做出明确说明，而不是将复杂性隐藏在概括之中。

在此基础上，我们可以定义 `find()`：

```
template<typename Iter, typename Val>
Iter find(Iter b, Iter e, Val x)
{
static_assert(Input_iterator<Iter>(), "find() requires an input iterator");
static_assert(Equality_comparable<Value_type<Iter>,Val>(), "find()'s iterator and value arguments must match");
while (b!=e) {
if (*b==x) return b; ++b;
}
return b;
```

多参数概念在指定通用算法时特别常见且有用。这也是你会发现概念数量最多、并且需要指定新概念的地方最多（而不是从常用概念的目录中挑选“标准”概念）。众所周知类型的变化似乎比算法对其参数的要求变化更有限。

# 24.4.3 Value Concepts

概念可以表达对一组模板参数的任意（语法）要求。特别是，模板参数可以是整数值，因此概念可以接受整数参数。例如，我们可以编写一个约束检查来测试值模板参数是否很小：

```
template<int N>
constexpr bool Small_size()
{
return N<=8;
}
```

一个更现实的例子是概念中数值参数只是其中之一。例如：

```
constexpr int stack_limit = 2048;
template<typename T,int N>
constexpr bool Stackable() // T is regular and N elements of T can fit on a small stack {
return Regular<T>() && sizeof(T)*N<=stack_limit;
```

这实现了“小到可以栈分配”的概念。它可能像这样使用：

```
template<typename T, int N>
struct Buffer {
//...
};
template<typename T, int N> void fct()
{
static_assert(Stackable<T,N>(),"fct() buffer won’t fit on stack");
Buffer<T,N> buf;
//...
}
```

Compared to the fundamental concepts for types, value concepts tend to be small and ad hoc.

# 24.4.4 Constraints Checks

本书中使用的约束检查可以在本书的支持网站上找到。它们不是标准的一部分，我希望将来它们会被适当的语言机制取代。然而，它们对于思考模板和类型设计很有用，并反映了标准库中 de facto 的概念。它们应放在单独的命名空间中，以避免干扰可能的未来语言特性和概念思想的替代实现。我使用命名空间 `Estd`，但那可能是一个别名（§14.4.2）。以下是你可能会觉得有用的几个约束检查：

- `Input_iterator<X>`: `X` 是一个迭代器，我们只能使用一次来遍历序列（使用 `++` 向前），每个元素只读取一次。

- `Output_iterator<X>`: `X` 是一个迭代器，我们只能使用一次来遍历序列（使用 `++` 向前），每个元素只写入一次。

- `Forward_iterator<X>`: `X` 是一个迭代器，我们可以使用它来遍历序列（使用 `++` 向前）。这就是单链表（例如 `forward_list`）自然支持的。

- `Bidirectional_iterator<X>`: `X` 是一个迭代器，我们可以向前（使用 `++`）和向后（使用`--`）移动。这就是双向链表（例如 `list`）自然支持的。

- `Random_access_iterator<X>`: `X` 是一个迭代器，我们可以使用它来遍历序列（向前和向后）并使用下标随机访问元素，以及使用 `+=` 和 `-=` 进行定位。这就是数组自然支持的。

- `Equality_comparable<X,Y>`: 一个 `X` 可以使用 `==` 和 `!=` 与一个 `Y` 进行比较。

- `Totally_ordered<X,Y>`: `X` 和 `Y` 是 `Equality_comparable`，并且一个 `X` 可以使用 `<`, `<=`, `>` 和 `>=` 与一个 `Y` 进行比较。

- `Semiregular<X>`: `X` 可以被复制、默认构造、在自由存储上分配，并且没有烦人的次要技术限制。
