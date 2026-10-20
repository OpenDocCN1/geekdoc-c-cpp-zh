

```cpp
class Dog : public Animal {
public:
    void bark() {
        cout << "Dog is barking." << endl;
    }
};
```

在此示例中，`Dog` 是一个派生类，它继承了基类 `Animal` 的 `eat` 函数。这种关系使得 `Dog` 既能使用 `Animal` 的现有功能，又能引入自身独有的行为。

多态性允许将不同类型的对象视为公共类型的对象。这是通过两种机制实现的：函数重载和虚函数。

## 函数重载

```cpp
class Calculator {
public:
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
};
```

在这里，`add` 函数被重载，以处理整数和浮点数的加法。编译器会根据传入参数的类型选择适当的版本。

## 虚函数

```cpp
// Base class with a virtual function
class Shape {
public:
    virtual void draw() {
        cout << "Drawing a shape." << endl;
    }
};

// Derived class overriding the virtual function
class Circle : public Shape {
public:
    void draw() override {
        cout << "Drawing a circle." << endl;
    }
};
```

在这个例子中，`Shape` 类有一个虚函数 `draw`，而 `Circle` 类对该函数进行了重写。这实现了动态绑定，从而能够根据对象的实际类型调用正确的函数。

## 优点与注意事项

继承和多态促进了代码复用、可扩展性，并能更自然地表示现实世界中的关系。然而，不当使用继承可能会导致歧义和维护困难，例如多重继承场景中的“菱形问题”。

## 封装与抽象：保护并简化复杂性

封装和抽象是面向对象编程（OOP）中的基本概念，它们有助于创建健壮、模块化且易于理解的代码。它们在管理软件系统的复杂性方面发挥着关键作用。

### 封装：数据隐藏与访问控制

封装将数据（属性）和操作这些数据的方法（函数）捆绑到一个称为类的单一单元中。它促进了数据隐藏的概念：类的实现细节对外部世界隐藏，对内部状态的访问通过公共接口进行控制。

```cpp
class BankAccount {
private:
    double balance;

public:
    // Public member functions for controlled access
    void deposit(double amount) {
        // Implementation details
        balance += amount;
    }

    void withdraw(double amount) {
        // Implementation details
        if (amount <= balance) {
            balance -= amount;
        } else {
            cout << "Insufficient funds." << endl;
        }
    }

    double getBalance() const {
        // Accessor function for read-only access
        return balance;
    }
};
```

在此示例中，`balance` 数据成员是私有的，只能通过受控的成员函数（如 `deposit`、`withdraw` 和 `getBalance`）来访问。这种封装保护了内部状态，并确保对它的修改经过了适当的验证。

### 抽象：管理复杂性

抽象通过基于现实世界实体建模类，并关注基本属性和行为，来简化复杂系统。它让程序员能够处理高层概念，而无需深入实现细节。

```cpp
class Shape {
public:
    // Pure virtual function for abstraction
    virtual void draw() const = 0;
};
```

在此示例中，`Shape` 类是一个表示通用形状的抽象。通过声明纯虚函数 `draw`，该类变为抽象类，其派生类（如 `Circle`、`Rectangle`）必须提供具体的实现。这允许进行高层建模，而无需在需要之前指定每个形状的细节。

### 优点与注意事项

封装和抽象提供了多个优点：

- **模块化**：封装允许创建自包含且模块化的单元，使代码更易于管理和维护。
- **安全性**：封装保护对象的内部状态，防止意外访问和修改。
- **灵活性**：抽象让程序员能够处理高层概念，促进代码适应不断变化的需求。

然而，需要保持平衡，因为过度使用抽象可能导致类层次结构过于复杂，使代码难以理解。

析构函数是一种特殊的成员函数，其名称与类名相同，前面带有波浪号（~）。当对象超出作用域或被显式删除时，析构函数会自动调用。析构函数对于释放与对象关联的资源（如释放内存或关闭文件）至关重要。

```cpp
class BankAccount {
public:
    // Constructor
    BankAccount() {
        balance = 0.0;
        cout << "BankAccount object created." << endl;
    }

    // Destructor
    ~BankAccount() {
        cout << "BankAccount object destroyed." << endl;
    }

    // Member function to display balance
    void displayBalance() {
        cout << "Balance: " << balance << endl;
    }

private:
    double balance;
};
```

在此示例中，`BankAccount` 类有一个构造函数来初始化余额，以及一个析构函数在对象销毁时打印一条消息。

## 隐式与显式构造函数调用

构造函数可以在创建对象时被隐式调用，也可以被显式调用。显式调用在需要动态内存分配或额外设置的场景中非常有用。

```cpp
Car myCar;    // Implicit call to the default constructor
Car anotherCar("Toyota", 2022);  // Explicit call to the parameterized constructor

BankAccount* accountPtr = new BankAccount();  // Explicit dynamic object creation
delete accountPtr;  // Explicit call to the destructor
```

## 拷贝构造函数

拷贝构造函数是一种特殊构造函数，它通过复制另一个对象的内容来创建一个新对象。当对象按值传递、按值返回或显式复制时，就会调用拷贝构造函数。

```cpp
class Student {
public:
    // Copy constructor
    Student(const Student& other) {
        this->name = other.name;
        this->age = other.age;
        cout << "Copy constructor called." << endl;
    }

    // Constructor
    Student(string name, int age) : name(name), age(age) {
        cout << "Student object created." << endl;
    }

    // Destructor
    ~Student() {
        cout << "Student object destroyed." << endl;
    }

private:
    string name;
    int age;
};
```

在此示例中，`Student` 类有一个拷贝构造函数，它通过复制另一个 `Student` 对象的数据来创建新对象。

## 运算符重载：扩展语言的词汇表

C++ 中的运算符重载允许用户自定义的类为标准运算符定义自身行为。此功能通过使类能够与运算符无缝协作来增强其表现力，从而使代码更直观、更易读。

### 重载一元运算符

一元运算符只作用于一个操作数。要重载一元运算符，请为该类定义一个成员函数，使用 `operator` 关键字后跟要重载的运算符。

```cpp
class ComplexNumber {
public:
    double real;
    double imag;

    // Overloading the unary minus (-) operator
    ComplexNumber operator-() const {
        ComplexNumber result;
        result.real = -real;
        result.imag = -imag;
        return result;
    }
};
```

在此示例中，一元负号运算符（-）被重载，用于对复数的实部和虚部取反。

### 重载二元运算符

二元运算符作用于两个操作数。要重载二元运算符，请为该类定义一个成员函数，使用 `operator` 关键字和两个参数。

```cpp
class Point {
public:
    double x;
    double y;

    // Overloading the binary plus (+) operator
    Point operator+(const Point& other) const {
        Point result;
        result.x = x + other.x;
        result.y = y + other.y;
        return result;
    }
};
```

在此示例中，二元加号运算符（+）被重载，用于将两个点相加。

### 重载比较运算符

比较运算符（`==`、`!=`、`<`、`>`、`<=`、`>=`）可以被重载，以定义用户自定义类型的自定义比较逻辑。

```cpp
class Date {
public:
    int day;
```

