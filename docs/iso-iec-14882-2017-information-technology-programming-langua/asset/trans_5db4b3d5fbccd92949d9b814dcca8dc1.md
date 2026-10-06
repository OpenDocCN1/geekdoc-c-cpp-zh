

# ISO/IEC 14882:2017(E)

- 每个与其他所有类型都不同的枚举类型。在所有这些情况下，每个枚举都有一个*底层类型*（underlying type）。底层类型可以使用*枚举基*（enum-base）指定。对于作用域枚举类型，如果未指定，则底层类型为*int*。在这种情况下，该底层类型被称为*固定的*（fixed）。在*枚举指定符*（enum-specifier）的结束括号之后，每个枚举成员的类型为其枚举类型，且枚举定义中的*常量表达式*（constant-expression）应当为底层类型的常量表达式（8.20)。如果底层类型不是固定，则在结束括号之前的每个枚举成员的类型为如下定义的底层类型：

- 如果为枚举成员指定了初始化器，则*常量表达式*应当为整数表达式（8.20)。如果该表达式具有无符号类型，则该枚举成员具有该枚举的底层类型，否则具有与表达式相同的类型。

- 如果没有为枚举成员指定初始化器，则其类型为无符号整数类型。

- 否则，枚举成员的类型与前一个枚举成员的类型相同，在这种情况下，该类型为足以容纳增值的无符号整数类型。如果不存在此类类型，则程序是非格式的（ill-formed）。

枚举类型从其声明点（6.3.2）到其*枚举基*（如果有）之后之后之前是不完全类型，在此时，它变为一个完整类型。底层类型不是固定的枚举，从其声明点到其*枚举指定符*结束之后之前是不完全类型，在此时，它变为一个完整类型。

底层类型不是固定的枚举由实现定义——即使用哪种整数类型来表示。如果没有整数类型可以表示枚举中定义的所有枚举成员值，则该程序是非格式的。底层类型不应大于无法放入*int*或*unsigned*的枚举成员值。如果*枚举列表*（enum-list）为空，则底层类型为只有一个值 0 的枚举。

对于底层类型为固定的枚举，底层类型的值是最小的*枚举成员*和最大的*枚举成员*，其中最小和最大对应于如下定义的范围 [min, max]：令 *K* 为补码表示的数字，对于反码或符号位表示为 0，对于 2^M - 1，其中 *M* 是大于或等于 max - min + 1 的最小值，且也是非负整数。持有底层类型所有值所需的最小位域的大小，当 *M* 为零时为 *M*，否则如此。

非作用域枚举成员的值通过整数提升（7.6）转换为整数。示例：

```cpp
enum color { red, yellow=2, blue };
color col = red;
color *cp = &col;
if (*cp == blue) // 这组值用于定义枚举类型的提升和转换。它并不排除表达式具有超出此范围的值。注意作用域枚举不提供这种枚举到 int 的转换：
```cpp
enum Col { red, yellow, green };
int x = Col::red; // ：int无法转换为 color
if (y == Col) // ：Col 没有 bool
```

- 11 每个枚举名和每个枚举成员都在直接包含枚举指定符的作用域内声明。作用域规则在 6.3 和 6.4 中定义了所有名称。示例：

```cpp
enum direction {left='l', right='r'};
void g() {
    direction d; // OK
    d = left; // OK
    d = direction::right; // OK
}
```

```cpp
void h(altitude='h', low='l') {
    altitude a;
    a = high; // 错误：high不在作用域内
    a = altitude::low; // OK
}
```

在作用域内声明的枚举成员可以使用类成员运算符（::、点 (.) 和箭头 (->））进行引用，见 8.2.5。示例：

```cpp
struct X {
    enum direction {left='l', right='r'};
    int f(int i) return i=left ? 0 : i=right ? 2;
};
```

```cpp
void g(X* p) {
    direction d; // 错误：direction不在作用域内
    int i;
    i = p->left(left); // 错误：left不在作用域内
    i = p->X(right); // OK
    i = p->f(p->left); // ...
}
```

- 12 如果枚举头文件具有嵌套名称指定符，则枚举指定符应当引用之前直接在类或命名空间中声明的枚举，或者命名空间内联命名空间（10.3.1）元素中的枚举（即不仅仅是由于 using 声明引入的），且枚举指定符应当出现在包含之前声明的命名空间中。在情况下，定义中枚举头的嵌套名称指定符不以类型指定符开头。

## 10.3 命名空间 [basic.namespace]

- 1 命名空间是一个可选命名的声明区域。命名空间的名称可以用于访问在该命名空间中声明的实体；即命名空间的成员。与其他声明区域不同，命名空间的定义可以跨越一个或多个翻译单元的多个部分划分。

- 2 翻译单元的最外层声明区域是一个命名空间；见 6.6.6。

### 10.3.1 命名空间定义 [namespace.def]

```cpp
namespace-name:
identifier
namespace-alias
namespace-definition:
  named-namespace-definition
  unnamed-namespace-definition
unnamed-namespace-definition:
  named-namespace-definition:
    inline_opt namespace attribute-spec_opt identifier { namespace-body }
  unnamed-namespace-definition:
    inline_opt namespace attribute-spec_opt { namespace-body }
  nested-namespace-definition:
    namespace-enclosing-namespace-specification :: identifier { namespace-body }
enclosing-namespace-specification:
  identifier
namespace-body:
  declaration-seq_opt
```

- 1 每个命名空间定义应当出现在全局作用域或命名空间作用域内（6.3.6）。标识符是命名空间的名称。如果标识符在查找（6.4.1）时指向命名空间名（但不是命名空间别名），该名称是在该命名空间的成员中引入的，则命名空间定义扩展之前声明的命名空间。否则，标识符作为命名空间名引入到出现具名命名空间定义的声明区域中。

- 3 由于命名空间定义在其命名空间体体中包含声明，且命名空间定义本身是一个声明，可以推导出命名空间定义可以嵌套。示例：

```cpp
namespace Outer {
    int i;
    namespace Inner {
        void i() { i++; } // Outer::i
        int i;
        void i() { i++; } // Inner::i
    }
}
```

- 4 声明的封闭命名空间是该声明在词法上出现的所有命名空间，但位于原始命名空间之外的命名空间声明（例如，作为定义

