
# ISO/14882:2017(E)

## 1 函数模板 `async` 提供了一种机制，用于可能在新的线程中启动函数，并在与其共享共享状态的 `future` 对象中提供函数的结果。

```cpp
template <class Class, Args...>
future<invoke_result<decay_t<F>, decay_t<Args...>>>
nasync(F&& f, Args&&... args);
```

```cpp
template <class Class, Args...>
future<invoke_result<decay_t<F>, decay_t<Args...>>>
async(launch policy, F&& f, Args&&... args);
```

## 2 要求
`F` 和 `Args` 中的每个 `T` 均应满足 `MoveConstructible`（可移动构造）要求，且 `INVOKE_DECAY(std::forward(f)) DECAY(std::forward(args))...` // 参见 23.14.3, 33.3.2

## 3 影响
该 `future` 的行为与带有 `launch::async | deferred` 策略的函数调用相同；对于 `F` 和 `Args` 使用相同的 `deferred` 策略相同的参数。第二个函数创建一个与返回的 `future` 关联的共享状态（`shared state`）。共享状态的 `future` 行为取决于所使用的策略（如果这些条件中有一个多个适用，实现可以选择任何一个异步共享状态）。

### 3.1
如果选择了 `async`，它将调用 `INVOKE_DECAY(std::forward(f))` 和 `DECAY(std::forward(args))...` 类似于 23.14.3, 33.3.2；如果由线程对象表示一个新的执行线程，则创建带有共享状态的并调用 `async`。任何返回值将作为结果存储在共享状态中。从执行 `INVOKE_DECAY(std::forward(f))` 和 `DECAY(std::forward(args))...` 传播的任何异常将存储在 `future` 中。存储在共享状态中的内容将影响任何从该共享状态返回的异步对象的行为。

### 3.2
如果设置为 `deferred`，则存储共享状态；`INVOKE_DECAY(std::forward(f))` 和 `DECAY(std::forward(args))...` 共享。这些 `f` 和 `args` 的拷贝构成 `deferred future`。对 `future` 的调用将评估 `INVOKE_DECAY(std::move(f), std::move(xyz))`，其中 `xyz` 是共享状态的值；`INVOKE_DECAY(std::forward(args))...` `xyz` 被存储在共享状态中。从 `future` 执行传播的任何异常将作为异常结果存储在共享状态中。在函数被调用之前，共享状态不会就绪，该调用可以从任何线程进行。该共享状态的异步返回应在调用等待函数的线程上调用延迟函数。一旦开始对 `INVOKE_DECAY(std::move(f), std::move(xyz))` 的调用，该 `future` 不再被视为有效 [注：如果此项与其他策略一起指定，例如当使用 `launch::async | launch::deferred` 的值时，当无法有效利用并发性时，实现应推迟选择或策略的选择 — 注释结束]

### 3.3
如果实现未设置值或本文档未通过实现指定值，则 `future` 返回一个默认构造的值。

## 4 返回值
一个类型为 `invoke_result<decay_t<F>, decay_t<Args>>` 的对象，它引用本地作用域之外的共享状态，其他调用此 `async` 的代码。[注：如果从 `async` 获取的 `future` 被移动，则 `future` 应该感知到其析构函数可能会阻塞，直到共享状态就绪。 — 注释结束]

## 5 同步
无论提供的策略参数如何，

### 5.1
`async` 的调用与 (4.7) `f` 的调用同步。[注：此声明即使在相应的 `future` 对象被移动到另一个时也适用。 — 注释结束]；

### 5.2
函数 `f` 的完成在 (4.7) 共享状态就绪之前排序。[注：`f` 可能不会被调用，因此其完成可能永远不会发生。 — 注释结束]

如果实现选择了 `launch::async` 策略，

- (5.3) 对异步返回对象上的等待函数的调用将共享由此 `async` 调用创建的共享状态，并将阻塞直到关联线程加入，或者超时 (3.3.2.5)；
- (5.4) 关联线程与 (4.7) 第一个成功检测到共享状态就绪的函数或与释放共享状态的最后一个函数的返回同步，以先发生者为准。

## 6 抛出异常
如果 `policy == launch::async` 且实现无法启动新线程，则抛出 `system_error`；如果无法分配数据结构的内存，则抛出 `std::bad_alloc`。

## 7 错误情况
- (7.1) `resource_unavailable_try_again` — 如果 `policy == launch::async` 且系统无法启动新线程。

## 8 示例

```cpp
int work1(int value);
int work2(int value);
int work3(int value) {
    auto handle = std::async([=]{ return work2(value); });
    int tmp = work3(value);
    return tmp + handle.get();
}
```

# ISO/IEC 14882:2017(E)

- + (21.1) — 如果存储的任务已经执行过，则满足 `promise_already_satisfied`。
- + (21.2) — 如果 `*this` 没有共享状态，则满足 `no_state`。

```cpp
void reset();
```

## 22 效果
等同于 `*this = packaged_task(std::move(f))`，其中 `f` 是存储在 `*this` 中的内容。[注：这为 `*this` 构建了一个新的共享状态。旧的状态被遗弃（33.6.5）。] — 注释结束]

