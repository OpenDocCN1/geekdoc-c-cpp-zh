+   The object cerr is used for error messages. In a typical environment, cerr behaves the same as cout.

+   The object cin is used for console input.

+   In order to use cin, cout, or cerr, you should place the following directives near the beginning of the file with your program:

```
#include <iostream>
using namespace std;
```

+   There are two forms of comments in C++: Everything following // on the same line is a comment, and anything enclosed in /* and */ is a comment.

+   Do not overcomment.

# ANSWERS TO SELF-TEST EXERCISES

1. int feet = 0, inches = 0;
int feet(0), inches(0);

2. int count = 0;
double distance = 1.5;
int count(0);
double distance(1.5);

3. The actual output from a program such as this is dependent on the system and the history of the use of the system.

```
#include <iostream>
using namespace std;

int main()
{
int first, second, third, fourth, fifth;
cout << " first << " " << second << " " << third
<< " " << fourth << " " << fifth << "\n";
return 0;
}
```

4. 3*x
3*x + y
(x + y)/7  Note that x + y/7 is not correct.
(3*x + y)/(z + 2)

5. bcbc

6. (1/3) * 3 is equal to 0
Since 1 and 3 are of type int, the / operator performs integer division, which discards the remainder, so the value of 1/3 is 0, not 0.3333.... This makes the value of the entire expression 0 * 3, which of course is 0.