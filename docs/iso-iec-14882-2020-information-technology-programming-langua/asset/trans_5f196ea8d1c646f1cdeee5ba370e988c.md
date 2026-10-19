

# 11.4.9.3 静态数据成员 [class.static.data]

1 静态数据成员不是类子对象的组成部分。如果静态数据成员被声明为 thread_local，则每个线程有一个该成员的副本。如果静态数据成员未被声明为 thread_local，则有一个数据成员的副本，由该类的所有对象共享。

2 静态数据成员不得为 mutable（9.2.2）。静态数据成员不得为未命名类（11.1）或局部类（11.6）的直接成员（11.4），或其（可能间接）嵌套类（11.4.11）的直接成员。

3 在类定义中对非内联静态数据成员的声明不是定义，并且其类型可以是不完全类型，除 cv void 外。未在类定义中内联定义的静态数据成员的定义应出现在包围成员类定义的命名空间作用域中。在命名空间作用域的定义中，静态数据成员的名称应使用 :: 运算符限定为其类名。静态数据成员定义中的初始化表达式位于其类的作用域内（6.4.7）。

> [示例 1:
```
class process {
    static process* run_chain;
    static process* running;
};

process* process::running = get_main();
process* process::run_chain = running;
```
类的静态数据成员 run_chain 在全局作用域中定义；记号 process::run_chain 指定成员 run_chain 是类 process 的成员并且在类 process 的作用域中。在静态数据成员定义中，初始化表达式引用类 process 的静态数据成员 running。——示例结束

> [注 1：静态数据成员一旦被定义，即使尚未创建其类的对象，它也存在。

> [示例 2：在上面的示例中，即使程序未创建类 process 的对象，run_chain 和 running 也存在。——示例结束]

4 如果非易失性非内联 const 静态数据成员为整型或枚举类型，则其在类定义中的声明可以指定大括号或等号初始化器，其中每个为赋值表达式的初始化子句都是常量表达式（7.7）。如果该成员在程序中被 odr 使用（6.3），则仍应在命名空间作用域中定义该成员，且命名空间作用域的定义不得包含初始化器。内联静态数据成员可以在类定义中定义，并且可以指定大括号或等号初始化器。如果成员使用 constexpr 说明符声明，则可以在命名空间作用域中重新声明且不带初始化器（此用法已弃用；参见 D.7）。其他静态数据成员的声明不得指定大括号或等号初始化器。

> [注 2：在有效程序中，odr 使用的静态数据成员有且仅有一个定义（6.3）。——注结束]

> [注 3：命名空间作用域中类的静态数据成员具有类名称的链接（6.6）。——注结束]

7 静态数据成员的初始化和销毁与非局部变量完全相同（6.9.3.2、6.9.3.3、6.9.3.4）。

## 11.4.10 位域 [class.bit]

1 形如 identifier_opt attribute-specifier-seq_opt : constant-expression brace-or-equal-initializer_opt 的成员声明符指定一个位域。可选的 attribute-specifier-seq 属于正在声明的实体。位域不得为静态成员。位域应具有整型或枚举类型；位域语义属性不是类成员类型的组成部分。constant-expression 应为积分常量表达式，其值大于或等于零，称为位域的宽度。如果位域的宽度大于位域类型的宽度（或在枚举类型的情形下，其底层类型的宽度），则多余的位为填充位（6.8）。类对象中位域的分配是实现定义的。位域的对齐是实现定义的。位域被打包到某个可寻址的分配单元中。

> [注 1：位域在某些机器上跨越分配单元，在另一些机器上不跨越。位域在某些机器上从右到左分配，在另一些机器上从左到右分配。——注结束]

2 省略标识符的位域声明声明一个未命名位域。未命名位域不是成员且不能被初始化。未命名位域不得使用 cv 限定的类型声明。[注 2：未命名位域用于填充以符合外部强加的布局。——注结束] 作为特例，宽度为零的未命名位域指定下一个位域在分配单元边界上对齐。只有在声明未命名位域时宽度才可以为零。

3 地址运算符 & 不得应用于位域，因此不存在指向位域的指针。非 const 引用不得绑定到位域（9.4.4）。[注 3：如果类型为 const T& 的引用的初始化器是引用位域的左值，则引用绑定到初始化为保存位域值的临时对象；引用并非直接绑定到位域。参见 9.4.4。——注结束]

4 如果将整型值（除 bool 外）存储到宽度为 N 的位域中，且该值可以在宽度为 N 且与位域类型具有相同符号性的假设有符号或无符号整数类型中表示，则原始值和位域的值比较相等。如果将值 true 或 false 存储到任意大小的 bool 类型的位域中（包括一位位域），则原始 bool 值和位域的值比较相等。如果将枚举类型的值存储到相同类型的位域中，且宽度足以容纳该枚举类型的所有值（9.7.1），则原始值和位域的值比较相等。

```
[示例 1:

enum BOOL { FALSE=0, TRUE=1 };
struct A {
    BOOL b:1;
};
A a;
void f() {
    a.b = TRUE;
    if (a.b == TRUE)        // yields true
        { /* ... */ }
}
— end example]
```

## 11.4.11 嵌套类声明 [class.nest]

1 一个类可以在另一个类中声明。在另一个类中声明的类称为嵌套类。嵌套类的名称是其外围类的局部名称。嵌套类位于其外围类的作用域中。[注 1：参见 7.5.4 关于使用非静态数据成员和非静态成员函数的限制。——注结束]

```
[示例 1:

int x;
int y;

struct enclose {
    int x;
    static int s;

    struct inner {
        void f(int i) {
            int a = sizeof(x);        // OK: operand of sizeof is an unevaluated operand
            x = i;                    // error: assign to enclose::x
            s = i;                    // OK: assign to enclose::s
            ::x = i;                  // OK: assign to global x
            y = i;                    // OK: assign to global y
        }
        void g(enclose* p, int i) {
            p->x = i;                 // OK: assign to enclose::x
        }
    };
};
```

```
inner* p = 0; // error: inner not in scope
```

— end example]

2 嵌套类的成员函数和静态数据成员可以在包围其类定义的命名空间作用域中定义。

[示例 2:

```
struct enclose {
  struct inner {
    static int x;
    void f(int i);
  };
};

int enclose::inner::x = 1;

void enclose::inner::f(int i) { /* ... */ }
```

— end example]

3 如果类 X 在命名空间作用域中定义，则嵌套类 Y 可以在类 X 中声明并随后在类 X 的定义中定义，或随后在包围类 X 定义的命名空间作用域中定义。

[示例 3:

```
class E {
  class I1; // forward declaration of nested class
  class I2;
  class I1 { }; // definition of nested class
};
class E::I2 { }; // definition of nested class
```

— end example]

4 与成员函数一样，在嵌套类中定义的友元函数（11.9.4）位于该类的词法作用域中；它遵循与该类的静态成员函数相同的名称绑定规则（11.4.9），但它没有对外部类的成员的特殊访问权限。

## 11.4.12 嵌套类型名 [class.nested.type]

1 类型名遵循与其它名称完全相同的范围规则。特别是，在类定义中定义的类型名在未加限定的情况下不能在其类之外使用。

[示例 1:

```
struct X {
  typedef int I;
  class Y { /* ... */ };
  I a;
};

I b; // error
Y c; // error
X::Y d; // OK
X::I e; // OK
```

— end example]

## 11.5 联合体 [class.union]

### 11.5.1 通用 [class.union.general]

1 联合体是使用 class-key union 定义的类。

2 在联合体中，非静态数据成员是活动的，如果其名称引用一个已开始生命周期且尚未结束的对象（6.7.3）。在任何时候，联合体类型对象的非静态数据成员中最多只有一个是活动的，即在任何时候最多只有一个非静态数据成员的值存储在联合体中。

[注 1：为了简化联合体的使用，做出了一个特殊保证：如果标准布局联合体包含若干个共享共同初始序列的标准布局结构体（11.4），并且如果一个

