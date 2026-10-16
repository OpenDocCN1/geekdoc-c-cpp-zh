

or graphically:

## Satellite Displayed

**Comm_sat** 除了为 **Comm_sat** 专门定义的操作之外，**Satellite** 和 **Displayed** 上的操作的并集也可以应用。例如：

```
void f(Comm_sat& s)
{
  s.draw(); // Displayed::draw()
  Pos p = s.center(); // Satellite::center()
  s.transmit(); // Comm_sat::transmit()
}
```

同样，**Comm_sat** 可以传递给期望 **Satellite** 的函数，也可以传递给期望 **Displayed** 的函数。例如：

```
void highlight(Displayed*);
Pos center_of_gravity(const Satellite*);

void g(Comm_sat * p) {
  highlight(p); // pass a pointer to the Displayed part of the Comm_sat
  center_of_gravity(p); // pass a pointer to the Satellite part of the Comm_sat
}
```

其实现显然涉及某种（简单的）编译器技术，以确保期望 **Satellite** 的函数看到的 **Comm_sat** 的部分与期望 **Displayed** 的函数所看到的部分不同。虚函数按通常方式工作。例如：

```
class Satellite {
public:
  virtual Pos center() const = 0; // center of gravity
  // ...
};

class Displayed {
public:
  virtual void draw() = 0;
  // ...
};

class Comm_sat : public Satellite, public Displayed { public:
  Pos center() const override;
  void draw() override;
  // ...
};

// override Satellite::center() // override Displayed::draw()
```

这确保了当 **Comm_sat** 被视为 **Comm_sat** 和 **Displayed** 时，分别会调用 **Comm_sat::center()** 和 **Displayed::draw()**。

为什么我不只是将 **Comm_sat** 的 **Satellite** 和 **Displayed** 部分完全

分开？我本可以定义 Comm_sat 拥有一个 Satellite 成员和一个 Displayed 成员。或者，我本可以定义 Comm_sat 拥有一个 Satellite_* 成员和一个 Displayed_* 成员，并让其构造函数建立适当的连接。对于许多设计问题，我会那样做。然而，启发此示例的系统建立在具有虚函数的 Satellite 类和（单独设计的）具有虚函数的 Displayed 类的思想之上。你通过派生提供自己的卫星和自己的显示对象。特别是，你必须重写 Satellite 虚成员函数和 Displayed 虚成员函数来指定你自己的对象的行为。这就是多重继承基类具有状态和实现时难以避免的情况。变通方法可能很痛苦且难以维护。

将两个原本无关的类通过多重继承“粘合”在一起作为第三个类的实现是粗糙的、有效的、相对重要但并不很有趣。基本上，它使程序员免于编写大量转发函数（以补偿我们只能重写基类中定义的函数这一事实）。该技术不会显著影响程序的整体设计，有时可能会与隐藏实现细节的愿望相冲突。然而，一种技术不必聪明才有用。

我通常更喜欢拥有单一的实现层次结构和（在需要时）提供接口的多个抽象类。这通常更灵活，并导致更容易演进的系统。然而，你并不总是能做到这一点——尤其是当你需要使用不想修改的现有类时（例如，因为它们是别人库的一部分）。

请注意，仅使用单继承时，程序员对实现类

Displayed 、 Satellite 和 Comm_sat 的选择将受到限制。Comm_sat 可以是 Satellite 或 Displayed，但不能同时是两者（除非 Satellite 派生自 Displayed 或反之亦然）。任一替代方案都涉及灵活性损失。

谁会想要一个 Comm_sat 类？与一些人的猜测相反，Satellite 示例是真实的。确实存在——也许仍然存在——一个按照此处描述多重实现继承的方式构建的程序。它用于研究涉及卫星、地面站等的通信系统的设计。事实上，Satellite 派生自一个早期的并发任务概念。给定这样的仿真，我们可以回答关于通信流量的问题，确定地面站被雷雨阻断时的适当响应，考虑卫星连接与地面连接之间的权衡等。

