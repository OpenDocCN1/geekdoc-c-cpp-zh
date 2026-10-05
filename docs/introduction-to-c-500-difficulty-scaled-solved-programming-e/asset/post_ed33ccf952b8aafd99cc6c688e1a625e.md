
# 5 • Program Control

U.5.3 Write a program that reads three integers and if the sum of any two of them is equal to the third one, should display the integers within [0, 10]. Otherwise, the program should read another integers and display how many of them are multiples of 6 or other than 20.

U.5.4 A factory produces small and big bottles. A small one costs $0.008 and a big one $0.002. For orders of more than $200 or more than 3000 bottles in total, there is an 8% discount. For orders of more than $600, the discount is 20%. Write a program that reads the number of small and big bottles ordered and displays the total cost.

U.5.5 Write a program that reads a student's grade and displays its corresponding description, as follows:

- a. (18–20]: Excellent
- b. (16–18]: Very Good
- c. (13–16]: Good
- d. [10–13]: Dangerous Zone
- e. [0–10]: Need Help

U.5.6 Each Ethernet network card is characterized by a unique 48-bit identifier, which is called MAC address. Typically, the MAC address is represented in hex form. To find the type of the address we check the value of the first octet at the left. If it is even, the address is unicast. If it is odd, it is multicast. If all octets are 0xFF, the address is broadcast. For example:

- a. The FF:FF:FF:FF:FF address is broadcast.
- b. The 18:20:3F:20:AB:11 address is unicast, because 18 is even.
- c. The A3:3F:40:A2:C3:42 address is unicast, because A3 is odd.

Write a program that reads a MAC address and displays its type. Assume that the user enters the MAC address in x:x:x:x:x:x form, where each x is a hex.

U.5.7 Write a program that reads the grades of three students in the lab part and their grades in the theory part. The final grade is calculated as: lab_grd*0.3 + theory_grd*0.7. The program should display how many students got a grade between 8 and 10. Do not use more than three variables.

U.5.8 Write a program that reads an annual income and calculates the tax due to the following table:

| INCOME | RATE (%) |
| :--- | :--- |
| 0–12000 | 0 |
| 12001–14000 | 15 |
| 14001–30000 | 30 |
| >30000 | 40 |

For example, if the user enters 18000, the tax due is: tax = (14000-12000)*0.15 + (18000-14000)*0.3.

U.5.9 Write a program that reads a four-digit positive integer and uses the ?: operator to display a message about whether it can be the same in reverse order or not (e.g., the number 7667 can be). Don't use an if statement.

U.5.10 Write a program that reads a floating-point value (e.g., x) and displays the value of $f(x)$, as follows:

```
f(x) = \begin{cases} 8, & x < -5 \\ x', & -5 \le x < 3 \\ x^2-4, & 3 \le x < 12 \\ 6, & x \ge 12 \end{cases}
```

U.5.11 Write a program that reads four integers and displays the pair with the largest sum. For example, if the user enters 10, -8, 17, and 5, the program should display 10+17=27. Don't use the && operator.

U.5.12 Write a program that reads the time in the h:m:s format and displays how much time is left until midnight (i.e., 24:00:00).

U.5.13 Use one `case` statement and the `?` operator to write the program of U.5.5.

U.5.14 Write a program that reads a month number (1 for January, 12 for December), the day (e.g., if the input is January, the valid values are from 1 to 31) and displays the date after 50 days. If case of February, the program should prompt the user to enter the date, which is 28 or 29. For example, if the user enters 3 for month, and 5 for day, the program should display: 4/24.

U.5.15 Write a program that reads three integers and the user's choice and uses the `switch` statement to support three cases. If the user's choice is 1, the program should check if the integers are different and display a message. If it is 2, it should check if any of them are equal and display a message, and if it is 3, it should display how many of them are within [-5, 5].

U.5.16 Write a program that reads numerators and denominators of two fractions and an integer which corresponds to math operation (e.g., 1: addition; 2: subtraction; 3: multiplication; 4: division) and uses the `switch` statement to display the result.

