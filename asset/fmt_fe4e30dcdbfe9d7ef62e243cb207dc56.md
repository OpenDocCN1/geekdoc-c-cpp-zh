
# 15.9.2. Query_base 和 Query 类

我们将从定义 `Query_base` 类开始开始实现：

点击此处查看代码图片

```cpp
// 抽象类作为具体查询类型的基类；所有成员均为私有
class Query_base {
    friend class Query;
protected:
    using line_no = TextQuery::line_no; // 用于 eval 函数中
    virtual ~Query_base() = default;
private:
    // eval 返回匹配此 Query 的 QueryResult
    virtual QueryResult eval(const TextQuery&) const = 0;
    // rep 是查询的字符串表示
    virtual std::string rep() const = 0;
};
```

`eval` 和 `rep` 都是纯虚函数，这使得 `Query_base` 成为抽象类（[15.4, p. 610]）。由于我们不打算直接使用 `Query_base` 或其派生类，`Query_base` 没有公共成员。所有对 `Query_base` 的都将通过 `Query` 对象进行。我们授予 `Query` 类友元权限，因为 `Query` 的成员将调用 `Query_base` 中的虚函数。

受保护成员 `line_no` 将位于 `eval` 函数内部。同样，析构函数是受保护的，因为它被派生类中的析构函数（隐式）使用。

# Query 类

`Query` 类提供了对（隐藏的）`Query_base` 继承层次的接口。每个 `Query` 对象将持一个指向对应 `Query_base` 对象的 `shared_ptr`。由于 `Query` 是访问 `Query_base` 类的唯一接口，`Query` 必须定义它自己的 `eval` 和 `rep` 版本。

`Query` 构造函数接受一个字符串将创建一个新的 `WordQuery` 并将其 `shared_ptr` 绑定到新创建的对象上。`&`、`|` 和 `-` 运算符分别创建 `AndQuery`、`OrQuery` 和 `NotQuery` 对象。这些运算符将返回一个绑定到新生成对象的 `Query` 对象。为了支持这些运算符，`Query` 需要一个接受 `Query_base` 的 `shared_ptr` 的构造函数并存储给定的指针。我们将此构造函数为私有，因为我们不打算通用地使用 `Query_base` 对象。由于此构造函数是私有的，我们需要将运算符设为友元。

根据前面的设计，`Query` 类非常简单：

点击此处查看代码图片

```cpp
// 用于管理 Query_base 继承层次的接口类
class Query {
    // 这些运算符需要访问 shared_ptr 构造函数
    friend Query operator-(const Query&);
    friend Query operator|(const Query&, const Query&);
    friend Query operator*(const Query&, const Query&);
public:
    Query(const std::string&); // 构建一个新的 WordQuery
    // 接口函数，调用相应的 Query_base 操作
```

# 《C++ Primer》第五版

```cpp
QueryResult eval(const TextQuery &t) const
{ return q->eval(t); }
std::string rep() const { return q->rep(); }
private:
    Query(std::shared_ptr<Query_base> query) : q(query) {}
    std::shared_ptr<Query_base> q;
```

我们首先将创建 `Query` 对象的运算符设为友元。这些运算符需要成为友元以便使用 `private` 构造函数。

在 `Query` 的 `public` 接口中，我们声明了但无法定义接受 `string` 的构造函数。该构造函数创建一个 `WordQuery`。

# 查询运算符

输出运算符是说明系统如何工作的一个良好示例：

```cpp
std::ostream & operator<<(std::ostream &os, const Query &q) {
    return os << q.rep();
}
```

# 15.9.3. 派生类

派自 `Query_base` 的类中最有趣的部分是它们是如何被表示的。`WordQuery` 类最直接。它的任务是持有搜索单词。

其他类作用于一个或两个操作数。`NotQuery` 有一个操作数，`AndQuery` 和 `OrQuery` 有两个。在这些类中，操作数可以是任何具体类。为了允许这种灵活性，操作数必须以指针形式存储。现在我们知道了这些类的设计，就可以实现它们了。

# WordQuery 类

`WordQuery` 查找给定字符串。它是唯一一个对给定 `TextQuery` 对象执行查询的操作：

点击此处查看图片

