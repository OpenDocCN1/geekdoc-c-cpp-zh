
你应该避免重载`&&`、`||`和逗号运算符。重载时，这些运算符将执行完全的从左到右求值。这与这些运算符的行为相反。重载时，没有这种保证。列表 14.7 给出了`Rational`类的一个新头文件`RationalOperators.h`。文件中的 10-22 行与列表 14.1 相同。比较运算符（`<`、`==`、`=`）和算术运算符（`+`、`*`、`/`）的函数定义在 48-57 行。

### 列表 14.7 RationalOperators.h

```cpp
#ifndef RATIONALOPERATORS_H
#define RATIONALOPERATORS_H
#include <string>
#include <iostream>
using namespace std;

class Rational
{
public:
    Rational();
    Rational(int numerator, int denominator);
    int getNumerator() const;
    int getDenominator() const;
    Rational add(const Rational&secondRational) const;
    Rational subtract(const Rational&secondRational) const;
    Rational multiply(const Rational&secondRational) const;
    Rational divide(const Rational&secondRational) const;
    int compareTo(const Rational&secondRational) const;
    bool equals(const Rational&secondRational) const;
    int intValue() const;
    double doubleValue() const;
    string toString() const;

    // 转换函数
    Rational(int numerator);

    // 运算符
    friend Rational operator+(const Rational& r1, const Rational& r2);
    friend Rational operator-(const Rational& r1, const Rational& r2);
    friend Rational operator*(const Rational& r1, const Rational& r2);
    friend Rational operator/(const Rational& r1, const Rational& r2);

    // 
    Rational& operator+=(const Rational& secondRational);
    Rational& operator-=(const Rational& secondRational);
    Rational& operator*=(const Rational& secondRational);
    Rational& operator/=(const Rational& secondRational);

    // 前缀 ++ --
    Rational& operator++();
    Rational& operator--();

    // 后置 ++ --
    Rational operator++(int);
    Rational operator--(int);

    // 下标和输入输出
    friend ostream& operator<<(ostream& os, const Rational&);
    friend istream& operator>>(istream& is, Rational& r);

private:
    int numerator;
    int denominator;
    static int gcd(int n, int d);
};

// 比较运算符
bool operator==(const Rational& r1, const Rational& r2);
bool operator!=(const Rational& r1, const Rational& r2);
bool operator<(const Rational& r1, const Rational& r2);
bool operator<=(const Rational& r1, const Rational& r2);
bool operator>(const Rational& r1, const Rational& r2);
bool operator>=(const Rational& r1, const Rational& r2);

// 算术运算符
Rational operator+(const Rational& r1, const Rational& r2);
Rational operator-(const Rational& r1, const Rational& r2);
Rational operator*(const Rational& r1, const Rational& r2);
Rational operator/(const Rational& r1, const Rational& r2);

#endif
```

### 列表 14.8 RationalOperators.cpp