U.5.17 Write a program that reads the current year, the year of a person's birth, and uses the `switch` statement to display the age. Suppose that the age has not two digits. For example, if the user enters 2020 and 1988, the program should display thirty-two.

U.5.18 Write a program that calculates the cost of renting a vehicle, according to the following table:

| VEHICLE | MIBAGE | DAYS 1–2 | DAYS 3–5 | DAYS > 5 |
| :--- | :--- | :--- | :--- | :--- |
| Moto | ≤ 100 | 30 | 25 | 30 |
| | > 100 | 40 | 35 | 30 |
| Auto | ≤ 100 | 60 | 55 | 50 |
| | > 100 | 80 | 70 | 60 |

The program should read the type of the vehicle, the mileage to rent, and use the `switch` statement to display the cost. Also, the program should ask the user if insurance is desired, and if the answer is positive (e.g., number 1 stands for Yes), an extra 5% in the total cost should be charged.

# Loops

Programs often contain blocks of code that must be executed more than once. A statement whose job is to repeatedly execute the same code as long as a controlling expression is true creates a loop. In this chapter, we will discuss: for, while, and do-while which allows us to set up loops as well as break, continue, and goto statements, which can be used to transfer control from one point to another.

# THE FOR STATEMENT

The for statement is one of the loop statements. The general form of the for statement is:

```
for(exp1; exp2; exp3)
  /* loop body that is executed long as exp2 is true. */
```

The three expressions exp1, exp2, and exp3 can be any valid expressions. The execution of the for statement involves the following steps:

1. exp1 is executed only once. Typically, exp1 initializes a variable used in the expressions.
2. The value of exp2 is evaluated. Typically, it is a relational condition. If it is false, the loop terminates and the execution of the program continues with the closing brace.
3. exp3 is executed. Typically, exp3 changes the value of a variable used in exp2.
4. Steps 2 and 3 are repeated until exp2 becomes false.

Generally, the loop terminates either when the exp condition becomes false or if a statement terminates its execution earlier, such as break or return. If the statement in the loop body consists of a single statement, the braces can be omitted. The following program displays the numbers from 0 to 9:```cpp
#include <iostream>
int main() {
  int i;
  for(i = 0; i < 10; i++) // The braces can be omitted
    std::cout << i << '\n';
  return 0;
}
```

# Introduction to C++

Regarding the position of the opening {, a common practice is to put it at the end of the statement, like this:

```cpp
for(i = 0; i < 10; i++) {
```

As I mentioned in the if statement, preference is to put it on a separate line. Let's see the execution steps:

- a. The statement i = 0; is executed.
- b. The condition i < 10 is checked. Since it is true, the program displays 0.
- c. The i++ statement is executed and i becomes 1. The condition i < 10 is checked again. Because it is still true, the program displays 1. This process is repeated until i becomes 10, at which the point i < 10 becomes false and the loop terminates. As a result, the program displays the numbers from 0 to 9.

Let's see another example. Some prefer to use the != operator instead of < in the for condition. They also prefer the prefix form to change the step. For example, they write:

The result is the same. And why do they prefer that way? The reason they prefer the prefix form is the postfix form must save the current value. Since we do not need it there is no reason this extra overhead. For basic types (e.g., int) the compiler will do the optimization and there will be no difference in performance. However, if the type is a complex one (e.g., iterator), then the prefix form is more efficient than generic programming. For example, as we'll see in Chapter 18. As for the !=, this preference possibly related to generic Chapter 26 can be applied to iterators to traverse library containers, while < may not be applicable. So, they always prefer this form, because it may be more efficient in complex types or in the < operator cannot be used.

Note that we can declare a variable in the first part of the statement. Its scope extends up to the variables in Chapter 11. For example:

```cpp
for(int i = 0; i < 10; i++) {
}
```

```cpp
cout << i; /* The compiler will display an error message for undeclared variable,
because i has not been declared in this scope. The scope of i is up to } */
```

The expressions in the for statement may consist of more than one expression separated by the comma operator (/). For example:

```cpp
int a, b;
for(a = 20, b = 10; a >2, b--);
```

In general, avoid using multiple expressions and prefer to use separate expressions to make the for easier to read.
