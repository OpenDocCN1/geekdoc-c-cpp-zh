

```cpp
void right(double angle){
    t.right(angle);
}
void left(double angle){
    t.left(angle);
}
// similar forwarding code for other functions allowed on Turtle.
```

正如你所见，在 mTurtleC 中我们有一个 Turtle 对象，你将在屏幕上看到它，还有一个成员 distance 用于跟踪乌龟移动了多少距离。显然，当创建 mTurtleC 时，我们应该将 distance 设置为 0，这正是上面的构造函数所做的。构造函数似乎对成员 t 没有做太多事情。但你知道成员 t 也会被创建，使用默认的 Turtle 构造函数。因此乌龟会出现在屏幕上。mTurtleC 中的成员函数 forward 会更新 distance，并使乌龟移动。最后，成员函数 distanceCovered 会按预期打印 distance。

right 的代码很简单，我们只需在成员 t 上调用函数 right，并使用相同的参数。我们将不得不为其他函数如 left、hide 等编写这样的转发函数。

显然，这将使我们能够编写前面给出的主程序；我们只需要在其中使用 mTurtleC 代替 mTurtle 即可。解决方案相当令人满意，主要缺点是需要编写转发函数。

## 23.1.2 使用继承的实现

使用继承，我们可以更紧凑地定义一个计量乌龟，如下所示。我们将这个类称为 mTurtleI。

```cpp
class mTurtleI : public Turtle{ // solution with inheritance
    float distance;
public:
    mTurtleI(){
        distance = 0;
    }
    void forward(float d){
        distance += abs(d);
        Turtle::forward(d);
    }
    float distanceCovered(){
        return distance;
    }
};
```

我们很快会解释每一行做了什么。现在我们只指出，这基本上会做第 23.1.1 节代码所做的事情。有了它，我们将能够运行第 23.1 节开头给出的主程序，当然我们需要在主程序中使用 mTurtleI 代替 mTurtle。

注意我们没有定义诸如 right 的函数。我们也没有显式定义类型为 Turtle 的成员 t。正如我们接下来将看到的，这些都是继承而来的！

## 23.2 一般原则

一般来说，我们可以通过编写以下内容将类 B 定义为现有类 A 的子类：

```cpp
class B : type-of-inheritance A {
    // body describes how B is different from A
};
```

其中，type-of-inheritance 可以是 public、private 或 protected。我们从 public 继承开始讨论，这是我们在上一节的类 mTurtleI 中使用的方式。我们将在第 23.7 节讨论其他类型的继承。

注意，名称 A 必须在我们定义 B 时已经定义。这通常通过包含 A 的头文件来实现。

上面的定义将创建一个类 B，它首先拥有 A 的所有数据成员和函数成员，除了构造函数和析构函数。如果我们希望 B 具有一些额外的数据或函数成员，我们可以在正文中定义它们。我们也可以重新定义 A 中已有的一些函数——对于类 B 的对象将使用新的定义。我们接下来讨论细节。

正如我们所说，A 中存在的数据成员也将出现在 B 的对象中。它们会单独出现，即我们可以按照我们很快讨论的一些规则直接访问它们。然而，我们也可以认为继承的成员共同构成了一个类 A 的继承对象，位于每个类 B 的对象内部。此外，我们可以通过在类 B 的定义正文中定义它们来拥有新的数据成员。

因此，对于第 23.1.2 节的类 mTurtleI，我们将得到继承的对象和新的数据成员 distance。正如你可能猜到的，一个 Turtle 对象将包含许多数据成员，例如一个成员 color（类型为 Color）保存乌龟颜色的信息。这些都包含在 mTurtleI 中。图 23.1(a) 显示了为类 mTurtleI 生成的对象的 contents。为了比较，在图 23.1(b) 中，我们也显示了一个类型为 mTurtleC 的对象的 contents。类 mTurtleC 的一个对象有两个数据成员，一个是 double 类型的成员 distance，一个是 Turtle 类型的成员 t。因此图 23.1 中的两个对象实际上包含相同的信息。主要区别在于，在 mTurtleC 中，被包含的乌龟对象 t 的成员如 color 不能直接访问，而在 mTurtleI 中，这些成员可以直接访问。

![](img/c7233aedab7e4c7cad32a7615b6a4783_390_0.png)

(a) mTurtleI 对象

(b) mTurtleC 对象

图 23.1：类 mTurtleI 和类 mTurtleC 对象的 contents

新的定义被称为覆盖旧的定义，并将用于类 B 的对象。A 中的 f 的定义将继续用于类 A 的对象。类 B 的实例如果必要也可以使用来自 A 的旧定义。只是，为此需要一种稍微复杂的语法。不要只使用函数 f 的名称，我们必须写 A::f。

我们在第 23.1.2 节中对 mTurtleI 的定义中看到了所有这些的例子。我们定义了一个新的成员函数 distanceCovered，它不存在于超类 Turtle 中，但对类 mTurtleI 来说是特殊的。我们还重新定义了 Turtle 中存在的成员函数 forward。新的函数适当地更改 distance 成员，并使用语法 Turtle::forward 调用类 Turtle 中的函数 forward。你可以将此函数视为在 mTurtleI 内部的继承 Turtle 对象上调用。

注意，虽然类 B 的对象继承了 A 的所有数据成员，但它们的访问性是有限的。事实上，继承的函数成员的访问性也是有限的。我们接下来讨论其精确规则。

### 23.2.1 访问规则和 protected 成员

假设 m 是 A 的数据或函数成员，b 是 B 的一个实例，B 是 A 的子类。那么实例 b 的成员 m 的访问方式由以下规则决定。

- **情况 1：m 是 A 的 public 成员：** 在这种情况下，我们可以认为 m 也是 B 的 public 成员。换句话说，m 可以在 B 的定义内部访问，也可以在 B 的定义外部访问。

- **情况 2：m 是 A 的 private 成员：** 那么 m 不能在我们编写的 B 的定义内部的代码中访问。当然它也不能在外部访问。换句话说，private 成员只能在成员被定义的类（及其友元类）的定义内部访问。子类实例不能直接访问超类的 private 成员。这并不意味着超类的 private 成员是无用的。A 中可能有一个 public 或 protected（见下文）成员函数 f 引用了 m。现在，B 中的代码可以引用 f，从而间接引用 m。

- **情况 3：m 是 A 的“protected”成员：** protected 的概念如下。如果类 A 的一个成员被指定为 protected，那么它只能在 A 的定义或其子类的定义内部访问。换句话说，protected 成员比 public 成员（可在任何地方访问）访问性更低，比 private 成员（只能在 A 的定义中访问）访问性更高。注意 m 也应被视为 B 的 protected 成员。

我们用以下代码片段说明上述规则。

```cpp
class A{
private:
    int p;
protected:
    int q;
    int getp(){return p;}
public:
    int r;
    void init(){p=1; q=2; r=3;}
};

class B: public A{
    double s;
public:
    void print(){
        cout << p << endl;  // compiler error 1.  p is private.
        cout << q << ", "
             << r << ", "
             << getp() << endl;
    }
};

int main(){
    B b;
    b.init();
    cout << b.p        // compiler error 2.  p is private
         << b.q        // compiler error 3.  q is protected
         << b.r
         << b.getp()   // compiler error 4.  getp is protected.
         << endl;
    b.print();
}
```

如果你编译这段代码，你会得到标记的 4 个编译错误。编译错误 1 和 2 是因为 p 在 A 中是 private，因此不能在 B 的定义中访问，

