

## 函数符号的友元

有时友元允许比成员函数更明显的函数调用语法。例如，假设我们想要一个函数来将 Distance 对象加倍。使用成员函数，我们的类变为：

```cpp
#include <iostream>

using namespace std;

class Distance {
   private:
      int feet;
      float inches;
   public:
      void setDist(int ft, float in);
      void getDist();
      void showDist();
      void addDist(Distance d2, Distance d3);
      Distance addDist(Distance d);
      Distance doubleDist();
};

Distance::Distance(int ft, float in) {
   feet = ft;
   inches = in;
}

void Distance::setDist(int ft, float in) {
   feet = ft;
   inches = in;
}

void Distance::getDist() {
   cout << "feet: ";
   cin >> feet;
   cout << "inches: ";
   cin >> inches;
}

void Distance::showDist() {
   cout << feet << "\'" << inches << "\"";
}
```

```cpp
void Distance::addDist(Distance d2, Distance d3) {
  inches = d2.inches + d3.inches;
  feet = d2.feet + d3.feet;
  if (inches >= 12.0) {
    inches -= 12.0;
    feet++;
  }
}

Distance Distance::addDist(Distance d) {
  Distance temp;
  temp.inches = inches + d.inches;
  temp.feet = feet + d.feet;
  if (temp.inches >= 12.0) {
    temp.inches -= 12.0;
    temp.feet += 1;
  }
  return temp;
}

Distance Distance::doubleDist() {
  int ft = feet * 2;
  float in = inches * 2;
  if (in >= 12.0) {
    ++ft;
    in -= 12.0;
  }
  return Distance(ft, in);
}

int main() {
  Distance d1(3, 6.0), d2;
  d2 = d1.doubleDist();
  cout << "d2 = ";
  d2.showDist();
}
```

请注意：

```
d2 = d1.doubleDist();
```

运行良好，但我们可能希望使用与普通数字相同的语法来处理 `Distance` 对象：

```
d2 = doubleDist(d1);
```

我们可以通过将 doubleDist() 设为 Distance 类的友元来实现这一点：

```cpp
#include <iostream>

using namespace std;

class Distance {
private:
    int feet;
    float inches;
public:
    void setDist(int ft, float in);
    void getDist();
    void showDist();
    void addDist(Distance d2, Distance d3);
    Distance addDist(Distance d);
    friend Distance doubleDist(Distance d);
};

Distance::Distance(int ft, float in) {
    feet = ft;
    inches = in;
}

void Distance::setDist(int ft, float in) {
    feet = ft;
    inches = in;
}

void Distance::getDist() {
   cout << "feet: ";
   cin >> feet;
   cout << "inches: ";
   cin >> inches;
}

void Distance::showDist() {
   cout << feet << "\' " << inches << "\"";
}

void Distance::addDist(Distance d2, Distance d3) {
    inches = d2.inches + d3.inches;
    feet = d2.feet + d3.feet;
    if (inches >= 12.0) {
        inches -= 12.0;
        feet++;
    }
}
```

```cpp
Distance Distance::addDist(Distance d) {
  Distance temp;

  temp.inches = inches + d.inches;
  temp.feet = feet + d.feet;
  if (temp.inches >= 12.0) {
    temp.inches -= 12.0;
    temp.feet += 1;
  }
  return temp;
}

Distance doubleDist(Distance d) {
  int ft = d.feet * 2;
  float in = d.inches * 2;
  if (in >= 12.0) {
    ++ft;
    in -= 12.0;
  }
  return Distance(ft, in);
}

int main() {
  Distance d1(3, 6.0), d2;
  d2 = doubleDist(d1);
  cout << "d2 = " << d2.showDist();
}
```

在 main() 中，我们现在说：

```
d2 = doubleDist(d1);
```

注意：作为成员函数时 `doubleDist()` 不需要参数，而作为友元时它需要一个参数。

一般来说，函数的友元版本比成员函数版本多需要一个参数。

## 第 10 章 引用

### 引用变量

我们知道如何创建指针作为别名来寻址其他变量：

```cpp
int num = 5;
int *p = &num;
```

