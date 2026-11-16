

## 子字符串函数

能够访问 String 对象的子字符串通常很有用。我们需要提取并返回 String 对象从缓冲区特定索引开始、指定长度的子字符串。

```
String substr(int, int);
```

## 输出函数

为了显示任何 String 对象的状态，我们必须编写一个打印函数。该函数将双引号内的字面量本身输出，并在同一行输出字符串字面量的长度。

```
void print();
```

重载 operator<<() 函数以仅输出字符串指针本身的内容也很有用。

```
friend ostream& operator<<(ostream&, const String&);
```

## 类继承

继承是通过扩展或增强现有类来创建派生类的过程。换句话说，派生类是从父类（或基类）继承而来的。这种能力使你无需“重新发明轮子”，因为如果新类与现有类非常相似，那么现有类的所有属性都可以继承到新类中，然后可以添加任何新成员。

继承允许你将相关类组织成层次结构，顶层的类作为下层类的抽象。这意味着派生类是其父类的特化。换句话说，派生类是基类的一种，但添加了更多细节。因此，派生类与其基类之间的关系称为 is-a 关系。

我们已经看到如何创建 String 类，并利用运算符函数重载功能使类接口更直观。现在假设你要将此类放入库中并宣布其存在，以便用户可以使用它。但有人随后对你说：“这个类很好，只是我本想将一元运算符 – 重载为成员函数，以便它反转 `String` 中字母的顺序并返回类的新实例。我该怎么办？”。在这种情况下，你的答案是让用户从 `String` 类派生一个新类并添加新函数。然后，当从新创建的类进行实例化时，原始类的所有功能仍然存在，再加上新函数的附加功能。由于这个新创建的类是带有更多功能的 `String` 类，新类确实是一种 `String` 类。

编写一个名为 `ReverseString` 的类，它从 `String` 类公有派生，包含以下成员函数：

- 一个默认构造函数
- 一个拷贝构造函数
- 一个接受 `const char*` 作为其唯一参数的构造函数
- 一个重载的赋值运算符
- 一个重载的一元 `operator~()` 函数，它反转字符串本身的字母，并按值返回一个新的 `ReverseString` 实例（注意，`buf` 指向的字符串字面量的实际内容从未被修改）

编写一个名为 `CaseString` 的类，它从 `String` 类公有派生，包含以下数据成员：

- 一个指针 `upper`，类型为 `char*`，保存字符串字面量的大写内容
- 一个指针 `lower`，类型为 `char*`，保存字符串字面量的小写内容

还在 `CaseString` 类中包含以下成员函数：

- 一个默认构造函数
- 一个拷贝构造函数
- 一个接受 `const char*` 作为其唯一参数的构造函数
- 一个重载的赋值运算符
- 一个 `print()` 函数，它将 `upper` 和 `lower` 指向的字符串字面量添加到输出中
- 一个析构函数

使用提供的 `StringDriver` 代码来测试你的类。

```cpp
// StringDriver.h
#ifndef _StringDriver_H
#define _StringDriver_H
#include "String.h"
#include "ReverseString.h"
#include "CaseString.h"
int main();
void test1();
void test2();
void test3();
void test4();
void test5();
void test6();
void test7();
void test8();
void test9();
void test10();
void test11();
void test12();
void test13();
void test14();
void test15();
void test16();
void test17();
void test18();
void test19();
void test20();
void wait();
#endif
```

