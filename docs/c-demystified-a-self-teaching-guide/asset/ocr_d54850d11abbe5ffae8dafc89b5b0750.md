# Logical Operators

C++ has logical operators that enable you to combine comparisons in one if or else statement. Table 6-1 lists the logical operators supported by C++ and describes what each does.

# Table 6-1: Logical Operators

| Operator | Name | What It Does |
| --- | --- | --- |
| && | And | Connects relational expressions. Both expressions must be true for the overall expression to be true. |
| || | Or | Connects two relational expressions. If either expression is true, the overall expression is true. |
| ! | Not | Reverses the "truth" of an expression, making a true expression false, and a false expression true. |

# The && & Operator

The && operator is also known as the Logical Operator. It is a binary operator; it takes two Boolean expressions as operands. It returns true only if both expressions are true. If either expression is false, the overall expression is false. Of course, if both expressions are false, the overall expression is false. Table 6-2 illustrates this.

# Table 6-2: The Logical And Operator

| Expression #1 | Expression #2 | Expression #1 && Expression #2 |
| --- | --- | --- |
| true | true | true |
| true | false | false |
| false | true | false |
| false | false | false |

The following program shows the use of the Logical And operator in determining whether the user is eligible to vote, the criteria being that the user must be at least 18 years old and a citizen.

```
#include <iostream>
using namespace std;
int main(void)
{
    int age;
    char choice;
    bool citizen;
    cout << "Enter your age: ";
    cin >> age;
    cout << "Are you a citizen (Y/N): ";
    cin >> choice;
```