```cpp
class WordQuery: public Query_base {
    friend class Query; // 使用 WordQuery 构造函数
    WordQuery(const std::string &s) : query_word(s) { }
    // 具体类：WordQuery 定义了所有继承的虚函数
    QueryResult eval(const TextQuery& t) const {
        return t.query(query_word); }
    std::string rep() const { return query_word; }
    std::string query_word; // 要搜索的单词
};
```

像 `Query_base` 一样，`WordQuery` 没有公共成员；`WordQuery` 必须创建一个友元以便允许 `Query` 访问 `WordQuery` 构造函数。

每个具体查询类都必须定义继承的虚函数 `eval` 和 `rep`。我们在 `WordQuery` 类体内部定义了这两个操作：`eval` 调用其给定 `TextQuery` 参数的 `query` 成员，在文件中执行搜索；`rep` 返回 `WordQuery` 表示的字符串。

# C++ Primer，第五版

在定义了 `WordQuery` 类后，我们现在可以定义接受字符串的 `Query` 构造函数：

点击此处查看代码图片

```
inline
Query::Query(const std::string &s): q(new WordQuery(s)) { }
```

该构造函数分配了一个 `WordQuery` 并初始化其指针成员指向一个新分配的对象。

# NotQuery 类与 ~ 运算符

`~` 运算符生成一个 `NotQuery`，它持有一个 `Query` 并对其进行取反：

点击此处查看代码图片

```cpp
class NotQuery : public Query_base {
    friend Query operator-(const Query &q);
    NotQuery(const Query &q): query(q) { }
    // 具体类：NotQuery 定义了所有纯虚函数
    std::string rep() const override { return "~" + query.rep() + ")"; }
    QueryResult eval(const TextQuery& const) const override;
    nQuery query;
inline Query operator~(const Query &operand) {
        return std::shared_ptr<Query_base>(new NotQuery(operand));
    }
};
```

由于 `NotQuery` 的成员都是私有的，我们首先将 `~` 运算符设为友元（friend）。为了表示一个 `NotQuery`，我们将符号连接到底层 `Query` 的表示字符串上。我们对输出加上括号，以确保读者能清晰理解优先级。

值得注意的是，`NotQuery` 自身的 `rep` 成员函数对 `rep` 的调用最终会变为虚函数调用：`query.rep()` 是 `Query` 类 `rep` 成员的非本地调用。`Query::rep` 调用了 `q->rep()`，这是一个通过其 `Query_base` 指针进行的虚函数调用。

`~` 运算符动态分配了一个新的 `NotQuery` 对象。返回（隐式地）使用了创建 `shared_ptr<Query_base>` 的 `Query` 构造函数。也就是说，返回语句等同于

点击此处查看代码图片

```cpp
// 将生成的 NotQuery 指针绑定到 shared_ptr<Query_base>
shared_ptr<Query_base> tmp(new NotQuery(expr));
return Query(tmp); // 使用接受 shared_ptr 的 Query 构造函数
```

`eval` 方法足够复杂，我们将在类体之外实现它。见于 §15.9.4 (第 647 页)。

# BinaryQuery 类

`BinaryQuery` 类是一个抽象基类，它持有操作两个操作数的查询类型所需的所需的数据：

点击此处查看代码图片

```cpp
class BinaryQuery: public Query_base {
protected:
    BinaryQuery(const Query& l, const Query& r, std::string s):
    lhs(l), rhs(r), opSym(s) {
    // 抽象类：BinaryQuery 没有定义 eval
    std::string rep() const { return "(" + lhs.rep() + " " + opSym + " " + rhs.rep() + ")"; }
    }
    Query lhs, rhs; // 右操作和左操作数
    std::string opSym; // 运算符名称
};
```

`BinaryQuery` 中的数据是两个 `Query` 操作数以及对应的运算符符号。构造函数接受两个操作数和一个运算符符号，并将它们分别存储在对应的数据成员中。

为了表示一个 `BinaryOperator`，我们生成一个带括号的表达式，该表达式由左操作数的表示字符串、运算符以及右操作数的表示字符串组成。当我们显示一个 `NotQuery` 时，对 `rep` 的调用最终会向 `lhs` 和 `rhs` 指向的 `Query_base` 对象的 `rep` 函数进行虚调用。

