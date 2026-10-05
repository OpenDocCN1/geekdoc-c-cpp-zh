
当 c 被销毁时，析构函数将按反序调用，也就是说首先调用 C 的，然后是 B 的，最后是 A 的。这里有一个更复杂的例子。考虑以下继承体系方案，其中每个类都包含默认构造函数和析构函数。它们将按什么顺序被调用？

```cpp
class A {...};
class B {......};
class C : public B, public A {......};
class D {......};
class E : public D {......};
class F : public E {......};
class G : public F, public C {{{...};
```

```cpp
int main() {
  G g;
  ...
}
```

子对象的构造顺序为 D, E, F, B, A, C, G。当 g 被销毁时，子对象的析构函数将按反序调用。

## 创建多个基类对象

如果在类层次结构中，基类和派生类之间存在多条路径，则会创建基类的多个对象，从而创建了其成员的多个拷贝。这可能并不理想。我们可以避免这种情况吗？我们稍后会回答，首先考虑以下程序：

```cpp
#include <iostream> // Example 21.5
using std::cout;
```

```cpp
class A {
private:
  int r;
public:
  A(int k) : r(k) { cout << " A()"; };
  virtual ~A() { cout << " ~A()"; };
  void show_A() const { cout << " A:" << r; }
};
```

```cpp
class B : public A {
private:
  int t;
public:
  B(int m) : A(m), t(m) { cout << " B()"; };
  ~B() { cout << " ~B()"; };
  void show_B() const;
};
```

```cpp
void B::show_B() const {
  cout << " B:" << t;
  show_A();
}
```

```cpp
class C : public A
{
private:
public:
    int v;
    C(int p) : A(p), v(p) { cout << " " C C(); };
    ~C() { cout << " " "~C()"; }
    void show_C() const;
};
```

```cpp
void C::show_C() const
{
    cout << " C:" << v;
    show_A();
}
```

```cpp
class BC : public B, public C
{
private:
    int z;
public:
    BC(int x) : B(x), C(x+1), z(2*x) { cout << " BC()" << "\n"; };
    ~BC() { cout << " ~BC()"; };
    void show_BC() const { cout << " BC:" << z << "\n"; }
};
```

```cpp
int main()
{
    BC bc(10);

    bc.show_B();
    bc.show_C();
    bc.show_BC();
    return 0;
}
```

B 类和 C 类派生自 A 类。BC 类派生自这两个类。我让构造函数带有参数，以便我们记住派生类的构造函数可以向基类的构造函数传递值。当 BC 对象被创建时，基类的构造函数被调用：

```cpp
BC(int x) : B(x), C(x+1), z(2*x) { cout << " BC()" << "\n"; };
```

首先回想，如示例 C20.4 的类层次结构所示，派生类的构造函数可以调用其直接基类的构造函数。该规则的例外是虚基类，我们将在下文中看到。现在，让我们 BC 构造函数。它调用 B 类和 C 类的构造函数并传递值 10。相应的，创建 A 类的第一个子对象，x 变为 10。然后，创建 C 类的构造函数并将值 11 传递给它。它调用 A 类的构造函数并向其传递相同的值。因此，创建了第二个 A 类子对象，x 变为 11。然后，创建 C 类的子对象，v 变为 11。总结来说，bc 对象包含了两个 A 类子对象、一个 B 类子对象和一个 C 类子对象。

通过多重继承，派生类对象包含其每个基类对应的一个子对象。

## 700 C++ 简介

## 正如我们所说，基类对象的构造顺序是从左到右的，基类出现在类的声明中（例如 `public B, public C`）。构造函数在初始化列表中出现的顺序并不重要。但是，如果我们改变顺序并写道：

```cpp
BC(int x) : C(x+1), B(x), z(2*x) {cout << " BC()\n";};
```

B 类的构造函数将再次被首先调用，然后是 C 的。
c.show_B() 调用 B 类的 show_B()。它显示 t 的值并调用其自身子对象的 show_A()。同样，show_C() 调用 C 类的 show_C()，它显示 v 的值并调用其自身子对象的 show_A()。析函数的调用顺序与构造函数的调用顺序相反。最后，程序显示：

```
A() B() A() C() BC()
B:10 A:10 C:11 A:11 BC:20
-BC() -C() -A() -B() -A()
```