## 23 抛出
- + (23.1) — 如果无法为新的共享状态分配内存，则抛出 `bad_alloc`。
- + (23.2) — 抛出错误条件为 `no_state` 的 `*this` 没有共享状态的 `future_error`。

## 33.6.10.2 packaged_task 全局变量

```cpp
template <class R, class... ArgTypes>
void swap(packaged_task<R(ArgTypes...)>&& x, packaged_task<R(ArgTypes...)>& y) noexcept;
```

1 效果：等同于通过 `swap(y) x`。

```cpp
template <class R, class Alloc>
struct uses_allocator<packaged_task<R>, Alloc>
  : true_type { };
```

2 需要：`Alloc` 应为分配器 (20.5.3)。

# ISO/IEC 14882:2017(E)

# 附录 A（信息性）

## 语法总结

此 C++ 语法的总结旨在辅助理解。它并不是对语言的精确陈述。特别是，所描述的语法接受有效 C++ 构造的超集。必须应用消歧规则（9.8, 10.1, 13.2）来区分表达式和声明。此外，必须使用访问控制、歧义和类型规则来剔除语法上正确但无意义的构造。

## A.1 关键字

新的上下文相关关键字通过 `typedef` (10.1.3)、`namespace` (10.3.1)、`class`（第 12 节）、`enumeration` (10.2) 和 `template`（第 17 节）声明引入程序。

```
typedef-name:
identifier
namespace:
identifier
namespace-alias:
identifier
class-name:
identifier
simple-template-id
enum-name:
identifier
template-name:
identifier
```

注意 `typedef-name` 命名的类也是 `class-name` (12.1)。

## A.2 词法约定

```
hex-digit:
hexadecimal-digit hexadecimal-digit
universal-character-name:
\u hex-quad
\U hex-quad
preprocessing-token:
header-name
identifier
pp-number
character-literal
user-defined-character-literal
string-literal
user-defined-string-literal
preprocessing-op-or-unc
每个非空白的字符

token:

- identifier
- keyword
- literal
- operator
- punctuation

- header-name:
  - h-char-sequence
  - "q-char-sequence

- h-char-sequence:
  - h-char
  - h-char-sequence

- h-char:
  源字符集中的除换行以外的成员

- q-char-sequence:
  - q-char
  - q-char-sequence

- q-char:
源字符集中的除换行以外的成员

- pp-number:
  - sign
  - digit
  - pp-number digit
  - pp-number nondigit
  - pp-number digit
  - pp-number sign
  - pp-number E
  - pp-number sign
  - pp-number y
  - pp-number F
  - pp-number

- identifier:
  - identifier-nondigit
  - identifier-nondigit
  - identifier-digit

- nondigit:
  - nondigit
  - universal-character-name

- 一个:
  - a b c d e f h i j m
  - n o p q r s t u v z
  - A B D E F H I J M
  - N O P Q R S T U W X

**: 一个:
  - 0 1 2 3 4 5 6 7 8 9

```

`preprocessing-op-or-unc`: 一个:

  { } ) 

  < > % % :: : ...

  new delete ? : . * & | !

  + / & /=

  = && << >> == !=

  <= && ++ - ->

and not_eq x or_eq

literal:

integer-literal

character-literal

floating-literal

boolean-literal

pointer-literal

integer-literal:

binary-literal suffix-opt

octal-literal suffix-opt

decimal-literal suffix-opt

hexadecimal-literal suffix-opt

binary-literal:

0 binary-digit

binary-literal 'opt binary-digit

octal-literal:

0 octal-digit

octal-literal 'opt octal-digit

decimal-literal:

nonzero-digit

decimal-literal 'opt decimal-digit

hexadecimal-literal:

hexadecimal-digit-sequence

binary-digit:

0

octal-digit:

0 1 2 3 4 5 6 7

nonzero-digit:

一个

1 2 3 4 5 6 7 8 9

hexadecimal-decimal-prefix: 一个:

  0x 0X

hexadecimal-digit-sequence:

hexadecimal-digit

hexadecimal-digit-sequence 'opt hexadecimal-digit

hexadecimal-digit: 一个:

0 1 2 3 4 5 6 7 8 9

a b c d e f

integer-suffix:

unsigned-prefix suffix-opt

unsigned-suffix long-suffix-opt

long-suffix suffix-opt

long-long-suffix suffix-opt

unsigned-suffix: 一个:

u

long-suffix: 一个:

1 L

long-long-suffix: 一个:

1 LL

character-literal:

encoding-prefix-opt 'sequence

encoding-prefix: 一个:

u L

c-char-sequence:

c-char

c-char-sequence: c-char

c-char:

字符集中的除双引号 " \ 或换行以外的成员

escape-sequence

universal-character-name

escape-sequence:

simple-escape-sequence

octal-escape-sequence

hexadecimal-escape-sequence

simple-escape-sequence: 一个:

\' \ f \r \ v

octal-escape-sequence:

\octal-digit

\octal-digit octal-digit

\octal-digit octal-digit

hexadecimal-escape-sequence:

\hexadecimal-digit

hexadecimal-escape-sequence hexadecimal-digit

floating-literal:

decimal-floating-literal

hexadecimal-floating-literal

decimal-floating-literal:

fractional-constant exponent-part-opt suffix-opt

digit-sequence exponent-part suffix-opt
