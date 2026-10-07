expressions is true, nonzero, the resulting expression has the value true. Otherwise, the expression has the value false. Here are some examples:

```
5 == 5 || 5 == 9 // true because first expression is true
5 > 3 || 5 > 10 // true because first expression is true
5 > 8 || 5 < 10 // true because second expression is true
5 < 8 || 5 > 2 // true because both expressions are true
5 > 8 || 5 < 2 // false because both expressions are true
```

Because the || has a lower precedence than the relational operators, you don't need to use parentheses in these expressions. Table 6.1 summarizes how the || operator works.

Table 6.1 The || Operator

| The Value of expr1 || expr2 |
|---|---|---||
| expr1 == true | expr1 == false | true true |
| expr2 == false | true | false |

C++ provides that the || is a sequence point. That is, any value changes indicated on the left side place before the right side is evaluated. (Or in the newer partance of C++11, the subexpression to the left of the operator is sequenced before the subexpression to the right.) For example, consider the following expression:

```
i < 6 || i == j
```

Suppose i originally has the value 10. By the time the comparison with j takes place, i has the value 11. Also C++ won't bother evaluating the expression on the right if the expression on the left is true, it only takes one expression to make the whole logical true. (The semicolon and the comma operator, recall, are also sequence points.)

Listing 6.4 uses the || operator in an if statement to check for uppercase and lowercase versions of a character. It also uses C++'s string concatenation feature (see Chapter 4,"Compound Types") to spread a single string over three lines.

Listing 6.4 or.cpp

```
// or.cpp -- using the logical OR operator
#include <iostream>
int main() {
		using namespace std;
	cout << "This program will reformat your hard disk\n"
		"and destroy all your data.\\n"
		"Do you wish to continue?\y/n";
}
char ch;
```