这声明了一个初始化为 5 的 int 变量 num 和一个指向 num 地址的 int 指针 p。

```cpp
cout << num << *p << endl; // 5 5
```

要使用指针寻址的值需要解引用指针，这会导致许多星号，可能会使代码混乱。C++ 提供了一种称为引用的指针别名替代方案。引用有三种主要用途：

- 作为变量
- 作为函数参数
- 作为函数结果

### 引用变量

C++ 中的引用变量只是另一个变量的别名。别名只是另一个变量的另一个名称。这意味着每当使用别名时，实际操作的是别名所引用的变量。

例如：

```cpp
int num = 5;
int& val = num;
```

这设置了一个引用变量 val 并将其分配给现有变量 num。我们说 val 是 int 的引用。引用变量包含另一个变量的地址，就像指针一样。因此 val 拥有 num 的地址。

此时，被引用的位置有两个关联的名称：num 和 val。

```cpp
cout << num << val << endl; // 5 5
```

因为两个变量指向内存中的同一位置，所以它们实际上是同一个变量，因此输出相同的值。请注意，与指针不同，引用变量在使用时会自动解引用。因此不需要星号 *。

```cpp
++num;
cout << num << val << endl; // 6 6
+val;
cout << num << val << endl; // 7 7
```

对 num 所做的任何赋值都会通过 val 反映出来，对 val 所做的任何赋值都会通过 num 反映出来。对 val 的任何操作都与对 num 的操作具有完全相同的效果。

```cpp
int z = 100;
val = z;
cout << num << val << endl; // 100 100
```

这不会导致 val 引用 z，因为编译器始终会为你解引用地址。上述代码将把 z 的值复制到 num。

注意：一旦引用变量被初始化为某个现有值，只要引用变量仍在作用域内，就不能更改或重新分配给其他变量。但是，引用变量所指向的值始终可以更改。

#### 引用规则

创建引用变量时，必须始终用某个其他现有变量的名称对其进行初始化。这意味着引用必须在其声明中初始化：

```cpp
int& iref; // error
```

与可以声明为未初始化状态的指针不同，或者如果指针不寻址有效数据则设置为 NULL，引用必须始终引用一个对象。引用没有等效于 NULL 指针的东西。

引用在四种特殊情况下不需要预先初始化：

- 当声明为 extern 时
- 当用作函数参数时
- 当用作函数返回类型时
- 在类声明中

一些示例：

```cpp
int&    - reference to an int
int*&   - reference to a pointer to an int

int a[10];
int& last = a[9]; // last is an alias for a[9];
```

给对象命名的原因通常是它还没有名称。此示例将名称 last 附加到数组 a 的最后一个元素。如果即将多次使用 a[9]，可能会这样做。使用引用可以节省程序文本，也可能节省计算时间。

#### 引用的引用

如果引用变量是另一个引用变量的别名，它实际上引用的是第一个引用变量所引用的变量。例如，两个引用变量是内存中同一变量的别名。

```cpp
int num1 = 1;
int& num2 = num1; // num2 is an alias for num1
int& num3 = num2; // num3 is an alias for num2 which
// really means that num3 is an
// alias for num1
```

#### 引用变量的地址

我们可以证明引用变量不是内存中具有自己地址的独立实体。如果你获取引用变量的地址，你得到的只是它作为别名的那个变量的地址。

例如：

```cpp
#include <cstdio>

int main() {
    int num1;
    int num2 = num1;
    printf("%p %p", &num1, &num2); // FFFFFFFF FFFFFFFF
    return 0;
}
```

因此引用变量没有自己的唯一地址。

#### 引用变量毫无用处！

最后，引用变量通常毫无用处！！！

如果你已经有一个变量，对该变量的引用只会提供复杂性。现在你有两种方式来更改同一个变量。你从引用变量中一无所获。它听起来就像混乱一样，在决定必须使用引用变量之前，你应该仔细考虑。

引用最初是为参数传递和返回值而设计的，引用变量仅被包含为了语法完整性，而不一定是因为它们是个好主意。引用通常仅在用户定义的类类型上下文中才是必要的。

