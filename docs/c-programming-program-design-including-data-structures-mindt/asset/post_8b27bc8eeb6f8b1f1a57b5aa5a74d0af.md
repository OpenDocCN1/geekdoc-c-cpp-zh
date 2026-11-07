
```cpp
using namespace std;                                      //Line 7

int main()                                                  //Line 8
{                                                          //Line 9
        double num;                                        //Line 10

        num = 2 * PRIZE;                                   //Line 11
        mySpace::x = static_cast<num>;                     //Line 12
        cout << PRIZE << " " << mySpace::x << " "         //Line 13
             << num << endl;

        return 0;                                          //Line 14
}                                                          //Line 15
```

13. What is wrong with the following program? (10)

```cpp
#include <iostream>                                      //Line 1

namespace aaa                                             //Line 2
{                                                          //Line 3
        const int x = 0;                                  //Line 3
        double y;                                          //Line 4
}                                                          

using namespace std;                                       //Line 5

int main()                                                  //Line 6
{                                                          
        y = 34.50;                                         //Line 7
        cout << "x = " << x << ", y = " << y             //Line 8
             << endl;                                      
        return 0;                                          //Line 9
}                                                          
```

14. What is wrong with the following program? (10)

```cpp
#include <iostream>                                      //Line 1
#include <math>                                           //Line 2

using nameSpace std;                                      //Line 3

void main()                                               //Line 4
{                                                          //Line 5
        cout << floor(sqrt(14.56)) << std::endl;           //Line 6
        return 0;                                          //Line 7
}                                                          //Line 8
```

15. Consider the following C++ code. (11)

```cpp
string str1, str2;
char ch;
int pos;

cin >> str1 >> str2 >> pos;
ch = str1[pos];
str1[pos] = str2[pos];
str2[pos] = ch;

cout << str1 << " " << str2 << endl;
```

Answer the following questions.

- a. What is the output if the input is **Summer Vacation 1**?
- b. What is the output if the input is **Temporary Project 4**?
- c. What is the output if the input is **Social Network 0**?

16. Suppose that you have the following statements:

```cpp
string str, str1, str2;

cin >> str1 >> str2;

if (str1 == str2)
    str = str1 + " = " + str2;
else if (str1 > str2)
    str = str1 + " > " + str2;
else
    str = str1 + " < " + str2;
```

Answer the following questions. (11)

- a. What is the value of **str** if the input is **Temporary Storage**?
- b. What is the value of **str** if the input is **Main Memory**?
- c. What is the value of **str** if the input is **run! run!**?

17. What is the output of the following program? (11)

```cpp
#include <iostream>
#include <string>

using namespace std;

int main()
{
    string str = "Regular exercise can reduce health insurance cost.";
    string str1;
    string str2 = "low fat diet";
    string newStr;

    string::size_type index;

    index = str.find("can");
    str1 = str.substr(0, index - 1);
    cout << str1 << endl;

    newStr = str1 + " and " + str2;
    cout << newStr << endl;
    cout << newStr.length() << endl;

    cout << str1.find("ex") << endl;
    cout << str2.find('d') << endl;

    index = str.find("health");
    newStr = str.substr(index, 17);

    cout << newStr << endl;
    cout << newStr.substr(7, 14) << endl;

    index = str.find("cost");
    cout << str.replace(index, 4, "$$$$") << endl;

    str = "Social Media!!";
    cout << str << endl;
    cout << str.length() << endl;

    str[0] = 'S';
    index = str.find('N');
    str[index] = 'M';

    cout << str << endl;

    return 0;
}
```

**18.** Consider the following statement.

```cpp
string str = "This summer we will drive across the country!";
```

What is the output of the following statements? (Assume that all parts are independent of each other.) (11)

- a.

  ```cpp
  cout << str.size() << endl;
  ```

- b.

  ```cpp
  cout << str.substr(12, 20) << endl;
  ```

- c.

  ```cpp
  string::size_type ind = str.find('s');
  str.replace(ind + 2, 6, "spring");
  cout << str << endl;
  ```

- d.

  ```cpp
  str.erase(20, 25);
  str.insert(20, "enjoy Caribbean cruise!");
  cout << str << endl;
  ```

## PROGRAMMING EXERCISES

