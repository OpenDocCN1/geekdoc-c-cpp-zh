
Display 6.1 shows the definition of a structure called `CDAccountV1` that can be used for this kind of account. (The V1 stands for version 1. We will define an improved version later in this chapter.)

## Display 6.1 A Structure Definition (part 1 of 2)

```cpp
//Program to demonstrate the CDAccountV1 structure type.
#include <iostream>
using namespace std;

//Structure for a bank certificate of deposit:
struct CDAccountV1
{
    double balance;
    double interestRate;
    int term; //months until maturity
};

void getData(CDAccountV1& theAccount);
//Postcondition: theAccount.balance, theAccount.interestRate, and
//theAccount.term have been given values that the user entered at the
//keyboard.

int main( )
{
    CDAccountV1 account;
    getData(account);

    double rateFraction, interest;
    rateFraction = account.interestRate/100.0;
    interest = account.balance*rateFraction*(account.term/12.0);
    account.balance = account.balance + interest;

    cout.setf(ios::fixed);
    cout.setf(ios::showpoint);
    cout.precision(2);
    cout << "When CD matures in "
         << account.term << " months,\n"
         << "it will have a balance of $"
         << account.balance << endl;

    return 0;
}
//Uses iostream:
void getData(CDAccountV1& theAccount)
{
    cout << "Enter account balance: $";
    cin >> theAccount.balance;
```

An improved version of this structure will be given later in this chapter.

## Display 6.1 A Structure Definition (part 2 of 2)

```cpp
36    cout << "Enter account interest rate: ";
37    cin  >> theAccount.interestRate;
38    cout << "Enter the number of months until maturity: ";
39    cin  >> theAccount.term;
40 }
```

## Sample Dialogue

```
Enter account balance: $100.00
Enter account interest rate: 10.0
Enter the number of months until maturity: 6
When your CD matures in 6 months,
it will have a balance of $105.00
```

## Structure Types

The structure definition in Display 6.1 is as follows:

```cpp
struct CDAccountV1
{
    double balance;
    double interestRate;
    int term;//months until maturity
};
```

The keyword `struct` announces that this is a structure-type definition. The identifier `CDAccountV1` is the name of the structure type, which is known as the structure tag. The structure tag can be any legal identifier that is not a keyword. Although this is not required by the C++ language, structure tags are usually spelled starting with an uppercase letter. The identifiers declared inside the braces, `{}`, are called member names. As illustrated in this example, a structure type definition ends with both a brace, `}`, and a semicolon.

A structure definition is usually placed outside any function definition (in the same way that globally defined constant declarations are placed outside all function definitions). The structure type is then a global definition that is available to all the code that follows the structure definition.

Once a structure type definition has been given, the structure type can be used just like the predefined types `int`, `char`, and so forth. Note that in Display 6.1 the structure type `CDAccountV1` is used to declare a variable in the function `main` and is used as the name of the parameter type for the function `getData`.

A structure variable can hold values just like any other variable can. A structure value is a collection of smaller values called member values. There is one member value for each member name declared in the structure definition. For example, a value of the type `CDAccountV1` is a collection of three member values, two of type `double` and one of type `int`. The member values that together make up the structure value are stored in member variables, which we discuss next.

## 2024年1月1日 星期一

今天是2024年的第一天，也是元旦。在这个辞旧迎新的时刻，我们向所有读者致以最诚挚的问候和祝福。

新的一年，新的起点。让我们回顾过去一年的成就与不足，展望未来的机遇与挑战。

- 元旦快乐
- 新年新气象
- 万事如意

| 项目 | 内容 |
|------|------|
| 日期 | 2024年1月1日 |
| 节日 | 元旦 |
| 天气 | 晴 |

> 千里之行，始于足下。

在新的一年里，我们期待与读者一起成长，共同进步。

```python
print("Hello, 2024!")
```

感谢大家一直以来的支持，祝大家新年快乐！

## EXAMPLES

