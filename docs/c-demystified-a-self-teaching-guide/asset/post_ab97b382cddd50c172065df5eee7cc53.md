
```cpp
#include <iostream>
using namespace std;
int main(void) {
    int num, counter, total = 0;
    cout << "How many items do you want to buy: ";
    cin >> num;
    bool keeping = true;
    for (int counter = 1; counter <= num; counter++) {
        if (!(counter % 13 == 0)) {
            total += 3;
        }
    }
    cout << "Total for " << num << " items is $" << total;
    return 0;
}
```

Note You could also use the relational != (not equal) operator, changing the statement to `if (counter % 13 != 0 )`.

## Nesting Loops

You can nest a for loop just as you can nest statements. For example, the following program prints five rows of ten X characters:

```cpp
#include <iostream>
using namespace std;
int main(void) {
    for (int x = 1; x <= 5; x++) {
        for (int y = 1; y <= 10; y++) {
            cout << "X";
        }
        cout << "\n";
    }
    return 0;
}
```

The for loop for (int x = 1; x <= 5; x++) is the outer loop. The for loop for (int y = 1; y <= 10; y++) is the inner loop.

With nested loops, for each iteration of the outer loop, the inner loop goes through all its iterations. By analogy, a clock, minutes the outer loop, seconds the inner loop. In an hour, there are 60 iterations of minutes, but for each iteration of a minute, there are 60 iterations of seconds.

In the rows and columns, the first iteration of the outer loop, the inner loop goes through all ten of its iterations, printing X characters and one new line character. Then, for the next iteration of the outer loop, the inner loop again again through all of its iterations, printing X characters and one new line character. The same thing happens on the third, fourth, and fifth iterations of the outer loop, resulting in five rows of ten X characters.

While nested loops can be used to print rows and columns for tables, they also have uses. For example, the following program prompts for the total number of salespeople as well as the number of salespersons the user input each sale of each salesperson, and afterward displays the average sale for each salesperson. The number of iterations of the outer loop will be the number of salespeople. The number of iterations of the inner loop will be the number of sales per salesperson.

```cpp
#include <iostream>
using namespace std;
int main(void)
{
    int persons, numSales;
    cout << "Enter number of salespeople: ";
    cin >> persons;
    cout << "Enter number of sales per salesperson: ";
    cin >> numSales;
    for (int x = 1; x <= persons; x++)
    {
        int sale, total = 0;
        float average;
        for (int y = 1; y <= numSales; y++)
        {
            cout << "Enter sale " << y << " for salesperson " << x << ":";
            cin >> sale;
            total += sale;
        }
        average = (float)total / numSales;
        cout << "Average sales for salesperson #" << x << " is " << average << endl;
    }
    return 0;
}
```

The input and output could be:
Enter number of salespeople: 2
Enter number of sales per salesperson: 3
Enter sale 1 for salesperson 1: 4
Enter sale 2 for salesperson 1: 5
Enter sale 3 for salesperson 1: 7
Average sales for salesperson #1 is 5.33333
Enter sale 1 for salesperson 2: 8
Enter sale 2 for salesperson 2: 3
Enter sale 3 for salesperson 2: 4
Average sales for salesperson #2 is 5

Note If you place a break or continue keyword in the inner loop, it will affect only that inner loop, and have no effect on the outer loop.

## Summary

You use a loop to repeat the execution of code statements. A loop is a structure that repeats the execution of code until a condition becomes false.

You learned in this chapter how to use one type of loop: the for. However, before discussing the for loop, I showed you how to use increment and decrement operators, which are used in for and other types of loops. I then explained the difference between prefix and postfix when using the increment and decrement operators.

You also learned in this chapter how to use the break keyword to prematurely terminate the current iteration of the loop. You then learned how to use the logical operators as an alternative to the break and continue keywords. You also learned about nesting one loop inside another.

The for loop is generally used when the loop will execute a fixed number of times. However, sometimes the number of times a loop will execute is unpredictable, depending on user input during runtime. For example, in a data entry application, you may want a loop that, upon entry of invalid data, asks the user another opportunity to enter data, or if they want to retry, gives the user another opportunity to enter. The number of times this loop may execute is unpredictable, since it will keep repeating until the user enters data or quits.

The next chapter will show you how to use two other types of loops, the while loop and the do while loop, that work better than a for loop when the number of times it will execute is unpredictable.

## Quiz

1. What does the increment operator do?
2. What does the decrement operator do?
3. Which occurs first, decrementing or the outputting of the value of *num*, in the statement cout << --num?
4. What is an iteration?
5. What is the usual purpose of the first expression in the parentheses following the for keyword?
6. What is the purpose of the second expression in the parentheses following the for keyword?
7. What is the usual purpose of the third expression in the parentheses following the for keyword?
8. Can one or more of the expressions in the parentheses following the for keyword be empty?
9. What is the purpose of the break keyword in a for loop?
10. What is the purpose of the continue keyword in a for loop?
11. If you were going to use nested loops to print rows and columns, which for loop would print the columns—inner or outer?

## Chapter 8: While and Do While Loops

## Overview

The for loop generally is used when the loop will iterate a fixed number of times. However, sometimes the number of times a loop will iterate is unpredictable, depending on user input during runtime. For example, in a data entry application, you may want a loop that, upon entry of invalid data, asks the user whether they want to retry or quit, and if they want to retry, gives the user another opportunity to enter data. The number of times this loop may iterate is unpredictable, since it will keep repeating until the user either enters valid data or quits.

This chapter will show you how to use the while loop, which is a better choice than a for loop when the number of times a loop will iterate is unpredictable.

While the total number of loop iterations may be unpredictable, there are often situations in which the loop will iterate at least once. An example is a loop that displays a menu with various choices, including exiting the program. In this example, the menu always displays at least once; the user cannot choose to exit before being given that choice. In such situations, a do loop, which this chapter will show you how to use, is a better choice than a while loop.

## The While Loop

The while loop is similar to a for loop in that both have the typical characteristics of a loop: the code inside continues until a condition becomes false. The difference between them is in the parentheses following the for and while keywords.

The parentheses following the for keyword consists of three expressions, initialization, condition, and update. By contrast, the parentheses following the while keyword consists only of the condition; you have to take care of any initialization and update elsewhere in the code.

This difference is illustrated by the program that outputs the numbers between 1 and 10. Chapter 7 included the program that outputs the numbers between 1 and 10 using the for loop.

```cpp
#include <iostream>
using namespace std;
int main(void)
{
    for (int num = 1; num <= 10; num++)
        cout << num << " ";
    return 0;
}
```

The same program using the while loop could be

```cpp
#include <iostream>
using namespace std;
int main(void)
{
    int num = 1;
    while (num <= 10)
    {
        cout << num << " ";
        num++;
    }
    return 0;
}
```

> Note The two statements in the body of the while loop could be combined into one statement, cout << num++. Two statements are used instead to make this example easier by eliminating the precedence issue in the statement between the insertion and increment operators.

With the while loop, the integer variable num to be declared and initialized before the loop since it cannot be inside the parentheses following the keyword. Further, num was updated inside the code of the loop using the increment operator. Update can also be done inside the parentheses following the keyword as shown by an example in this stage.

The update of the variable is particularly important with the while loop. Without that update, the loop would be infinite. For example, in the excerpt from this program, if num is not incremented, the loop would be infinite. The value of num would not change from 1, so the condition num <= 10 would always remain true.

```cpp
int num = 1;
```
