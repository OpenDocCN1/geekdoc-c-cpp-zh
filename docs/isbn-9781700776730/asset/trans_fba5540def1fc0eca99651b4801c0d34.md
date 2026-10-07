
派生类可以通过以下形式访问基类的成员函数：

```
int x = obj.getDependent();
```

或者使用作用域解析运算符：

```
obj.Employee::display();
```

请注意，当基类和派生类中的函数具有相同名称时，需要使用作用域解析运算符。同样注意，派生类可以作为其派生类的基类，从而允许你创建派生类的层级结构。

## 类层次结构

在之前的示例中，继承被用于为现有类添加功能。让我们来看一个继承用于不同目的的示例，即作为程序原始设计的一部分。

我们的示例模拟了一个小部件公司员工的数据库。在这家公司，有三种类型的员工：

- 经理（Managers）——管理其他员工
- 科学家（Scientists）——进行研究以开发更好的小部件
- 工人（Laborers）——操作危险的小部件冲压机

数据库存储所有员工的姓名和员工 ID，无论他们属于哪种类别。

- 对于经理，还存储了他们的职称和高尔夫俱乐部会费。
- 对于科学家，存储了他们发表的学术论文数量。
- 工人除了姓名和 ID 号外不需要额外数据。

我们的程序设计将从一个基类 `Employee` 开始，它处理员工的姓和 ID 号。从该类将派生出另外三个类：`Manager`、`Scientist` 和 `Laborer`。

![](img/88ecbb96455b36fdc78e686bde4f5234_333_0.png)

`Manager` 和 `Scientist` 类包含了关于此类类别员工的额外信息以及处理这些信息的成员函数。

```cpp
// hier.cpp
#include <iostream>

class Employee {
private:
    char name[81];
    long id;
public:
    void getData() {
        cout << "Enter last name: " << cin >> name;
        cout << "Enter ID: " << cin >> id;
    }
    void putData() {
        cout << "Name: " << name << endl;
        cout << "ID: " << id << endl;
    }
};

class Manager : public Employee {
private:
    char title[81];
    double dues;
public:
    void getData() {
        Employee::getData();
        cout << "Title: " << cin >> title;
        cout << "Golf Club Dues: " << cin >> dues;
    }
    void putData() {
        Employee::putData();
        cout << "Title: " << title << endl;
        cout << "Golf Club Dues: " << dues << endl;
    }
};

class Scientist : public Employee {
private:
    int pubs;
public:
    void getData() {
        Employee::getData();
        cout << "Number of Publications: " << cin >> pubs;
    }
    void putData() {
        Employee::putData();
        cout << "Number of Publications: " << pubs << endl;
    }
};

class Laborer : public Employee {
};
```

注意，`Laborer` 类运行方式与 `Employee` 类相同，因为它不包含任何额外的数据或函数。`Laborer` 类似乎是没必要的，但通过将其作为一个独立的类，我们强调了所有类都派生自同一个源 `Employee`。

创建表面上空的 `Laborer` 类的另一个原因是考虑到维护问题。在将来，如果我们决定修改 `Laborer` 类，就不需要更改 `Employee` 的类型限定符。

仅用于派生其他类的类（例如 `Employee`）有时被称为抽象类（abstract classes），这意味着不会创建此类类的实际实例（对象）。“抽象”一词有一个更精确的定义，与多态和虚拟函数有关，我们稍后会遇到这些。

## 继承层级

类可以派生自本身已经是派生类的类。考虑下面的类层次结构：

```cpp
class A {
};
class B : public A {
};
class C : public B {
};
```

在这里，类 `B` 派生自类 `A`，类 `C` 派生自类 `B`。这个过程可以扩展到任意层级。

通过这种方式，我们可以扩展 `Employee` 类程序，添加一种名为工头（foreman）的特殊工人。由于工头是一种工人，`Foreman` 类将派生自 `Laborer` 类。

工头监督小部件冲压操作，指导工人小组。他们负责他们所在小组的小部件生产配额。工头的能力通过成功完成配额的百分比来衡量。因此，我们在 `Foreman` 类中有一个代表此百分比的配额数据项：

```cpp
class Foreman : public Laborer {
private:
    float quotas;
public:
    void getData() {
        Laborer::getData();
        cout << "Enter quotes: " << cin >> quotas;
    }
    void putData() {
        Laborer::putData();
        cout << "Quotas: " << quotas << endl;
    }
};
```

![](img/88ecbb96455b36fdc78e686bde4f5234_336_0.png)

注意，类层次结构不是组织架构图。组织架构图显示的是命令链。类层次结构是共同特征的泛化。类越通用，它在图中的位置越高！因此，`Laborer` 比 `Foreman` 更通用，后者是专门的 `Laborer`。所以在类层次结构中，`Laborer` 显示在 `Foreman` 之上。

## 访问机制

### 使用派生类实例访问基类成员
派生类的实例对基类的公共成员（通常是函数）具有完全访问权限。假设派生类作用域内不存在同名的成员，则将自动使用基类的成员。

```cpp
// derived.cpp
class Base {
protected:
    int num;
public:
    Base(int n = 0) : num(n) {}
    int getNum() const { return num; }
};

class Derived : public Base {
};

int main() {
    Derived d;
    cout << d.getNum(); // 第一次调用检查 Derived
    // 然后是 Base
    cout << d.Base::getNum(); // 第二次调用直接访问 Base
    return 0;
}
```

### 覆盖类数据成员
除了创建与基类名称不同的成员外，派生类还可以选择性地覆盖现有名称。这是通过在派生类中声明与基类名称相同的来实现来实现。也就是说，如果派生类的实例或成员函数引用了已覆盖的基类数据成员，默认将使用派生类的成员。

```cpp
// base.cpp
class Base {
protected:
    int num;
public:
    Base(int n = 0) : num(n) {}
    int getNum() { return num; }
};

class Derived : public Base {
private:
    int num;
public:
    Derived(int n = 1) : num(n) {}
    int getNum() { return num + 1; }
};

int main() {
    Derived d;
    cout << d.getNum() << endl; // 输出 2
    cout << d.Base::getNum() << endl; // 输出 0
    return 0;
}
```

### 覆盖成员函数
我们还可以覆盖基类的成员函数。我们可以在派生类中使用与基类名称相同的函数。你可能希望这样做，以便程序对基类和派生类对象的调用方式是一样的。

考虑以下 `Stack` 类：

```cpp
// stack.cpp
const int MAX = 100;

class Stack {
protected:
    int s[MAX];
int top;
public:
    Stack() { top = -1; }
    void push(int num) { s[++top] = num; }
    int pop() { return s[top--]; }
};
```

这里有一个潜在的缺陷。没有溢出或下溢的检查。

为了修复这些缺陷，我们将创建一个自 `Stack` 的新类 `Stack2`。

```cpp
class Stack2 : public Stack {
public:
    void push(int num) {
        if (top < MAX-1)
            Stack::push(num);
        else {
            cout << "Stack overflow.";
            exit(1);
        }
    }
    int pop() {
        if (top > 0)
            return Stack::pop();
        else {
            cout << "Stack underflow.";
            exit(1);
        }
    }
};
```