- 1.
  - **a.** Define an enumeration type `triangleType` that has the values `scalene`, `isosceles`, `equilateral`, and `noTriangle`.
  - **b.** Write a function `triangleShape` that takes as parameters three numbers, each of which represents the length of a side of the triangle. The function
  - **c.** Write a program that prompts the user to input the lengths of the sides of a triangle and outputs the shape of the triangle.

- 2. Redo Programming Exercise 16 of Chapter 4 so that all of the named constants are defined in a `namespace`.

- 3. The Programming Example: Pig Latin Strings converts a string into the pig Latin form, but it processes only one word. Rewrite the program so that it can be used to process a text of an unspecified length. If a word ends with a punctuation mark, in the pig Latin form, put the punctuation at the end of the string. For example, the pig Latin form of `Hello!` is `ello-Hay!`. Assume that the text contains the following punctuation marks: `,` (comma), `.` (period), `?` (question mark), `;` (semicolon), and `:` (colon). (Your program may store the output in a file.)

- 4. Write a program that prompts the user to input a string. The program then uses the function `substr` to remove all the vowels from the string. For example, if `str = "There"`, then after removing all the vowels, `str = "Thr"`. After removing all the vowels, output the string. Your program must contain a function to remove all the vowels and a function to determine whether a character is a vowel.

- 5. Write a program that can be used to calculate the federal tax. The tax is calculated as follows: For single people, the standard exemption is $4,000; for married people, the standard exemption is $7,000. A person can also put up to 6% of his or her gross income in a pension plan. The tax rates are as follows: If the taxable income is:
  - Between $0 and $15,000, the tax rate is 15%.
  - Between $15,001 and $40,000, the tax is $2,250 plus 25% of the taxable income over $15,000.
  - Over $40,000, the tax is $8,460 plus 35% of the taxable income over $40,000.

  Prompt the user to enter the following information:

  - Marital status
  - If the marital status is “married,” ask for the number of children under the age of 14
  - Gross salary (If the marital status is “married” and both spouses have income, enter the combined salary.)
  - Percentage of gross income contributed to a pension fund

  Your program must consist of at least the following functions:

  - a. Function `getData`: This function asks the user to enter the relevant data.
  - b. Function `taxAmount`: This function computes and returns the tax owed.

  To calculate the taxable income, subtract the sum of the standard exemption, the amount contributed to a pension plan, and the personal exemption, which is $1,500 per person. (Note that if a married couple has two children under the age of 14, then the personal exemption is $1,500 × 4 = $6,000.)

- 6. Write a program that uses a random number generator to generate a two-digit positive integer and allows the user to perform one or more of the following operations:
  - a. Double the number.
  - b. Reverse the digits of the number.
  - c. Raise the number to the power of 2, 3, or 4.
  - d. Sum the digits of the number.
  - e. If the number is a two-digit number, then raise the first digit to the power of the second digit.
  - f. If the number is a three-digit number and the last digit is less than or equal to 4, then raise the first two digits to the power of the last digit.

  After performing an operation if the number is less than 10, add 10 to the number. Also, after each operation determine if the number is prime.

  Each successive operation should be performed on the number generated by the last operation. Your program should not contain any global variables and each of these operations must be implemented by a separate function. Also, your program should be menu driven.

- 7. **(Fraction calculator)** Write a program that lets the user perform arithmetic operations on fractions. Fractions are of the form *a/b*, in which *a* and *b* are integers and *b ≠ 0*. Your program must be menu driven, allowing the user to select the operation (+, -, *, or /) and input the numerator and denominator of each fraction. Furthermore, your program must consist of at least the following functions:
  - a. **Function menu:** This function informs the user about the program’s purpose, explains how to enter data, and allows the user to select the operation.
  - b. **Function addFractions:** This function takes as input four integers representing the numerators and denominators of two fractions, adds the fractions, and returns the numerator and denominator of the result. (Notice that this function has a total of six parameters.)
  - c. **Function subtractFractions:** This function takes as input four integers representing the numerators and denominators of two fractions, subtracts the fractions, and returns the numerator and denominator of the result. (Notice that this function has a total of six parameters.)
  - d. **Function multiplyFractions:** This function takes as input four integers representing the numerators and denominators of two fractions, multiplies the fractions, and returns the numerators and denominators of the result. (Notice that this function has a total of six parameters.)

![](img/b217c421655b51e7494cf3b89bb5432d_568_0.png)
