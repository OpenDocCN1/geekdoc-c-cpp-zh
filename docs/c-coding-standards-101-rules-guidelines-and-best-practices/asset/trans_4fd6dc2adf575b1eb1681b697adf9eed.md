

## 52. 保持拷贝与析构的一致性。

### 摘要

你创建的东西，也要负责清理：如果你定义了拷贝构造函数、拷贝赋值运算符或析构函数中的任何一个，你可能需要定义另外两个中的一个或全部。

### 讨论

如果你需要定义这三个函数中的任何一个，这意味着你需要它执行超出默认行为的工作——而且这三个函数之间具有不对称的相互关联。具体如下：

- *如果你编写/禁用了拷贝构造函数或拷贝赋值运算符中的任意一个，你可能需要对另一个也做同样的事情：* 如果其中一个做了“特殊”工作，那么另一个很可能也应该做，因为这两个函数应当具有类似的效果。（参见第53条，该条单独详细阐述了这一点。）
- *如果你显式编写了拷贝函数，你可能需要编写析构函数：* 如果拷贝构造函数中的“特殊”工作是分配或复制某些资源（例如内存、文件、套接字），你需要在析构函数中释放它。
- *如果你显式编写了析构函数，你可能需要显式编写或禁用拷贝操作：* 如果你必须编写非平凡的析构函数，通常是因为你需要手动释放对象持有的资源。如果是这样，这些资源很可能需要仔细地复制，因此你需要关注对象被拷贝和赋值的方式，或者完全禁用拷贝。

在许多情况下，使用 RAII“拥有”对象来持有封装得当的资源，可以消除自己编写这些操作的需要。（参见第13条。）

优先使用编译器生成的特殊成员；只有这些成员才能被归类为“平凡的”，而且至少有一家主要的 STL 供应商会针对具有平凡特殊成员的类进行大力优化。这很可能成为普遍做法。

### 异常

当这些特殊函数中的任何一个仅被声明为 private 或 virtual，而没有特殊语义时，并不意味着需要其他特殊函数。

在少数情况下，含有奇怪类型成员（例如引用、**std::auto_ptr**）的类属于例外，因为它们具有特殊的拷贝语义。在持有引用或 **auto_ptr** 的类中，你可能需要编写拷贝构造函数和赋值运算符，但默认的析构函数已经能做正确的事情。（注意，使用引用或 **auto_ptr** 成员几乎总是错误的。）

### 参考文献

[*Cline99*] §30.01-14 • [*Koenig97*] §4 • [*Stroustrup00*] §5.5, §10.4 • [*SuttHysl04b*]

## 54. 避免切片。在基类中考虑使用 Clone 而不是拷贝。

### 摘要

切片面包很好，但切片对象可不好：对象切片是自动的、不可见的，并且很可能让美妙的多态设计戛然而止。在基类中，考虑禁用拷贝构造函数和拷贝赋值运算符，如果客户需要制作多态（完整、深）副本，则改为提供虚函数 **Clone**。

### 讨论

当你构建类层次结构时，通常目的是为了获得多态行为。你希望对象一旦创建，就能保持其类型和身份。这个目标与 C++ 通常的对象拷贝语义相冲突，因为拷贝构造函数不是虚函数，也无法成为虚函数。考虑以下代码：

```cpp
class B { /* ... */ };
class D : public B { /* ... */ };

void Transmogrify( B obj );             // oops: takes an object by value
void Transubstantiate( B& obj ) {        // ok: takes a reference
  Transmogrify( obj );                   // oops: slices the object
  // ...
}

D d;
Transubstantiate( d );
```

程序员的意图是以多态方式操作 **B** 及 **B** 派生对象。然而，由于失误（疲劳？咖啡因太少？），程序员要么忘记了在 **Transmogrify** 的签名中写上 **&**，要么想创建一个副本但方式不对。代码可以正常编译，但当 **Transmogrify** 被调用时，传入的 **B** 对象会（嗯，就是这样）变成一个 **B**。这是因为按值传递涉及对 **B::B( const B& )** 的调用，即 B 的拷贝构造函数，而传入的 **const B&** 会被自动转换为对 d 的引用。抹掉最初促使你使用继承的所有动态多态行为，这很可能不是你想要的。