> 注意
> `BinaryQuery` 类没有定义 `eval` 函数并继承了一个纯虚函数。`BinaryQuery` 也是一个抽象基类，我们无法创建 `BinaryQuery` 类型的对象。

# AndQuery 和 OrQuery 类以及关联运算符

`AndQuery` 和 `OrQuery` 类及其对应的运算符非常相似：

点击此处查看代码图片

```cpp
class AndQuery: public BinaryQuery {
    friend Query operator&(const Query&);
    AndQuery(const Query& left, const Query& right):
        BinaryQuery(left, right, "&") { }
    // 具体类：AndQuery 继承 rep 并定义了剩余的虚函数
    QueryResult eval(const TextQuery&) const;
};
inline Query operator&(const Query& lhs, const Query& rhs)
{
    return std::shared_ptr<Query_base>(new AndQuery(lhs, rhs));
}
class OrQuery: public BinaryQuery {
    friend Query operator|(const Query&);
    OrQuery(const Query& left, const Query& right):
        BinaryQuery(left, right, "|") { }
    QueryResult eval(const TextQuery&) const;
};
inline Query operator|(const Query& lhs, const Query& rhs)
{
    return std::shared_ptr<Query_base>(new OrQuery(lhs, rhs));
}
```

这些类将相应的运算符设为友元，并使用构造函数创建对应类型的 `BinaryQuery`。它们继承了 `rep` 的定义并重写了 `eval` 函数。与运算符 `&` 和 `|` 返回新分配对象的 `shared_ptr`。

# 练习 15.9.3

**练习 15.34**：对于图 15.3 (第 638 页) 中的表达式：
- (a) 执行该表达式的构造函数。
- (b) 来自 `q` 的 `rep` 调用。
- (c) 来自 `q` 的 `eval` 调用。

**练习 15.35**：实现 `Query` 和 `Query_base` 类，包括 `rep` 的定义，但省略 `eval` 的定义。

**练习 15.36**：在构造函数和 `rep` 成员中放置打印语句，并运行代码以检查 (a) 和 (b) 的答案。

**练习 15.37**：如果派生类的成员是 `shared_ptr<Query_base>` 而不是 `Query`，你的类需要哪些更改？

**练习 15.38**：以下声明是否合法？如果不合法，为什么？如果合法，解释这些声明的意思。

```cpp
BinaryQuery a = Query("fire") & Query("bird");
AndQuery b = Query("fire") & Query("bird");
OrQuery c = Query("fire") & Query("bird");
```

# 15.9.4. eval 函数

`eval` 函数是查询系统的核心。每个这些函数都会对其操作数调用 `eval` 然后应用自己的逻辑：`OrQuery eval` 返回操作数的并集；`AndQuery` 返回交集。`NotQuery` 必须返回操作数集合中不包含的行号。

为了支持 `eval` 函数中的处理，我们需要练习 12.3.2 (第 490 页) 中添加的 `QueryResult` 版本。我们假设 `QueryResult` 具有 `begin` 和 `end` 成员，允许遍历行号集合。我们还假设 `QueryResult` 有一个名为 `get_file` 的成员，返回执行查询的底层文件的 `shared_ptr`。

> 警告
> 我们的 `Query` 类成员是在练习 12.3.2 (第 490 页) 中为 `QueryResult` 定义的。

`OrQuery::eval`: 表示两个操作数结果的并集，我们通过对每个操作数调用 `eval` 获取。这些操作数是 `Query` 对象，调用 `eval` 是调用 `Query::eval`，后者反而对底层 `Query_base` 对象进行虚调用。这些调用每一个都产生一个表示操作数行号的 `Query`。我们将这些行号合并到一个新集合：

点击此处查看代码图片

```cpp
// 返回操作数集合的并集
QueryResult
OrQuery::eval(const TextQuery& text) const
{
  // 通过 Query 成员 lhs 和 rhs 进行虚调用
  // eval 的调用返回每个操作数的 QueryResult
  auto right = rhs.eval(text), left = lhs.eval(text);
  // 将左操作数的行号拷贝到结果集中
  auto ret_lines = make_shared<set<line_no>>(left.begin(), left.end());
  // 从右操作数插入行
  ret_lines->insert(right.begin(), right.end());
  // 返回表示 lhs 和 rhs 并集的新 QueryResult
  return QueryResult(rep(), ret_lines, left.get_file());
}
```
