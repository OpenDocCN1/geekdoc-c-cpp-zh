

关键要认识到的是，基类 **shipping_company** 声明了一个没有实现的纯虚函数。只有在派生类中才为该函数提供了实际的定义。

当你有纯虚函数时，必须认识到你不能实例化基类。在示例中，拥有一个运输公司是没有意义的；对于某个通用的运输公司来说，无法知道运费是多少。相反，你需要拥有一个具体的运输公司。

你不能从抽象类创建对象，尽管你可以拥有对抽象类的引用。提供实现细节的类——创建对象的低层派生类——是具体类。

因此，如果你取相同的先前定义并修改 **main** 例程以创建一个 **shipping_company** 的实例，你会得到一个错误，提示你不能声明抽象类型。◆

一个具有纯函数的类是 **abstract class**。它定义了一个接口，如 **shipping_company**，该接口不能引用类的任何特定实例，而只是定义了一些更通用、抽象的表示。

```
// Error when trying to instantiate an abstract class
int main() {
  shipping_company;
}
```

## Exercise

创建一个抽象的 **shape** 类，它具有一个 **area** 函数。然后，创建 2 个具体的类——**square** 和 **circle**——它们继承自通用的 **shape** 类。

Click here to see the solution.

## READINGS

+ a Stroustrup, *Programming Principles and Practice Using C++*, sections 14.2–14.3.
+ b Lippman, Lajoie, and Moo, *C++ Primer*, sections 15.3–15.4.

## Here's one way that could be implemented.

```
// Program 2.9
// Abstract shape class with pure virtual function
#include<iostream>
using namespace std;

class shape {
public:
    virtual float area() = 0;
};

class square : public shape {
private:
    float side_length;
public:
    square(float s) {
        side_length = s;
    }
    float area() {
        return side_length * side_length;
    }
};

class circle : public shape {
private:
    float radius;
public:
    circle(float r) {
        radius = r;
    }
    float area() {
        return radius * radius * 3.14159;
    }
};

 main() {
    square s(3.0);
    circle c(3.0);
    cout << "Areas are: " << s.area() << " and " << c.area() << endl;
    return 0;
}
```

## // QUIZ

+ 1. Are the following true or false regarding a pure virtual function?

+ a You can provide a default definition for the pure virtual function to use in case it is not in a subclass.

+ c The class with a pure virtual function is declared is an abstract class.

+ d Only one subclass can instantiate the pure virtual function.

+ b It is defined using a line where the virtual function header is provided and then = 0; is added.

+ 2 How would you create a new type of exception, called an insufficient_storage exception, stored (in a public member variable) integer amount_short?

What would be the output of the following code? (Be careful to look at how each function is defined and exactly what is called in each function call.)

```
#include<iostream>
#include<string>
using namespace std;

class airplane {
public:
    float weight;
    string name;

    void print_name() {
        cout << "For the airplane " << name << ",";
    }
    virtual void print_info() {
        cout << "weight is: " << weight << endl;
    }
};

class jet : public airplane {
public:
    int numengines;

    void print_name() {
        cout << "For the jet " << name << ",";
    }

    void print_info() {
        cout << "weight is: " << weight << " " and there are " << numengines << " engines"<< endl;
    }
};

void print_plane_data(airplane &a) {
    a.print_name();
    a.print_info();
}

void print_plane_data2(airplane &a) {
    airplane privateplane;
    jet commercialplane;
    privateplane.name = "A123";
    privateplane.weight = 3000.0;
    commercialplane.name = "B456";
    commercialplane.weight = 10000.0;
    commercialplane.numengines = 4;
    privateplane.print_name();
    privateplane.print_info();
    commercialplane.print_name();
    commercialplane.print_info();
    print_plane_data(commercialplane);
    print_plane_data2(commercialplane);
}

int main() {
```

Lecture 20 | Object-Oriented Programming with Polymorphism

## // QUIZ ANSWERS

+ 1 Remember that a pure virtual function is declared in an abstract class and must be instantiated in a subclass.

+ 2 To create such an exception, you would need to have #included <exception> and <stdexcept>. Then, the class itself inherits from exception:

So, when commercialplane print_name directly then, the jet version is used. But when commercialplane is passed to print_plane_data or print_plane_data2, it is treated as an airplane, not a jet, so the airplane version is used.

+ a False. You cannot provide a default version of the pure virtual function; if this were the case, it would not be a pure virtual function, but just a regular virtual function.

```
class insufficient_storage :
public exception {
public:
 int amount_short;
};
```

Then, insufficient_storage could be used wherever an exception was used.

The print_plane_ function takes an airplane parameter by value. Thus, the local parameter, a, is always airplane, regardless of what subclass might have been passed. There is a new airplane object created in memory, which is based on the function. Thus, the airplane version of functions (both print_name and print_name_info) are called.

+ b True. You define a pure virtual function by adding =0; to the header. For example,

```
virtual bool is_valid() = 0;
```

declares a pure function named is_valid that takes no parameters and returns a Boolean.

+ 3 Here is the output:

For the airplane A123, weight is: 3000
For the jet B456, weight is: 10000 and there are 4 engines
For the airplane B456, weight is: 10000 and there are 4 engines

The print_data2 function, however, takes an airplane parameter by reference. Thus, when you pass nothing copied; you have a reference to the full jet object (which was not virtual) function still uses the airplane version, the print_info function is virtual, so the version of which print_info is defined. In this case, that is the jet version.

+ c True. When a class has a pure virtual function, it cannot be instantiated; you cannot have an object of that class because the function is not defined. This is called an abstract class.

Notice several things about how the classes are arranged.

+ d False. The pure virtual function can be instantiated by and all subclasses. Every subclass must have some definition (inherited or in that class) for it to be instantiated.

The airplane class defines print_name as a non-virtual function. The jet class also defines print_name, with slightly different output. This means only jet objects or references will look to the jet version of the function and any time there is an airplane, including a reference to an airplane, the airplane version will be used.

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_245_0.png)

## 21 Using Classes to Build a Game Engine in C++

+ IN THIS LECTURE:
Designing Classes
Coding Your Design
Quiz
Quiz Answer

What you've been learning about object-oriented program is all going to come together now as you are walked through a development process for designing a game engine that can be used for more than one game through the use of classes.

## // DESIGNING CLASSES

You want to create a system that lets play 2-person board games on a computer. In lecture 15, you developed a Connect 4 game; in this lecture, you want to build using your top-down design use object-oriented principles. In fact, you can handle all of 2-person games—not just Connect 4, but checkers, chess, or Othello.

In Reversi, players take turns placing either black or white pieces on an 8-8 board. The game starts with 2 white and 2 black pieces already placed in the 4 squares.

If a black piece is placed, it has to be placed next to some white piece—beside, above, below, or diagonally. If the new black piece causes any white pieces to be newly bracketed by a pair of black pieces—in a row, column, or diagonally—then that causes all newly bracketed pieces to switch color to black.

For this implementation, the focus will be on 2 different games: Connect 4 and Othello, known more as Reversi.

The winner is the one with the most of his or her color piece on the board after the board is filled up.

As is with any approach to software development, the first thing you should do when faced with a programming problem is stop and think.

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_246_0.png)