如果你作为 **B** 的作者确实允许切片，但你不希望调用者轻易或意外地切片，这里有一个我们出于完整性而提及、但不建议在需要可移植的代码中使用的选项：你可以将 B 的拷贝构造函数设为 **explicit**。这有助于避免隐式切片，但也会阻止所有按值传递（这对于基类来说可能是好事，因为基类本来就不应该可实例化；参见第35条）：

```cpp
// Making the copy constructor explicit (has side effects, needs improvement)
class B { // ...
public:
    explicit B( const B& rhs );
};

class D : public B { /* ... */ };
```

调用代码如果确实想切片，仍然可以切片，但必须（嗯）明确地这样做：

```cpp
void Transmogrify( B obj );             // note: now can’t ever be called (!)

void Transmogrify2( const B& obj ) {    // an idiom to explicitly say “I want to take
    B b( obj );                          // obj by value anyway (and possibly slice it)”
    // ...
}

B b;                                    // base classes shouldn’t be concrete (see
D d;                                    // Item 35), but let’s imagine that B is

Transmogrify( b );                      // now an error (or should be; see note)
Transmogrify( d );                      // now an error (or should be; see note)
Transmogrify2( d );                     // ok
```

注意：在撰写本文时，一些编译器会错误地接受对 **Transmogrify** 的这两个调用中的一个或两个。这个惯用法是标准的，但（目前）还不是完全可移植的。

有一种更好的方法，可以以可移植的方式实现防止切片的目标，而且还能带来更多价值。假设像 **Transmogrify** 这样的函数确实希望获得一个完整的深拷贝，而无需知道传给它的对象的实际派生类型。更通用的惯用解决方案是将基类的拷贝构造函数设为 **protected**（这样像 **Transmogrify** 这样的函数就不会意外调用它），并改为依赖虚函数 **Clone**：

```cpp
// Adding Clone (first cut, better but still needs improvement)
class B { // ...
public:
    virtual B* Clone() const = 0;

protected:
    B( const B& );
};

class D : public B { // ...
public:
  virtual D* Clone() const { return new D(*this); }

protected:
  D( const D& rhs ) : B( rhs ) { /* ... */ }
};
```

现在，尝试切片将（可移植地）产生编译期错误，而将 Clone 设为纯虚函数会强制直接派生类覆盖它。不幸的是，这个解决方案仍然有两个编译器无法检测的问题：层次结构中更远层的派生类仍然可能忘记实现 Clone，而且对 Clone 的覆盖可能实现不当，导致副本与原始对象类型不同。Clone 应该应用非虚接口（NVI）模式（参见第39条），该模式将 Clone 的公共接口和虚性质分开，并让你能够植入一项有价值的断言：

```cpp
class B { // ...
public:
  B* Clone() const {                         // nonvirtual
    B* p = DoClone();
    assert( typeid(*p) == typeid(*this) && "DoClone incorrectly overridden" );
                                                // check DoClone’s returned type
    return p;
  }

protected:
  B( const B& );

private:
  virtual B* DoClone() const = 0;
};
```

现在，Clone 是所有调用代码使用的非虚接口。派生类只需要覆盖 DoClone。该断言将标记任何与原始对象类型不同的副本，从而表明某个派生类忘记覆盖 DoClone 函数；毕竟，断言正是用来报告此类编程错误的（参见第68和70条）。

### 异常

某些设计可能要求基类的拷贝构造函数保持 public（例如，当你的层次结构的一部分是第三方库时）。在这种情况下，优先通过（智能）指针传递，而不是通过引用传递；如第25条所示，通过指针传递不易受到切片和不必要的临时构造的影响。

### 参考文献

[Dewhurst03] §30, §76, §94 • [Meyers96] §13 • [Meyers97] §22 • [Stroustrup94] §11.4.4 • [Stroustrup00] §12.2.3