```cpp
// StringDriver.cpp
#include <iostream>
#include <fstream>
#include <stdlib.h>
#include "StringDriver.h"
using namespace std;
ofstream csis;

int main() {
    csis.open("cis.txt");
    test1();
    test2();
    test3();
    test4();
    test5();
    test6();
    test7();
    test8();
    test9();
    test10();
    test11();
    test12();
    test13();
    test14();
    test15();
    test16();
    test17();
    test18();
    test19();
    test20();
    csis.close();
}

void test1() {
    cout << "1. Testing S1: String default constructor."
         << endl << endl;
    csis << "1. Testing S1: String default constructor."
         << endl << endl;
    String s1;
    s1.print();
    wait();
}

void test2() {
    cout << "2. Testing S2: String one arg (char *) constructor."
         << endl << endl;
    csis << "2. Testing S2: String one arg (char *) constructor."
         << endl << endl;
    String s2("ABC");
    s2.print();
    wait();
}

void test3() {
    cout << "3. Testing S3: String one arg (char) constructor,"
         << endl << endl;
    csis << "3. Testing S3: String one arg (char) constructor."
         << endl << endl;
    String s3("Z");
    s3.print();
    wait();
}

void test4() {
    cout << "4. Testing S4: String one arg (int) constructor,"
         << endl << endl;
    csis << "4. Testing S4: String one arg (int) constructor."
         << endl << endl;
    String s4(10);
    s4.print();
    wait();
}

void test5() {
    cout << "5. Testing S5, T5: String copy constructor."
         << endl << endl;
    csis << "5. Testing S5, T5: String copy constructor."
         << endl << endl;
    String s5("Purple Rain");
    s5.print();
    String t5(s5);
    t5.print();
    wait();
}

void test6() {
    cout << "6. Testing S6: String two arg (char, int) constructor,"
         << endl << endl;
    csis << "6. Testing S6: String two arg (char, int) constructor."
         << endl << endl;
    String s6("**", 10);
    s6.print();
    wait();
}

void test7() {
    cout << "7. Testing S7, T7, U7: String assignment."
         << endl;
    csis << "7. Testing S7, T7, U7: String assignment."
         << endl;
    String s7("Sally Ride"), t7, u7;
    t7 = u7 = s7;
    s7.print();
    t7.print();
    u7.print();
    wait();
}

void test8() {
    cout << "8. Testing S8: String assignment."
         << endl;
    csis << "8. Testing S8: String assignment."
         << endl;
    String s8("ABC");
    s8.print();
    wait();
}

void test9() {
    cout << "9. Testing S9: Implicit type conversion."
         << endl;
    csis << "9. Testing S9: Implicit type conversion."
         << endl;
    String s9;
    s9 = "ABC";
    s9.print();
    wait();
}

void test10() {
    cout << "10. Testing S10, T10, U10: String concatenation."
         << endl;
    csis << "10. Testing S10, T10, U10: String concatenation."
         << endl;
    String s10("DEE");
    String t10("HI");
    String u10("ABC" + s10 + "G" + t10 + 'I');
    u10.print();
    String v10('X' + u10);
    v10.print();
    wait();
}

void test11() {
    cout << "11. Testing S11, T11: String concatenation."
         << endl << endl;
    csis << "11. Testing S11, T11: String concatenation."
         << endl << endl;
    String s11("A");
    String t11("BC");
    s11 += s11 += t11 += 'D';
    s11.println();
    t11.print();
    wait();
}

void test12() {
    cout << "12. Testing S12, T12: String unary operator."
         << endl << endl;
    csis << "12. Testing S12, T12: String unary operator."
         << endl << endl;
    String s12("Unary +");
    String t12(+s12);
    s12.print();
    t12.print();
    t12 = +s12;
    s12.print();
    wait();
}

void test13() {
    cout << "13. Testing S13, T13: String comparison operators."
         << endl << endl;
    csis << "13. Testing S13, T13: String comparison operators."
         << endl << endl;
    String s13("ABC"), t13("ABCD");
    s13.print();
    t13.print();
    cout << endl;
    cout << "==" << (s13 == t13 ? "True" : "False") << endl;
    cout << "!=" << (s13 != t13 ? "True" : "False") << endl;
    cout << "<=" << (s13 <= t13 ? "True" : "False") << endl;
    cout << "<" << (s13 < t13 ? "True" : "False") << endl;
    cout << ">=" << (s13 >= t13 ? "True" : "False") << endl;
    cout << ">" << (s13 > t13 ? "True" : "False") << endl;
    cout << endl;
    csis << "==" << (s13 == t13 ? "True" : "False") << endl;
    csis << "!=" << (s13 != t13 ? "True" : "False") << endl;
    csis << "<=" << (s13 <= t13 ? "True" : "False") << endl;
    csis << "<" << (s13 < t13 ? "True" : "False") << endl;
    csis << ">=" << (s13 >= t13 ? "True" : "False") << endl;
    csis << ">" << (s13 > t13 ? "True" : "False") << endl;
    wait();
}

