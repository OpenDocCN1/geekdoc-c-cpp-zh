

## 9.12.3 Carries dependency attribute [dcl.attr.depend]

```
alignas(double) unsigned char c[sizeof(double)];    // array of characters, suitably aligned for a double
extern unsigned char c[sizeof(double)];               // no alignas necessary
alignas(float)
    extern unsigned char c[sizeof(double)];            // error: different alignment in declaration
```

— end example]

1 属性标记 carries_dependency 指定函数进出时的依赖传播。它在每个属性列表中最多出现一次，且不得存在属性参数子句。该属性可应用于函数声明或 lambda 中参数声明的声明符 id，此时它指定参数的初始化会携带依赖到该对象的每个左值到右值转换（7.3.2）（6.9.2）。该属性也可应用于函数声明的声明符 id，此时它指定返回值，如有，则携带对函数调用表达式求值的依赖。

2 函数的首次声明如果有任何声明为其声明符 id 指定了 carries_dependency 属性，则必须指定该属性。此外，函数的首次声明如果有任何声明为该函数的某个参数指定了 carries_dependency 属性，则必须为该参数指定该属性。如果一个函数或其某个参数在一个翻译单元的首次声明中带有 carries_dependency 属性，而在另一个翻译单元的首次声明中未带该属性，则程序格式错误，无需诊断。

3 [注记 1：carries_dependency 属性不会改变程序的含义，但可能导致生成更高效的代码。 — 结束注记]

4 [示例 1：

```
/* Translation unit A. */

struct foo { int* a; int* b; };
std::atomic<struct foo *> foo_head[10];
int foo_array[10][10];

[[carries_dependency]] struct foo* f(int i) {
    return foo_head[i].load(memory_order::consume);
}

int g(int* x, int* y [[carries_dependency]]) {
    return kill_dependency(foo_array[*x][*y]);
}

/* Translation unit B. */

[[carries_dependency]] struct foo* f(int i);
int g(int* x, int* y [[carries_dependency]]);

int c = 3;

void h(int i) {
    struct foo* p;

    p = f(i);
    do_something_with(g(&c, p->a));
    do_something_with(g(p->a, &c));
}
```

函数 f 上的 carries_dependency 属性意味着返回值会携带 f 之外的依赖，因此实现在返回 f 时无需约束顺序。f 及其调用者的实现可以选择保留依赖而不是发出硬件内存排序指令（又称栅栏）。函数 g 的第二个参数具有 carries_dependency 属性，但第一个参数没有。因此，函数 h 对 g 的第一次调用会携带依赖进入 g，但第二次调用不会。可能实现需要在对 g 的第二次调用之前插入栅栏。 — 结束示例]

```
}
case 5:
    h();
case 4:                         // implementation may warn on fallthrough
    i();
    [[fallthrough]];              // error
}
```

— end example]

## 9.12.6  Likelihood attributes [dcl.attr.likelihood]

*attribute-tokens* likely 和 unlikely 可应用于标签或语句。*attribute-tokens* likely 和 unlikely 在每个 *attribute-list* 中最多出现一次，且不得存在 *attribute-argument-clause*。*attribute-token* likely 不得出现在包含 *attribute-token* unlikely 的 *attribute-specifier-seq* 中。

*建议做法：* likely 属性的使用旨在允许实现针对包含它的执行路径进行优化，该路径被认为比任何不包含对语句或标签的属性的替代执行路径任意更可能。unlikely 属性的使用旨在允许实现针对包含它的执行路径进行优化，该路径被认为比任何不包含对语句或标签的属性的替代执行路径任意更不可能。执行路径仅当包含对该标签的跳转时才包含该标签。

> [*注记 1：* 过度使用任一属性都可能导致性能下降。 — *结束注记*]

*示例 1：*