```cpp
14.8 RationalOperators.cpp
#include "RationalOperators.h"
#include <iostream>

Rational::Rational()
{
    numerator = 0;
    denominator = 1;
}

Rational::Rational(int numerator, int denominator)
{
    int factor = gcd(numerator, denominator);
    this->numerator = numerator / factor;
    this->denominator = denominator / factor;
}

int Rational::getNumerator() const
{
    return numerator;
}

int Rational::getDenominator() const
{
    return denominator;
}

int Rational::gcd(int n, int d)
{
    int n1 = abs(n);
    int n2 = abs(d);
    int gcd = 1;

    for (int k = 1; k <= n1 && k <= n2; k++)
    {
        if (n1 % k == 0 && n2 % k == 0)
            gcd = k;
    }
    return gcd;
}

Rational Rational::add(const Rational&secondRational) const
{
    int n = numerator * secondRational.getDenominator() + denominator * secondRational.numerator();
    int d = denominator * secondRational.getDenominator();
    return Rational(n, d);
}

Rational Rational::subtract(const Rational&secondRational) const
{
    int n = numerator * secondRational.getDenominator() - denominator * secondRational.numerator();
    int d = denominator * secondRational.getDenominator();
    return Rational(n, d);
}

Rational Rational::multiply(const Rational&secondRational) const
{
    int n = numerator * secondRational.getNumerator();
    int d = denominator * secondRational.getDenominator();
    return Rational(n, d);
}

Rational Rational::divide(const Rational&secondRational) const
{
    int n = numerator * secondRational.getDenominator();
    int d = denominator * secondRational.numerator();
    return Rational(n, d);
}

int Rational::compareTo(const Rational&secondRational) const
{
    Rational temp = subtract(secondRational);
    if (temp.numerator() < 0)
        return -1;
    else if (temp.numerator() > 0)
        return 1;
    else
        return 0;
}

bool Rational::equals(const Rational&secondRational) const
{
    return compareTo(secondRational) == 0;
}

int Rational::intValue() const
{
    return numerator / denominator;
}

double Rational::doubleValue() const
{
    return (double)numerator / denominator;
}

string Rational::toString() const
{
    return to_string(numerator) + "/" + to_string(denominator);
}

Rational operator+(const Rational& r1, const Rational& r2)
{
    return r1.add(r2);
}

Rational operator-(const Rational& r1, const Rational& r2)
{
    return r1.subtract(r2);
}

Rational operator*(const Rational& r1, const Rational& r2)
{
    return r1.multiply(r2);
}

Rational operator/(const Rational& r1, const Rational& r2)
{
    return r1.divide(r2);
}

Rational& Rational::operator+=(const Rational& secondRational)
{
    Rational temp = add(secondRational);
    numerator = temp.numerator();
    denominator = temp.denominator();
    return *this;
}

Rational& Rational::operator-=(const Rational& secondRational)
{
    Rational temp = subtract(secondRational);
    numerator = temp.numerator();
    denominator = temp.denominator();
    return *this;
}

Rational& Rational::operator*=(const Rational& secondRational)
{
    Rational temp = multiply(secondRational);
    numerator = temp.numerator();
    denominator = temp.denominator();
    return *this;
}

Rational& Rational::operator/=(const Rational& secondRational)
{
    Rational temp = divide(secondRational);
    numerator = temp.numerator();
    denominator = temp.denominator();
    return *this;
}

Rational& Rational::operator++()
{
    numerator++;
    return *this;
}

Rational& Rational::operator--()
{
    numerator--;
    return *this;
}

Rational Rational::operator++(int)
{
    Rational temp = *this;
    numerator++;
    return temp;
}

Rational Rational::operator--(int)
{
    Rational temp = *this;
    numerator--;
    return temp;
}

int& Rational::operator[](int index)
{
    // Placeholder for logic
    return numerator; 
}

ostream& operator<<(ostream& os, const Rational& r)
{
    os << r.toString();
    return os;
}

istream& operator>>(istream& is, Rational& r)
{
    // Placeholder for logic
    return is;
}

bool operator==(const Rational& r1, const Rational& r2)
{
    return r1.equals(r2);
}

bool operator!=(const Rational& r1, const Rational& r2)
{
    return !r1.equals(r2);
}

bool operator<(const Rational& r1, const Rational& r2)
{
    return r1.compareTo(r2) < 0;
}

bool operator<=(const Rational& r1, const Rational& r2)
{
    return r1.compareTo(r2) <= 0;
}

bool operator>(const Rational& r1, const Rational& r2)
{
    return r1.compareTo(r2) > 0;
}

bool operator>=(const Rational& r1, const Rational& r2)
{
    return r1.compareTo(r2) >= 0;
}
```

## 14.11 使用重载运算符的有数类

```cpp
return -1;
else if (temp.getNumerator() == 0)
return 0;
else
return 1;
```

```cpp
bool Rational::equals(const Rational &secondRational) const {
    if (compareTo(secondRational) == 0)
        return true;
    else
        return false;
}
```

```cpp
int Rational::intValue() {
    return getNumerator() / getDenominator();
}
```

```cpp
double Rational::doubleValue() const {
    return 1.0 * getNumerator() / getDenominator();
}
```

```cpp
string Rational::toString() {
    string ss1, ss2;
    ss1 << numerator;
    ss2 << denominator;
    if (denominator == 1)
        return ss1.str() + "";
    else
        return ss1.str() + "/" + ss2.str();
}
```

```cpp
Rational Rational::Rational(int numerator) {
    this->numerator = numerator;
    this->denominator = 1;
}
```

// 定义简写运算符的形式运算符
