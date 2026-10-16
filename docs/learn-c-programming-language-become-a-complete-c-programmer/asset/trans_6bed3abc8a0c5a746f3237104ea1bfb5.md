

如同抽象类常见的那样，Container 没有构造函数。毕竟，它没有任何数据需要初始化。另一方面，Container 却有一个析构函数，而且该析构函数是虚函数。同样，这对于抽象类来说也很常见，因为它们通常是通过引用或指针来操作的，而通过指针销毁一个 Container 的人并不知道其实现拥有何种资源；另见 §3.2.4。

一个实现了抽象类 Container 定义的接口所需函数的容器可以使用具体的类 Vector：

```
class Vector_container : public Container { // Vector_container implements Container
Vector v;
public:
Vector_container(int s) : v(s) { } // Vector of s elements
~Vector_container() {}

double& operator[](int i) { return v[i]; }
int size() const { return v.size(); }
};
```

`:public` 可以读作“派生自”或“是…的子类型”。类 Vector_container 被称为派生自类 Container，而类 Container 被称为类 Vector_container 的基类。另一种替代术语分别称 Vector_container 和 Container 为子类和超类。派生类被说成是从其基类继承成员，因此使用基类和派生类通常被称为继承。

成员 `operator[]()` 和 `size()` 被称为覆盖了基类 Container 中的对应成员 (§20.3.2)。析构函数 `~Vector_container()` 覆盖了基类析构函数 `~Container()`。请注意，成员析构函数 `~Vector()` 会被其类的析构函数 `~Vector_container()` 隐式调用。

对于像 `use(Container&)` 这样完全不了解实现细节而使用 Container 的函数，必然有其他函数来创建一个它可以操作的[content]

如同抽象类常见的那样，Container 没有构造函数。毕竟，它没有任何数据需要初始化。另一方面，Container 却有一个析构函数，而且该析构函数是虚函数。同样，这对于抽象类来说也很常见，因为它们通常是通过引用或指针来操作的，而通过指针销毁一个 Container 的人并不知道其实现拥有何种资源；另见 §3.2.4。

一个实现了抽象类 Container 定义的接口所需函数的容器可以使用具体的类 Vector：

```
class Vector_container : public Container { // Vector_container implements Container
Vector v;
public:
Vector_container(int s) : v(s) { } // Vector of s elements
~Vector_container() {}

double& operator[](int i) { return v[i]; }
int size() const { return v.size(); }
};
```

`:public` 可以读作“派生自”或“是…的子类型”。类 Vector_container 被称为派生自类 Container，而类 Container 被称为类 Vector_container 的基类。另一种替代术语分别称 Vector_container 和 Container 为子类和超类。派生类被说成是从其基类继承成员，因此使用基类和派生类通常被称为继承。

成员 `operator[]()` 和 `size()` 被称为覆盖了基类 Container 中的对应成员 (§20.3.2)。析构函数 `~Vector_container()` 覆盖了基类析构函数 `~Container()`。请注意，成员析构函数 `~Vector()` 会被其类的析构函数 `~Vector_container()` 隐式调用。

对于像 `use(Container&)` 这样完全不了解实现细节而使用 Container 的函数，必然有其他函数来创建一个它可以操作的
