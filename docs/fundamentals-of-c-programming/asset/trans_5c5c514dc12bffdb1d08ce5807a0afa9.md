
IntPoint(int x, int y): x(x), y(y) {}
};

class Rectangle {
    IntPoint corner; // Location of the rectangle's lower-left corner
    int width; // The rectangle's width
    int height; // The rectangle's height

public:
    Rectangle(IntPoint pt, int w, int h):
        corner(pt.x < -100 ? -100 : (pt.x > 100 ? 100 : pt.x),
               pt.y < -100 ? -100 : (pt.y > 100 ? 100 : pt.y)),
        width(w < 0 ? 0 : w),
        height(h < 0 ? 0 : h) {}

    int perimeter() {
        return 2*width + 2*height;
    }

    int area() {
        return width * height;
    }

    int get_width() {
        return width;
    }

    int get_height() {
        return height;
    }

    // Returns true if rectangle r overlaps this
    // rectangle object.
    bool intersect(Rectangle r) {
        // Details omitted
    }

    // Returns the length of a diagonal rounded to the nearest
    // integer.
    int diagonal() {
        // Details omitted
    }

    // Returns the geometric center of the rectangle with
    // the (x,y) coordinates rounded to the nearest integer.
    IntPoint center() {
        // Details omitted
    }

    bool is_inside(IntPoint pt) {
        // Details omitted
    }
}

};
int main() {
    Rectangle rect1(IntPoint(2, 3), 5, 7),
                rect2(IntPoint(2, 3), 1, 3),
                rect3(IntPoint(2, 3), 15, 3),
                rect4(IntPoint(2, 3), 5, 3);
    std::cout << rect1.get_width() << '\n';
    std::cout << rect1.get_height() << '\n';
    std::cout << rect2.get_width() << '\n';
    std::cout << rect2.get_height() << '\n';
    std::cout << rect3.get_width() << '\n';
    std::cout << rect3.get_height() << '\n';
    std::cout << rect4.get_width() << '\n';
    std::cout << rect4.get_height() << '\n';
    std::cout << rect1.get_area() << '\n';
    std::cout << rect1.get_perimeter() << '\n';
    std::cout << rect2.get_area() << '\n';
    std::cout << rect2.get_perimeter() << '\n';
    std::cout << rect3.get_area() << '\n';
    std::cout << rect3.get_perimeter() << '\n';
    std::cout << rect4.get_area() << '\n';
    std::cout << rect4.get_perimeter() << '\n';
}

- (a) 程序输出什么？

- (b) 关于 Rectangle 对象的左下角，x 坐标允许的最小值和最大值是多少？y 坐标允许的最小值和最大值是多少？

- (c) Rectangle 对象的最小和最大宽度是多少？

- (d) Rectangle 对象的最小和最大高度是多少？

- (e) 当客户端尝试使用超出可接受范围的参数创建 Rectangle 对象时会发生什么？

- (f) 实现 diagonal 方法。

- (g) 实现 center 方法。

- (h) 实现 intersect 方法。

- (i) 实现 is_inside 方法。

- (j) 完成名为 corner 的以下函数：

IntPoint corner(Rectangle r ) {
    // Details go here
}

该函数返回传入的 Rectangle 对象 r 的左下角。你不得修改 Rectangle 类。

- (k)

9. 开发一个 Circle 类，如上述 Rectangle 类一样，提供计算周长和面积的方法。Rectangle 的实例变量不适用于圆；具体来说，圆没有角，也不需要指定宽度和高度。一个中心点和半径更自然地描述一个圆。适当地构建你的 Circle 类。

10. 根据上述问题中的 Rectangle 和 Circle 类，编写一个 encloses 函数：

```cpp
// Returns true if rectangle rect is large enough to
// completely enclose circle circ
bool encloses(Rectangle rect, Circle circ) {
// Details omitted
}
```

使其在圆 circ 的尺寸允许其完全放入矩形 rect 内时返回 true。如果 circ 太大，函数返回 false。rect 和 circ 的位置不影响结果。

11. 考虑以下 C++ 代码：

```cpp
class Widget {
int value;
public:
Widget();
Widget(int v);
int get();
void bump();
};
Widget::Widget() {
value = 40;
}
Widget::Widget(int v) {
if (v >= 40)
value = v;
else
value = 0;
}
int Widget::get() const {
return value;
}
void Widget::bump() {
if (value < 50)
value++;
}
int main() {
Widget w1, w2(5);
std::cout << w1.get() << '\n';
std::cout << w2.get() << '\n';
w1.bump(); w2.bump();
}
```

