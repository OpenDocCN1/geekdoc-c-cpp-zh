
## SELF-TEST EXERCISES

21. Write an if-else statement that outputs the word High if the value of the variable score is greater than 100 and Low if the value of score is at most 100. The variable score is of type int.

22. Suppose savings and expenses are variables of type double that have been given values. Write an if-else statement that outputs the word Solvent, decreases the value of savings by the value of expenses, and sets the value of expenses to 0, provided that savings is at least as large as expenses. If, however, savings is less than expenses, the if-else statement simply outputs the word Bankrupt and does not change the value of any variables.

23. Write an if-else statement that outputs the word Passed provided the value of the variable exam is greater than or equal to 60 and the value of the variable programs_done is greater than or equal to 10. Otherwise, the if-else statement outputs the word Failed. The variables exam and programs_done are both of type int.

24. Write an if-else statement that outputs the word Warning provided that either the value of the variable temperature is greater than or equal to 100, or the value of the variable pressure is greater than or equal to 200, or both. Otherwise, the if-else statement outputs the word OK. The variables temperature and pressure are both of type int.

25. Consider a quadratic expression, say

x² - x - 2

Describing where this quadratic is positive (that is, greater than 0), involves describing a set of numbers that are either less than the smaller root (which is -1) or greater than the larger root (which is +2). Write a C++ Boolean expression that is true when this formula has positive values.

26. Consider the quadratic expression

x² - 4x + 3

Describing where this quadratic is negative involves describing a set of numbers that are simultaneously greater than the smaller root (+1) and less than the larger root (+3). Write a C++ Boolean expression that is true when the value of this quadratic is negative.

27. What is the output of the following cout statements embedded in these if-else statements? You are to assume that these are embedded in a complete correct program. Explain your answer.

## DISPLAY 2.12 A while Loop

```
1  #include <iostream>
2  using namespace std;
3  int main()
4  {
5      int countDown;
6      cout << "How many greetings do you want? ";
7      cin >> countDown;
8      while (countDown > 0)
9      {
10         cout << "Hello ";
11         countDown = countDown - 1;
12     }
13     cout << endl;
14     cout << "That's all!\n";
15     return 0;
16 }
```

### Sample Dialogue 1

How many greetings do you want? 3
Hello Hello Hello
That's all!

### Sample Dialogue 2

How many greetings do you want? 1
Hello
That's all!

### Sample Dialogue 3

How many greetings do you want? 0
That's all!

The loop body is executed zero times.

```
cout << "Hello ";
countDown = countDown - 1;
```

Therefore, every time the loop body is repeated, "Hello " is output and the value of the variable countDown is decreased by one. After the computer repeats the loop body three times, the value of countDown is decreased to 0 and the program in Display 2.12 and the Boolean expression in parentheses

## DISPLAY 2.13 Syntax of the while Statement

### A Loop Body with Several Statements:

```
1   while ( Boolean_Expression )
2   {
3       Statement_1
4       Statement_2
5       ...
6       Statement_Last
7   }
```

Do NOT put a semicolon here.

body

### A Loop Body with a Single Statement:

```
8   while ( Boolean_Expression )
9       Statement
```

body

are no longer satisfied. So, this while statement ends after repeating the loop body three times.

The syntax for a while statement is given in Display 2.13. The Boolean_Expressions allowed are exactly the same as the Boolean expressions allowed in an if-else statement. Just as in if-else statements, the Boolean expression in a while statement must be enclosed in parentheses. In Display 2.13 we have given the syntax templates for two cases: the case when there is more than one statement in the loop body and the case when there is just a single statement in the loop body. Note that when there is only a single statement in the loop body, you need not include the braces { and }.

Let’s go over the actions performed by a while statement in greater detail. When the while statement is executed, the first thing that happens is that the Boolean expression following the word while is checked. It is either true or false. For example, the comparison

```
countDown > 0
```

is true if the value of countDown is positive. If it is false, then no action is taken and the program proceeds to the next statement after the while statement. If the comparison is true, then the entire body of the loop is executed. At least one of the expressions being compared typically contains something that might be changed by the loop body, such as the value of countDown in the while statement in Display 2.12. After the body of the loop is executed, the comparison is again checked. This process is repeated again and again as long as the comparison continues to be true. After each iteration of the loop body, the comparison is again checked and if it is true, then the entire loop body is executed again. When the comparison is no longer true, the while statement ends.

## DISPLAY 2.15 A do-while Loop

```
#include <iostream>
using namespace std;
int main()
{
    char ans;
    do
    {
        cout << "Hello\n";
        cout << "Do you want another greeting?\n" << "Press y for yes, n for no,\n" << "and then press return: ";
        cin >> ans;
    } while (ans == 'y' || ans == 'Y');
    cout << "Good-Bye\n";
    return 0;
}
```

### Sample Dialogue

```
Hello
Do you want another greeting?
Press y for yes, n for no, and then press return: y
Hello
Do you want another greeting?
Press y for yes, n for no, and then press return: Y
Hello
Do you want another greeting?
Press y for yes, n for no, and then press return: n
Good-Bye
```

unary operators, ++ and --. The ++ operator is called the increment operator and the -- operator is called the decrement operator. They are usually used with variables of type int. If n is a variable of type int, then n++ increases the value of n by one and n-- decreases the value of n by one. So n++ and n-- (when followed by a semicolon) are executable statements. For example, the statements

```
int n = 1, m = 7;
n++;
cout << "The value of n is changed to " << n << endl;
m--;
cout << "The value of m is changed to " << m << endl;
```

yield the following output:

```
The value of n is changed to 2
The value of m is changed to 6
```

And now you know where the “++” came from in the name “C++.”

Increment and decrement statements are often used in loops. For example, we used the following statement in the while loop in Display 2.12:

```
countDown = countDown - 1;
```

However, most experienced C++ programmers would use the decrement operator rather than the assignment statement, so the entire while loop would read as follows:

```
while (countDown > 0)
{
    cout << "Hello ";
    countDown--;
}
```

## PROGRAMMING EXAMPLE Charge Card Balance

Suppose you have a bank charge card with a balance owed of $50 and suppose the bank charges you 2% per month interest. How many months can you let pass without making any payments before your balance owed will exceed $100? One way to solve this problem is to simply read each monthly statement and count the number of months that go by until your balance reaches $100 or more. Better still, you can calculate the monthly balances with a program rather than waiting for the statements to arrive. In this way you will obtain an answer without having to wait so long (and without endangering your credit rating).

After one month the balance would be $50 plus 2% of $50, which is $51. After two months the balance would be $51 plus 2% of $51, which is $52.02. After three months the balance would be $52.02 plus 2% of $52.02, and so on. In general, each month increases the balance by 2%. The program could keep track of the balance by storing it in a variable called balance. The change in the value of balance for one month can be calculated as follows:

```
balance = balance + 0.02 * balance ;
```

If we repeat this action until the value of balance reaches (or exceeds) 100.00 and we count the number of repetitions, then we will know the number of months it will take for the balance to reach 100.00. To do this, we need another variable to count the number of times the balance is changed. Let us call this new variable count. The final body of our while loop will thus contain the following statements:
