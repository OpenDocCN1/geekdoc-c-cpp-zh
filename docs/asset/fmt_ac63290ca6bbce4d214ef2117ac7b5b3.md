
```cpp
另一个示例，
class C {
void h(int *[C[10]]);
```
```cpp
// 不是：void h(int *C[10]);
```
-- end example

## 8.3 声明符（declarators）的含义

+ 1 声明符列表出现在可选的（第 7 节）声明说明符（`decl-specifier`）之后。每个声明符恰好声明一个声明符-id；它是被声明的标识符。未限定的声明符-id 应该是声明特殊函数（12.1, 12.3, 12.4, 13.5）的简单标识符，以及声明模板特化或部分特化（14.7）的简单标识符。当声明符-id 被限定时，声明符应引用该限定符所指的类或命名空间之前声明的成员（或者在命名空间的情况下，引用一组内联命名空间 (7.3.1)）或者引用已特化的成员；该成员不应通过声明符-id 的嵌套名说明符所指定的类或命名空间作用域内的 `using` 声明引入。限定声明符-id 的嵌套名说明符不应以 `decltype` 说明符开头；注意：如果限定符是全局 `::` 作用域解析运算符，则声明符引用全局命名空间作用域内的命名标识。— 注释结束 | 声明符-id 之后可选的属性说明符序列（`attribute-specifier-seq`）属于被声明的实体。

+ `static`, `thread_load`, `extern`, `register`, `mutable`, `friend`, `inline`, `virtual`, `typedef` 说明符直接应用于初始化声明符列表中的每个声明符-id；每个声明符-id 指定的类型取决于声明说明符序列（`decl-specifier-seq`）及其声明符本身。

+ 3 因此，特定标识符的声明符形式如下：

`T D`

其中 `T` 的形式为 `attribute-specifier-seq_opt` `decl-specifier-seq`，而 `D` 是声明符。遵循对于该声明所包含的声明符-id 所指定类型的递归过程。

+ 4 首先，声明说明符序列确定一个类型。在声明中：

`T D`

`decl-specifier-seq` 确定类型 `T`。[示例：在声明

`int unsigned i;`

中类型说明符 `int unsigned` 决定了类型 "unsigned int" (7.1.2)。— 示例结束

+ 5 在声明 `attribute-specifier-seq_opt T D` 中，如果 `D` 是一个未修饰的标识符，则该标识符的类型为 'T'。

+ 6 在声明 `TD` 中，如果 `D` 的形式为

`( D1 )`

则包含的声明符-id 的类型与声明

`D1`

中包含的声明符-id 的类型相同。

括号不会改变嵌入的声明符-id 的类型，但它们可以改变复杂结构的绑定。

### 8.3.1 指针 [dcl.ptr]

+ 1 在声明 `TD` 中，如果 `D` 的形式为

`* attribute-specifier-seq_opt cv-specifier-seq_opt D1`

且 `D1` 中声明符的类型为“派生声明符类型列表”（`derived-declarator-type-list`），则标识符 `D` 的类型为“指向 `T` 的派生声明符类型列表指针”。`cv` 说明符作用于指针而不是对象。同样，可选的属性说明符序列 (7.6) 指针而不是对象。

+ 2 [示例：声明

`const int i = 10, &ci, *const pc = pc;`

`int i, *p, *const cp = 8;`

声明 `ci`，一个常量整数；`pc`，一个指向常量整数的指针；`pc`，一个指向常量整数的常量指针；`pc`，一个指向指向常量整数的指针；i；一个整数；] (注：原文 `pc` 处重复，翻译遵循原文)

```cpp
class C {
void f(int(*fp)(C C)) {}
// 不是：void f(int C)
```
```cpp
int g();
void foo() {
  f(1);
  f(g);
// 错误：不能将 1 转换为函数指针
// OK
```
```cpp
另一个示例，
class C {
void h(int *[C[10]]);
```
```cpp
// 不是：void h(int *C[10]);
```
-- end example
