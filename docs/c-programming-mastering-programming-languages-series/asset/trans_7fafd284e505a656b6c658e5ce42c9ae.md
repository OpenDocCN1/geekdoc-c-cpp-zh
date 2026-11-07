

```cpp
// Accessing the balance through a public member function
std::cout << "Current Balance: $" << myAccount.getBalance() << std::endl;

return 0;
}
```

在此示例中，BankAccount 类将余额封装为私有数据成员，确保通过公共成员函数进行受控访问。

## 继承：可重用性与层次结构

继承是一种机制，允许一个类从另一个类继承属性和行为。这促进了代码重用，并建立了层次结构。考虑以下示例：

```cpp
#include <iostream>

// Base class representing a Shape
class Shape {
public:
    virtual void draw() const {
        std::cout << "Drawing a shape." << std::endl;
    }
};

// Derived class Circle inheriting from Shape
class Circle : public Shape {
public:
    void draw() const override {
        std::cout << "Drawing a circle." << std::endl;
    }
};

int main() {
    // Creating objects of base and derived classes
    Shape genericShape;
    Circle myCircle;

    // Invoking draw functions
    genericShape.draw(); // Output: Drawing a shape.
    myCircle.draw();     // Output: Drawing a circle.

    return 0;
}
```

在此示例中，Circle 类继承自 Shape 类，通过重写的 draw 函数展示了继承和多态的概念。

## 多态：多种形态

多态允许将不同类的对象视为共同基类的对象。这一概念使函数能够处理各种派生类的对象，从而促进灵活性和可扩展性。考虑以下示例：

```cpp
#include <iostream>

// Base class representing an Animal
class Animal {
public:
    virtual void speak() const {
        std::cout << "Animal speaks." << std::endl;
    }
};

// Derived classes for specific animals
class Dog : public Animal {
public:
    void speak() const override {
        std::cout << "Dog barks." << std::endl;
    }
};

class Cat : public Animal {
public:
    void speak() const override {
        std::cout << "Cat meows." << std::endl;
    }
};

int main() {
    // Creating objects of base and derived classes
    Animal genericAnimal;
    Dog myDog;
    Cat myCat;

    // Invoking speak functions
    genericAnimal.speak();  // Output: Animal speaks.
    myDog.speak();          // Output: Dog barks.
    myCat.speak();          // Output: Cat meows.

    return 0;
}
```

```cpp
void displayInfo() {
    std::cout << "Title: " << title << ", Author: " << author << ", Year: " << year <<
        std::endl;
}
};

int main() {
    // Creating an object of the Book class
    Book myBook;

    // Accessing and setting data members
    myBook.title = "The Catcher in the Rye";
    myBook.author = "J.D. Salinger";
    myBook.year = 1951;

    // Invoking the member function to display information
    myBook.displayInfo();

    return 0;
}
```

在此示例中，Book 类封装了属性（title、author 和 year）以及行为（displayInfo）。myBook 对象是 Book 类的实例，体现了该类定义的属性和功能。

## 对象：类的实例

对象是类的实例，依据类提供的蓝图创建。每个对象都有自己的一组数据成员，并且可以调用其类中定义的成员函数。创建对象的过程通常称为实例化。在上面的示例中，myBook 是 Book 类的实例，表示一本具有独特属性和行为的特定书籍。

## 成员函数和数据成员

类中的成员函数定义了由该类创建的对象的行为。它们操作数据成员，提供了一种操作和交互对象内部状态的方式。在 Book 类示例中，displayInfo 是一个成员函数，用于将书籍信息打印到控制台。

## 访问修饰符：公共接口

访问修饰符（如 public、private 和 protected）定义了类成员的可见性和可访问性。Book 类示例中的 public 访问说明符允许从类外部访问数据成员和成员函数，便于与该类的对象进行交互。

理解 C++ 中类和对象的原则，为有效的面向对象编程奠定基础。通过类，开发者可以创建模块化、可重用且组织良好的代码结构，促进代码清晰性和可维护性。对象作为类的实例，允许实例化和使用已定义的蓝图，从而能够创建动态且灵活的软件系统。

## 封装与数据隐藏

封装是 C++ 中面向对象编程（OOP）的基石，是一种将数据和方法组合到称为类的单个单元中的概念。本节深入探讨封装的意义以及数据隐藏的实践，阐明它们如何有助于代码组织、可重用性和可维护性。

### 封装：捆绑数据和方法

封装涉及将数据（属性）和操作该数据的方法（函数）捆绑到单个单元（即类）中。这种捆绑创建了一个具有明确定义接口的自包含模块，将内部细节与外部世界隔离开来。考虑以下示例：

```cpp
#include <iostream>

// Class definition for a BankAccount with encapsulation
class BankAccount {
private:
    // Private data member (encapsulation)
    double balance;

public:
    // Public member functions for interaction
    void deposit(double amount) {
        balance += amount;
    }

    void withdraw(double amount) {
        if (amount <= balance) {
            balance -= amount;
        } else {
            std::cout << "Insufficient funds." << std::endl;
        }
    }

    double getBalance() const {
        return balance;
    }
};

int main() {
    // Creating an object of the BankAccount class
    BankAccount myAccount;

    // Performing transactions using public member functions
    myAccount.deposit(1000.0);
    myAccount.withdraw(500.0);

    // Accessing the balance through a public member function
    std::cout << "Current Balance: $" << myAccount.getBalance() << std::endl;

    return 0;
}
```

在此示例中，BankAccount 类将余额封装为私有数据成员，确保通过公共成员函数进行受控访问。这种封装为与 BankAccount 对象交互提供了清晰且受控的接口。

### 数据隐藏：控制访问

数据隐藏是封装的一个关键方面，通过使用 private、public 和 protected 等访问说明符指定类成员的可见性来实现。私有成员只能在类内部访问，从而形成一道屏障，防止外部代码直接操作。在 BankAccount 示例中，balance 数据成员是私有的，确保只能通过公共成员函数提供的受控接口修改它。

### 封装与数据隐藏的好处

封装和数据隐藏有助于代码可维护性，因为对类内部实现的更改不会影响通过其公共接口与该类交互的外部代码。这促进了代码稳定性，并降低了进行修改时产生意外副作用的风险。

此外，封装通过创建可轻松集成到程序不同部分的模块化单元来促进代码可重用性。具有明确定义接口的类成为构建块，可简化开发过程并增强代码可读性。

封装和数据隐藏是 C++ 面向对象编程中的基本原则。它们通过将数据和方法捆绑到内聚单元中，提供清晰的交互接口，同时保护内部实现细节，从而支持创建健壮且模块化的代码。这些实践有助于开发可维护、可重用且组织良好的软件系统。

## 构造函数与析构函数

构造函数和析构函数是 C++ 中对象生命周期管理的重要组成部分。本节探讨构造函数在初始化对象方面的重要性，以及析构函数在对象离开作用域或被显式删除时执行清理任务方面的重要性。理解这些概念对于有效的面向对象编程和资源管理至关重要。

### 构造函数：精确初始化对象

构造函数是类中的特殊成员函数，负责在对象创建时初始化其状态。它们确保对象以明确定义且一致的状态开始。在 C++ 中，构造函数的名称与类相同，并在实例化对象时自动调用。考虑以下示例：

```cpp
#include <iostream>

// Class definition with a constructor
class Point {
private:
    int x, y;
```