正如你所猜的，这种重复的继承会导致重复和歧义。例如，我们写道：

```cpp
bc.show_A();
```

不，编译器将显示一条类似于 `BC::show_A() is ambiguous` 的错误信息。这是因为有两个 A 类子对象，编译器无法选择用于显示 `show_A()` 的对象。是在 B 类的 A 子对象中，还是在 C 类的 A 子对象中？在示例中，我通过通过 B 和 C 子对象的函数来调用 `show_A()` 跳过了这个问题。因此，编译器将显示包含在每个类中的 A 子对象的 `show_A()`。正如我们所知，另一种方法是使用 `::` 作用域解析符并指定我们想要的 A 子对象。例如：

```cpp
bc::show_A(); /* 调用了 B 类 A 子对象的 show_A() */ */
c::show_A(); /* 调用了 C 类 A 子对象的 show_A() */ */
```

## 多个基类对象与问题

 让我们来看一个更真实的例子，涉及多个基类对象的构造以及可能出现的问题。这次我不会选择 `show_names`（例如 `show_A`），这是一个简单的情况，因为很清楚将调用哪个 show，但我将选择相同的名称 `show()` 并使用虚函数来实现多态。程序定义了 `Person` 类并用它派生出 `Programmer` 和 `Author` 类。`ProAuth` 类派生自这两个类。本质上，该程序似乎是一个程序员和一个作家。

```cpp
#include <iostream> // Example 21.6
#include <string>
using std::cout;
using std::cin;
using std::string;
```

```cpp
class Person
private:
  string name;
  int code;
public:
  Person() {name = "None"; code = 0;}
  Person(string n, int c) : name(n), code(c) {}
  virtual ~Person() {}
  virtual void show() const { cout << "Name:" << name << " Code:" << code; }
};
```

```cpp
class Programmer : public Person
private:
  string cmp;
public:
  Programmer() : Person() {cmp = "None";}
  Programmer(string n, int c, string s) : Person(n, c), cmp(s) {}
  void show() const override;
};
```

```cpp
void Programmer::show() const {
  Person::show();
  cout << " Company:" << cmp;
}
```

```cpp
class Author : public Person
private:
  int titles;
public:
  Author() : Person() {titles = 0;}
  Author(string n, int c, int t) : Person(n, c), titles(t) {}
  void show() const override;
};
```

```cpp
void Author::show() const {
    Person::show();
    cout << " Titles:" << titles;
}
```

```cpp
class ProgAuth : public Programmer, public Author
private:
    int z;
public:
  ProgAuth() : Programmer(), Author() {z = 0;}
  ProgAuth(string n, int c, string s, int t, int z) : Programmer(n, c, s), Author(n, t), z(z) {}
  void show() const override;
};
```

```cpp
int main() {
    Person *p[3];
    Programmer per("First", 1, "Net");
    Programmer pro("Second", 2, "Any");
    Author auth("Third", 3, 5);

    p[0] = &per;
    p[1] = &pro;
    p[2] = &auth;

    for (int i = 0; i < 3; i++) {
        p[i]->show();
        cout << endl;
    }
    return 0;
}
```

输出如下：
```
Name:None Code:0 Name:First Code:1 Company:Net
Name:None Code:0 Name:Second Code:2 Company:Any
Name:None Code:0 Name:Third Code:3 Titles:5
Name:First Code:1 Company:Net
Name:Second Code:2 Company:Any
Name:Third Code:3 Titles:5
```

上面的代码展示了虚函数的作用。如果基类的 `show()` 没有声明为 `virtual`，那么当以下代码时会发生什么：

```cpp
ProgAuth pro_auth;
pro_auth.show(); // 编译错误。
```

当 `pro_auth` 对象被创建时，调用了四个构造函数。具体来说，`ProgAuth` 对象的构造函数调用了 `Programmer` 和 `Author` 构造函数来创建相应的子对象，以及 `Person` 和 `Author` 构造函数来创建相应的子对象，每个 `Author` 类子对象包含了两个 `Person` 类子对象。如果 `show()` 在基类中没有声明为虚，编译器将检查 `p` 数组的类型并三次调用 `Person::show()`。

到为止，这个程序是展示虚函数的另一个例子。

