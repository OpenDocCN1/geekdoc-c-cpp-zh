
## PITFALL: (continued)

On the other hand, if you overload + as a nonmember (as in Display 8.1), then the following is perfectly legal:

```
fullAmount = 25 + baseAmount;
```

This is the biggest advantage of overloading an operator as a nonmember.

Overloading an operator as a nonmember gives you automatic type conversion of all arguments. Overloading an operator as a member gives you the efficiency of bypassing accessor and mutator functions and directly accessing member variables. There is a way to overload an operator (and certain functions) that offers both of these advantages. It is called overloading as a friend function and is our next topic.

## Friend Functions

If your class has a full set of accessor and mutator functions, you can use the accessor and mutator functions to define nonmember overloaded operators (as in Display 8.1 as opposed to Display 8.2). However, although this may give you access to the private member variables, it may not give you efficient access to them. Look again at the definition of the overloaded addition operator + given in Display 8.1. Rather than just reading four member variables, it must incur the overhead of two invocations of getCents and two invocations of getDollars. This adds a bit of inefficiency and also can make the code harder to understand. The alternative of overloading + as a member gets around this problem at the price of losing automatic type conversion of the first operand. Overloading the + operator as a friend will allow us to both directly access member variables and have automatic type conversion for all operands.

A friend function of a class is not a member function of the class, but it has access to the private members of that class (to both private member variables and private member functions) just as a member function does. To make a function a friend function, you must name it as a friend in the class definition. For example, in Display 8.3 we have rewritten the definition of the class Money yet another time. This time we have overloaded the operators as friends. You make an operator or function a friend of a class by listing the operator or function declaration in the definition of the class and placing the keyword friend in front of the operator or function declaration.

A friend operator or friend function has its declaration listed in the class definition, just as you would list the declaration of a member function, except that you precede the declaration by the keyword friend. However, a friend is not a member function; rather, it really is an ordinary function with extraordinary access to the data members of the class. The friend is defined exactly like the ordinary function it is. In particular, the operator definitions shown in Display 8.3 do not include the qualifier Money:: in the function heading. Also, you do not use the keyword friend in the function definition (only in the function declaration). The friend operators in Display 8.3 are invoked just like the nonfriend, nonmember operators in Display 8.1, and they have automatic type conversion of all arguments just like the nonfriend, nonmember operators in Display 8.1.

friend function

## 1. 引言

本文档旨在介绍一种新型的文档解析方法，该方法结合了深度学习和传统图像处理技术，能够高效地从复杂版面中提取结构化信息。

## 2. 方法概述

本方法主要分为三个步骤：版面分析、文本识别和结构重建。首先，通过卷积神经网络对文档图像进行区域分割；其次，利用光学字符识别技术提取文本内容；最后，根据版面信息重建文档的逻辑结构。

- 步骤一：版面分析
- 步骤二：文本识别
- 步骤三：结构重建

### 2.1 版面分析

版面分析阶段，我们采用基于注意力机制的U-Net架构，对图像中的文本块、表格、图片等元素进行像素级分割。

![](img/c76bba8c1d927f399768ffe2ab5f5bee_373_0.png)

## Display 8.3 Overloading Operators as Friends (part 2 of 2)

```
25    int dollarsPart(double amount) const;
26    int centsPart(double amount) const;
27    int round(double number) const;
28 };

29 int main()
30 {
31    <If the main function is the same as in Display 8.1, then the screen dialogue will be the same as shown in Display 8.1.>
32 }
33 
34 const Money operator +(const Money& amount1, const Money& amount2)
35 {
36    int allCents1 = amount1.cents + amount1.dollars*100;
37    int allCents2 = amount2.cents + amount2.dollars*100;
38    int sumAllCents = allCents1 + allCents2;
39    int absAllCents = abs(sumAllCents); //Money can be negative.
40    int finalDollars = absAllCents/100;
41    int finalCents = absAllCents%100;
42 
43    if (sumAllCents < 0)
44    {
45       finalDollars = -finalDollars;
46       finalCents = -finalCents;
47    }
48 
49    return Money(finalDollars, finalCents);
50 }

49 const Money operator -(const Money& amount1, const Money& amount2)
50    <The complete definition is Self-Test Exercise 7.>

51 bool operator ==(const Money& amount1, const Money& amount2)
52 {
53    return ((amount1.dollars == amount2.dollars)
54       && (amount1.cents == amount2.cents));
55 }

56 const Money operator -(const Money& amount)
57 {
58    return Money(-amount.dollars, -amount.cents);
59 }

60 <Definitions of all other member functions are the same as in Display 8.1.>

Note that friends have direct access to member variables.
```

## Friend Classes

**friend class**

A class can be a **friend** of another class in the same way that a function can be a friend of a class. If the class F is a friend of the class C, then every member function of the class F is a friend of the class C. To make one class a friend of another, you must declare the friend class as a friend within the other class.

**forward declaration**

When one class is a friend of another class, it is typical for the classes to reference each other in their class definitions. This requires that you include a **forward declaration** to the class defined second, as illustrated in the outline that follows this paragraph. Note that the forward declaration is just the heading of the class definition followed by a semicolon.

```
## Friend Functions

A friend function of a class is an ordinary function except that it has access to the private members of objects of that class. To make a function a friend of a class, you must list the function declaration for the friend function in the class definition. The function declaration is preceded by the keyword friend. The function declaration may be placed in either the private section or the public section, but it will be a public function in either case, so it is clearer to list it in the public section.

### SYNTAX OF A CLASS DEFINITION WITH FRIEND FUNCTIONS

```cpp
class Class_Name
{
public:
    friend Declaration_for_Friend_Function_1
    friend Declaration_for_Friend_Function_2
    .
    .
    Member_Function_Declarations
private:
    Private_Member_Declarations
};
```

### EXAMPLE

```cpp
class FuelTank
{
public:
    friend void fillLowest(FuelTank& t1, FuelTank& t2);
    //Fills the tank with the lowest fuel level, or et al if a tie.

    FuelTank(double theCapacity, double theLevel);
    FuelTank();
};
```
```

![](img/c76bba8c1d927f399768ffe2ab5f5bee_375_0.png)

```
```cpp
void input();
void output() const;
private:
    double capacity; // in liters
    double level;
};
```
```

A friend function is **not** a member function. A friend function is defined and called the same way as an ordinary function. You do not use the dot operator in a call to a friend function, and you do not use a type qualifier in the definition of a friend function.

If you want the class F to be a friend of the class C, the general outline of how you set things up is as follows:

```
```cpp
class F; // forward declaration

class C
{
public:
    ...
    friend class F;
};

class F
{
```
```

Complete examples using friend classes are given in Chapter 17. We will not be using friend classes until then.

## PITFALL: Compilers without Friends

On some C++ compilers friend functions simply do not work as they are supposed to work. Worst of all, they may work sometimes and not work at other times. On these compilers friend functions do not always have access to private members of the class as they are supposed to. Presumably, this will be fixed in later releases of these compilers. In the meantime, you will have to work around this problem. If you have one of these compilers for which friend functions do not work, you must either use accessor functions to define nonmember functions and overloaded operators or you must overload operators as members.