```cpp
std::cout << w1.get() << '\n';
std::cout << w2.get() << '\n';
for (int i = 0; i < 20; i++) {
    w1.bump();
    w2.bump();
}
std::cout << w1.get() << '\n';
std::cout << w2.get() << '\n';
}
```

- (a) 程序输出什么？

- (b) 如果 w1 是一个 Widget 对象，表达式 w1.get() 可以返回的最小值是多少？

- (c) 如果 w1 是一个 Widget 对象，表达式 w1.get() 可以返回的最大值是多少？

## 第 15 章

### 15.1 传递对象参数

回顾清单 14.5（simplerational.cpp）中的 print_fraction 函数：

```cpp
void print_fraction(SimpleRational f) {
 std::cout << f.get_numerator() << "/" << f.get_denominator();
}
```

请注意，该函数使用按值传递协议接受其参数 f。这意味着在执行以下客户端代码期间：

```cpp
SimpleRational my_rational(3, 4);
print_fraction(my_rational);
```

程序会创建一个新的 SimpleRational 对象（print_fraction 定义中的形式参数 f），并将实际参数 my_rational 的成员数据复制到 f 中。此时程序有两个 3/4 分数的副本：客户端在其变量 my_rational 中有一个 3/4 理性数对象，正在执行的 print_fraction 在其形式参数 f 中有一个 3/4 理性数对象。当 print_fraction 函数执行完毕后，形式参数 f 作用域结束，其内存被释放。函数返回给调用者，留下调用者的 3/4 理性数对象作为唯一剩余的对象。

尽管 SimpleRational 对象相对较小（在 Visual C++ 下为四个字节），但创建一个作为形式参数的新对象、将实际参数的内容复制到形式参数中，最后清理形式参数的整个过程，都是执行程序不必要的工作。

我们在第 11.1.4 节中指出，将 std::vector 对象声明为函数的 const 引用参数，既提供了按引用传递的效率，又提供了按值传递的安全性：

- 按引用传递的效率：函数通过对象在内存中的位置访问调用者的对象。按引用传递向函数发送一个内存地址。无需将对象的数据复制到函数中。

- 按值传递的安全性：由于形式参数被声明为 const，函数无法修改调用者的实际参数。

我们在第 13.3 节中重新探讨了针对 std::string 对象的按 const 引用传递这一概念。

结果表明，最好优先使用按 const 引用传递对象，而不是按值传递。这意味着以下函数应该替换原始的 print_fraction 函数：

```cpp
void print_fraction(const SimpleRational& f) {
    std::cout << f.get_numerator() << " / " << f.get_denominator();
}
```

重写 multiply 也是必要的。以下提供了新的实现：

```cpp
// Returns the product of two rational numbers
SimpleRational multiply(const SimpleRational& f1,
                        const SimpleRational& f2) {
    return {f1.get_numerator() * f2.get_numerator(),
            f1.get_denominator() * f2.get_denominator()};
}
```

在 multiply 的这个新版本中，const 引用参数避免了每次调用 multiply 时构造、成员数据复制和内存清理两个 SimpleRational 对象的操作。

如果对于对象类型按 const 引用传递是更好的方法，为什么 C++ 不自动为我们这样做？C++ 默认按值传递。这以牺牲某些类型的效率为代价，保证了所有类型的安全性。

什么时候对对象类型使用按值传递是合理的？调用者可以创建一个对象，然后将该对象的副本传递给一个函数，该函数会修改该对象并将修改后的版本返回给调用者。调用者随后可以同时拥有原始对象和函数返回的修改后的对象。通过按 const 引用传递也可以做到这一点，但需要多写一点代码。以下示例代码说明了这一点：

```cpp
SimpleRational zero1(const SimpleRational& f) {
    SimpleRational result(f); // Make a copy of parameter f
    result.set_numerator(0);
    return result;
}
```

```cpp
SimpleRational zero2(SimpleRational f) {
    // Just use f; it is a copy of the caller's actual parameter
    f.set_numerator(0);
    return f;
}
```

在这里，zero1 必须显式地将其形式参数复制到它最终将返回的新局部变量中。zero2 函数不需要复制其形式参数；其形式参数已经是调用者实际参数的副本。

调用者可以如下使用 zero1 和 zero2 函数：