```cpp
struct StudentRecord
{
    int studentNumber;
    char grade;
};

int main( )
{
    StudentRecord yourRecord;
    yourRecord.studentNumber = 2001;
    yourRecord.grade = 'A';
}
```

Some writers call the dot operator the structure member access operator, although we will not use that term.

This coincidence of names will produce no problems. For example, if you declare the following two structure variables,

```cpp
FertilizerStock superGrow;
CropYield apples;
```

then the quantity of superGrow fertilizer is stored in the member variable `superGrow.quantity`, and the quantity of apples produced is stored in the member variable `apples.quantity`. The dot operator and the structure variable specify which quantity is meant in each instance.

### Structure Variables in Assignment Statements

A structure value can be viewed as a collection of member values. A structure value can also be viewed as a single (complex) value (that just happens to be made up of member values). Since a structure value can be viewed as a single value, structure values and structure variables can be used in the same ways that you use simple values and simple variables of the predefined types such as `int`. In particular, you can assign structure values using the equal sign. For example, if `apples` and `oranges` are structure variables of the type `CropYield` defined earlier, then the following is perfectly legal:

```cpp
apples = oranges;
```

The previous assignment statement is equivalent to

```cpp
apples.quantity = oranges.quantity;
apples.size = oranges.size;
```

## Simple Structure Types

You define a structure type as shown here. The `Structure_Tag` is the name of the structure type.

### Syntax

```cpp
struct Structure_Tag
{
    Type_1 Member_Variable_Name_1;
    Type_2 Member_Variable_Name_2;
                         .
                         .
                         .
    Type_Last Member_Variable_Name_Last;
};
```

*Do not forget this semicolon.*

### Example

```cpp
struct Automobile
{
    int year;
    int doors;
    double horsePower;
    char model;
};
```

Although we will not use this feature, you can combine member names of the same type into a single list separated by commas. For example, the following is equivalent to the previous structure definition:

```cpp
struct Automobile
{
    int year, doors;
    double horsePower;
    char model;
};
```

Variables of a structure type can be declared in the same way as variables of other types. For example,

```cpp
Automobile myCar, yourCar;
```

The member variables are specified using the dot operator. For example, `myCar.year`, `myCar.doors`, `myCar.horsePower`, and `myCar.model`.

## Pitfall: Forgetting a Semicolon in a Structure Definition

When you add the final brace, `}`, to a structure definition, it feels like the structure definition is finished, but it is not. You must also place a semicolon after that final brace. There is a reason for this, even though the reason is a feature that we will have no occasion to use. A structure definition is more than a definition. It can also be used to declare structure variables. You are allowed to list structure variable names between that final brace and that final semicolon. For example, the following defines a structure called `WeatherData` and declares two structure variables, `dataPoint1` and `dataPoint2`, both of type `WeatherData`:

```cpp
struct WeatherData
{
    double temperature;
    double windVelocity;
} dataPoint1, dataPoint2;
```

## Structures as Function Arguments

A function can have call-by-value parameters of a structure type or call-by-reference parameters of a structure type, or both. The program in Display 6.1, for example, includes a function named `getData` that has a call-by-reference parameter with the structure type `CDAccountV1`.

A structure type can also be the type returned by a function. For example, the following defines a function that takes one argument of type `CDAccountV1` and returns a different structure of type `CDAccountV1`. The structure returned will have the same balance and term as the argument but will pay double the interest rate that the argument pays.

```cpp
CDAccountV1 doubleInterest(CDAccountV1 oldAccount)
{
    CDAccountV1 temp;
    temp = oldAccount;
    temp.interestRate = 2*oldAccount.interestRate;
    return temp;
}
```

Notice the local variable `temp` of type `CDAccountV1`; `temp` is used to build up a complete structure value of the desired kind, which is then returned by the function. If `myAccount` is a variable of type `CDAccountV1` that has been given values for its member variables, then the following will give `yourAccount` values for an account with double the interest rate of `myAccount`:

```cpp
CDAccountV1 yourAccount;
yourAccount = doubleInterest(myAccount);
```
