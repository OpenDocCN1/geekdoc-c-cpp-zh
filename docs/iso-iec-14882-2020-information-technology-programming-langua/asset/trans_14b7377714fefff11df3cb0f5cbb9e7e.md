

*user-defined-integer-literal:*
  *decimal-literal ud-suffix*
  *octal-literal ud-suffix*
  *hexadecimal-literal ud-suffix*
  *binary-literal ud-suffix*

*user-defined-floating-point-literal:*
  *fractional-constant exponent-part_opt ud-suffix*
  *digit-sequence exponent-part ud-suffix*
  *hexadecimal-prefix hexadecimal-fractional-constant binary-exponent-part_opt ud-suffix*
  *hexadecimal-prefix hexadecimal-digit-sequence binary-exponent-part_opt ud-suffix*

*user-defined-string-literal:*
  *string-literal ud-suffix*

*user-defined-character-literal:*
  *character-literal ud-suffix*

*ud-suffix:*
  *identifier*

1 如果一个标记同时匹配 *user-defined-literal* 和另一种 *literal* 种类，则将其视为后者。
[示例 1：`123_km` 是 *user-defined-literal*，但 `12LL` 是 *integer-literal*。 — 示例结束]
在 *user-defined-literal* 中位于 *ud-suffix* 前面的语法非终结符，被视为与该非终结符语法相匹配的最长字符序列。

2 *user-defined-literal* 被视为对字面量运算符或字面量运算符模板的调用（12.8）。对于给定的具有 *ud-suffix* X 的 *user-defined-literal* L，其调用形式通过在 L 的上下文中使用无限定名称查找规则（6.5.2）查找其字面量后缀标识符为 X 的 *literal-operator-id* 来确定。设 S 为此次查找找到的声明集合。S 不应为空。

3 如果 L 是 *user-defined-integer-literal*，设 n 为去掉其 *ud-suffix* 后的字面量。如果 S 包含参数类型为 `unsigned long long` 的字面量运算符，则字面量 L 被视为以下形式的调用
`operator "" X(nULL)`
否则，S 必须包含原始字面量运算符或数值字面量运算符模板（12.8），但不能同时包含两者。如果 S 包含原始字面量运算符，则字面量 L 被视为以下形式的调用
`operator "" X("n")`
否则（S 包含数值字面量运算符模板），L 被视为以下形式的调用
`operator "" X<'c1', 'c2', ... 'ck'>( )`
其中 n 是源字符序列 c1 c2...ck。
[注 1：序列 c1c2...ck 只能包含来自基本源字符集的字符。 — 注释结束]

4 如果 L 是 *user-defined-floating-point-literal*，设 f 为去掉其 *ud-suffix* 后的字面量。如果 S 包含参数类型为 `long double` 的字面量运算符，则字面量 L 被视为以下形式的调用
`operator "" X(fL)`
否则，S 必须包含原始字面量运算符或数值字面量运算符模板（12.8），但不能同时包含两者。如果 S 包含原始字面量运算符，则字面量 L 被视为以下形式的调用
`operator "" X("f")`
否则（S 包含数值字面量运算符模板），L 被视为以下形式的调用
`operator "" X<'c1', 'c2', ... 'ck'>( )`
其中 f 是源字符序列 c1 c2...ck。
[注 2：序列 c1c2...ck 只能包含来自基本源字符集的字符。 — 注释结束]

5 如果 L 是 *user-defined-string-literal*，设 str 为去掉其 *ud-suffix* 后的字面量，设 len 为 str 中的代码单元数（即不包括终止空字符的长度）。如果 S 包含一个具有非类型模板参数的字面量运算符模板，且 str 是其良构的 *template-argument*，则字面量 L 被视为以下形式的调用
`operator "" X<str>( )`
否则，字面量 L 被视为以下形式的调用
`operator "" X(str, len)`

6 如果 L 是 *user-defined-character-literal*，设 ch 为去掉其 *ud-suffix* 后的字面量。S 必须包含一个字面量运算符（12.8），其唯一参数的类型为 ch，且字面量 L 被视为以下形式的调用

```
operator "" X(ch)
```