```
    void g(int);
    int f(int n) {
        if (n > 5) [[unlikely]] {       // n > 5 is considered to be arbitrarily unlikely
            g(0);
            return n * 2 + 1;
        }

        switch (n) {
        case 1:
            g(1);
            [[fallthrough]];

        [[likely]] case 2:               // n == 2 is considered to be arbitrarily more
            g(2);                         // likely than any other value of n
            break;
        }
        return 3;
    }
```

— end example]

## 9.12.7  Maybe unused attribute [dcl.attr.unused]

*attribute-token* maybe_unused 表示名称或实体可能有意未使用。它在每个 *attribute-list* 中最多出现一次，且不得存在 *attribute-argument-clause*。

该属性可应用于类声明、*typedef-name*、变量（包括结构化绑定声明）、非静态数据成员、函数、枚举或枚举器的声明。

名称或实体在未标记 maybe_unused 的情况下声明后，后续可以带该属性重新声明，反之亦然。实体在首次标记它的声明后被视为已标记。

*建议做法：* 对于标记为 maybe_unused 的实体，实现不应发出该实体或其结构化绑定（如果有）被使用或未使用的警告。对于未标记 maybe_unused 的结构化绑定声明，实现不应发出此类警告，除非其所有结构化绑定均未使用。

## 第三卷·第一号

### 乡村空間の再生と観光の持続可能性を考える。

地域の食文化と観光を結びつけ、農村の新しい価値を創出する実践を紹介する。農家の知恵や技は、その土地ならではの食の物語として観光資源となる。

農村には豊かな自然と食の文化が息づいている。郷土の味を再発見し、訪れる人々との交流を通じて地域を活性化させる取り組みが各地で進んでいる。

| テーマ | 内容 |
| --- | --- |
| 食文化 | 地域固有の食材と調理法 |
| 観光 | 農家民泊・体験プログラム |
| 地域再生 | 空き家活用・移住促進 |

> 「その土地の物語を食べることこそ、最も深い旅のかたちである。」

今後は、地域住民と訪問者が共に育てる持続可能な観光のモデルが求められる。

## 9.12.9  Noreturn attribute [dcl.attr.noreturn]

1 属性标记 noreturn 指定函数不返回。它在每个属性列表中最多出现一次，且不得存在属性参数子句。该属性可应用于函数声明中的声明符 id。函数的首次声明如果有任何声明为该函数指定了 noreturn 属性，则必须指定该属性。如果一个函数在一个翻译单元中声明为带有 noreturn 属性，而在另一个翻译单元中声明为不带该属性，则程序格式错误，无需诊断。

2 如果在先前声明为带有 noreturn 属性的 f 处调用函数 f，并且 f 最终返回，则行为未定义。

> [注记 1：函数可能通过抛出异常终止。 — 结束注记]

3 建议做法：实现应发出警告，如果标记为 [[noreturn]] 的函数可能返回。

4 [示例 1：

```
[[ noreturn ]] void f() {
    throw "error";
}

[[ noreturn ]] void q(int i) { // behavior is undefined if called with an argument <= 0
    if (i > 0)
        throw "positive";
}
```

— end example]

## 9.12.10  No unique address attribute [dcl.attr.nouniqueaddr]

1 属性标记 no_unique_address 指定非静态数据成员是潜在重叠的子对象（6.7.2）。它在每个属性列表中最多出现一次，且不得存在属性参数子句。该属性可适用于非静态数据成员，但不适用于位域。

> 2 [注记 1：非静态数据成员可以与其他非静态数据成员或基类的地址相同，并且通常会在对象末尾插入的任何填充都可被重用于其他成员的存储。 — 结束注记]

[示例 1：

```
template<typename Key, typename Value,
    typename Hash, typename Pred, typename Allocator>
class hash_map {
    [[no_unique_address]] Hash hasher;
    [[no_unique_address]] Pred pred;
    [[no_unique_address]] Allocator alloc;
    Bucket *buckets;
    // ...
public:
    // ...
};
```

在此，hasher、pred 和 alloc 如果其各自的类型均为空，则可以与 buckets 具有相同的地址。 — 结束示例]

