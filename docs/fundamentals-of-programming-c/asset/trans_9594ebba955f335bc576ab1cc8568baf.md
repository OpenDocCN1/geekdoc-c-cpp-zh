

## 17. 多态

你可能会认为，可以使编译器在所有情况下确定要调用的虚方法。在下面的代码中：

```cpp
Text t1("ABC\n");
FancyText t2("XYZ", "", "]", ":");
cout << t1.get() << " " << t2.get() << endl;
Text *p1, *p2;
p1 = &t1;
p2 = &t2;
cout << p1->get() << " " << p2->get() << endl;
```

编译器不能推断出 p2 的类型吗？因为 p2 被赋值指向 t2，而它知道 t2 的类型是 FancyText 了？

这种扩展的分析能力会进一步增加编译器的复杂度，而 C++ 编译器已经是相当复杂的软件了。尝试添加这种方法证明是徒劳的，因为编译器无法无法确定要调用哪种方法。要了解原因，请以下代码：

```cpp
Text *p;
if (std::rand() % 2 == 0)
    p = new Text("ABC");
else
    p = new FancyText("XYZ", "", "]", ":");
cout << p->get() << endl;
```

这段代码在运行时生成一个伪随机数。如果生成偶数，它引导 p 指向一个 Text 对象；否则，它引导 p 指向一个 FancyText 对象。这段代码将调用哪种方法，是 Text::get 还是 FancyText::get？由于代码在运行时生成伪随机数，编译器无法确定 p 指向的确切对象；编译器无法确定调用哪个 `get` 方法。然而，编译器可以生成代码，跳转到 p 关联虚表中对应于 `get` 方法索引的地址地址的方法。

列表 17.3 (vtables.cpp) 展示了虚方法表指针在包含虚方法的对象内部占据了空间。

列表 17.3: vtables.cpp

```cpp
#include <iostream>
using namespace std;
// 一个没有虚方法的类
class NoTable {
    int data;
public:
    void set(int d) { data = d; }
    int get() { return data; }
};

// 一个带有虚方法的类
class HasVTable {
    int data;
public:
```

## 17.4. 多态

```cpp
    virtual void set(int d) { data = d; }
    virtual int get() { return data; }

int main() {
    NoTable no_vtable;
    HasVTable has_vtable;
    no_vtable.set(10);
    has_vtable.set(10);
    cout << "no_vtable size = " << sizeof(no_vtable) << endl;
    cout << "has_vtable size = " << sizeof(has_vtable) << endl;
}
```

列表 17.3 (vtables.cpp) 的输出是

```
no_vtable size = 4
has_vtable size = 8
```

一个 NoTable 为其整数字段需要四个字节，而一个 HasVTable 对象占据八个字节——四个字节用于其整数字段，另外四个字节用于其秘密指针。

动态绑定实现了面向对象编程中一种强大的技术，称为多态。多态行为根据其被调用的对象的实际类型表现出不同的行为。考虑列表 17.4 (polymorphicvector.cpp)。

# 列表 17.4: polymorphicvector.cpp

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

// 所有 Text 生类的基类
class Text {
  string text;
public:
  Text(const string& t) : text(t) {}
  virtual string get() const {
    return text;
  }
};

// 为文本提供极少的装饰
class FancyText : public Text {
  string left_bracket;
  string right_bracket;
  string connector;
public:
  FancyText(const string& t, const string& left, const string& right, const string& conn)
    : Text(t), left_bracket(left), right_bracket(right),
      connector(conn) {
    string get() const override {
        return left_bracket + Text::get() + right_bracket;
    }
};
// 文本始终是单词 FIXED
class FixedText : public Text {
public:
    FixedText() : Text("FIXED") {}
};
int main() {
    vector<Text*> texts = { new Text("Wow"),
                               new FancyText("Wee", ":", "[", ":-"),
                               new FixedText,
                               new FancyText("Whoa", ":", ":", ":") };
    for (auto t : texts) {
        cout << t->get() << endl;
    }
}
```

我们从第 11.1 节知道，vector 是一个同质元素的集合。同质性意味着 vector 中的元素必须是相同类型。当涉及继承关系时，同质性具有更深层次的含义。列表 17.4 (polymorphicvector.cpp) 中 texts 的声明类型是 **vector<Text***。通过继承，texts 不仅持有指向简单对象的指针，同时还可以持有指向 FixedText 的指针。