7 [示例 2：

```
long double operator "" _w(long double);
std::string operator "" _w(const char16_t*, std::size_t);
unsigned operator "" _w(const char*);
int main() {
    1.2_w;        // calls operator "" _w(1.2L)
    u"one"_w;    // calls operator "" _w(u"one", 3)
    12_w;         // calls operator "" _w("12")
    "two"_w;     // error: no applicable literal operator
}
```

— 示例结束]

8 在翻译阶段 6（5.2）中，相邻的 *string-literals* 会被连接，并且 *user-defined-string-literals* 为此目的被视为 *string-literals*。在连接期间，*ud-suffixes* 会被移除并忽略，连接过程按 5.13.5 中所述进行。在阶段 6 结束时，如果一个 *string-literal* 是涉及至少一个 *user-defined-string-literal* 的连接的结果，则所有参与的 *user-defined-string-literals* 必须具有相同的 *ud-suffix*，并且该后缀应用于连接结果。

9 [示例 3：

```
int main() {
    L"A" "B" "C"_x;    // OK: same as L"ABC"_x
    "P"_x "Q" "R"_y;  // error: two different ud-suffixes
}
```

— 示例结束]

## 6 基础 [basic]

### 6.1 前言 [basic.pre]

1 [注 1：本条款介绍了 C++ 语言的基本概念。它解释了对象与名称之间的区别以及它们与表达式的值类别的关系。它引入了声明和定义的概念，并介绍了 C++ 对类型、作用域、链接和存储期的概念。讨论了启动和终止程序的机制。最后，本条款介绍了语言的基本类型并列出了从这些类型构造复合类型的方式。 — 注释结束]

2 [注 2：本条款不涵盖仅影响语言某一部分的的概念。此类概念在相关条款中讨论。 — 注释结束]

3 实体是值、对象、引用、结构化绑定、函数、枚举数、类型、类成员、位域、模板、模板特化、命名空间或包。

4 名称是对标识符（5.10）、operator-function-id（12.6）、literal-operator-id（12.8）、conversion-function-id（11.4.8.3）或 template-id（13.3）的一种用法，该用法表示实体或标签（8.7.6，8.2）。

5 每个表示实体的名称都由声明引入。每个表示标签的名称要么由 goto 语句（8.7.6）引入，要么由带标签语句（8.2）引入。

6 变量由引用声明引入，但非静态数据成员除外，或由对象声明引入。变量的名称，如果有，则表示该引用或对象。

7 局部实体是具有自动存储期（6.7.5.4）的变量、其对应变量为此类实体的结构化绑定（9.6），或 *this* 对象（7.5.2）。

8 有些名称表示类型或模板。通常，每当遇到一个名称时，都需要确定该名称是否表示这些实体，然后再继续解析包含它的程序。此过程称为名称查找（6.5）。

9 两个名称是相同的，如果

- (9.1) — 它们是由相同的字符序列组成的标识符，或
- (9.2) — 它们是由相同的运算符形成的 operator-function-id，或
- (9.3) — 它们是由相同的类型形成的 conversion-function-id，或
- (9.4) — 它们是引用同一类、函数或变量的 template-id（13.6），或
- (9.5) — 它们是由相同的字面量后缀标识符形成的 literal-operator-id（12.8）。

10 在多个翻译单元中使用的名称可能取决于名称在每个翻译单元中指定的链接（6.6），从而可能引用这些翻译单元中的同一实体。

### 6.2 声明和定义 [basic.def]

1 声明（条款 9）可向翻译单元引入一个或多个名称，或重新声明先前声明引入的名称。如果是这样，声明指定了这些名称的解释和语义属性。声明还可能具有包括以下效果：

- (1.1) — 静态断言（9.1），
- (1.2) — 控制模板实例化（13.9.3），
- (1.3) — 指导构造函数的模板参数推导（13.7.2.3），
- (1.4) — 属性的使用（9.12），以及
- (1.5) — 无事发生（在空声明的情况下）。

2 除非满足以下条件，否则声明所声明的每个实体也由该声明定义：

- (2.1) — 它声明了一个函数但未指定函数体（9.5），
- (2.2) — 它包含 extern 说明符（9.2.2）或链接说明22（9.11），并且既没有初始值设定项也没有函数体，

22) 出现在链接说明中的大括号封闭的 declaration-seq 中并不影响声明是否为定义。