## 21.3.3 Ambiguity Resolution

两个基类可能具有同名的成员函数。例如：

```
class Satellite {
public:
virtual Debug_info get_debug();
// ...
```

```
};
class Displayed {
public:
virtual Debug_info get_debug();
//...
};
```

当使用 Comm_sat 时，这些函数必须消除歧义。这可以通过用其类名限定成员名来简单完成：

```
void f(Comm_sat& cs)
{
Debug_info di = cs.get_debug(); // error : ambiguous
di = cs.Satellite::get_debug(); // OK
di = cs.Displayed::get_debug(); // OK
}
```

然而，显式消除歧义很混乱，因此通常最好通过在派生类中定义新函数来解决此类问题：

```
class Comm_sat : public Satellite, public Displayed {
public:
Debug_info get_debug() // override Comm_sat::get_debug() and Displayed::get_debug()
{
Debug_info di1 = Satellite::get_debug();
Debug_info di2 = Displayed::get_debug();
return merge_info(di1,di2);
}
//...
};
```

派生类中声明的函数会覆盖其基类中同名同类型的所有函数。通常，这正是正确的做法，因为在单个类中使用相同名称表示不同语义的操作通常是不好的。虚函数的理想情况是，对函数的调用效果与使用哪个接口找到该函数无关（§20.3.2）。

在重写函数的实现中，通常有必要显式限定名称以获得来自基类的正确版本。限定名，例如 Telstar::draw，可以指在 Telstar 或其基类之一中声明的 draw。例如：

```
class Telstar : public Comm_sat {
public:
void draw()
{
Comm_sat::draw(); // finds Displayed::draw // ... own stuff ...
}
//...
};
```

or graphically:
Satellite Displayed
Comm_sat
Telstar

如果 Comm_sat::draw 没有解析为在 Comm_sat 中声明的 draw，编译器会递归地在其基类中查找；也就是说，它会查找 Satellite::draw 和 Displayed::draw，并在必要时在其基类中查找。如果恰好找到一个匹配，该名称将被使用。否则，Comm_sat::draw 要么未找到，要么不明确。

如果在 Telstar::draw() 中我写了 plain draw()，结果将是 Telstar::draw() 的“无限”递归调用。

我本可以写 Displayed::draw()，但如果有人添加了 Comm_sat::draw()，代码就会被微妙地破坏；通常最好引用直接基类而不是间接基类。我本可以写 Comm_sat::Displayed::draw()，但那会是冗余的。如果我写了 Satellite::draw()，结果将是错误，因为 draw 在类层次结构的 Displayed 分支上。

get_debug() 示例基本上假设 Satellite 和 Displayed 的至少某些部分是共同设计的。名称、返回类型、参数类型和语义完全匹配纯属偶然的可能性极低。更可能的是，类似的功能以不同方式提供，因此需要付出努力才能将其合并为可一起使用的东西。我们最初可能被提供两个我们无法修改的类 SimObj 和 Widget，我们不能完全修改它们，它们提供的东西也不完全是我们需要的，而且它们提供的东西是通过不兼容的接口提供的。在这种情况下，我们可能会将 Satellite 和 Displayed 设计为我们的接口类，为我们的更高层类提供“映射层”以使用：

## Section 21.3.3 Ambiguity Resolution 629

```
class Satellite : public SimObj {
// map SimObj facilities to something easier to use for Satellite simulation
public:
virtual Debug_info get_debug(); // call SimObj::DBinf() and extract information // ...
};
```

```
class Displayed : public Widget {
// map Widget facilities to something easier to use to display Satellite simulation results
public:
virtual Debug_info get_debug(); // read Widget data and compose Debug_info // ...
};
```

or graphically:
SimObj Widget
Satellite Displayed
Comm_sat
Telstar

有趣的是，这正是我们用来消除歧义的

