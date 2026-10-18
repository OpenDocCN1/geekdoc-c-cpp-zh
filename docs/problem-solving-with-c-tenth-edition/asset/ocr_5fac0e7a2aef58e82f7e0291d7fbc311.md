26. (1 < x) && (x < 3)

27. a. 0 is false. In the section on type compatibility, it is noted that the int value 0 converts to false.

b. 1 is true. In the section on type compatibility, it is noted that a nonzero int value converts to true.

c. -1 is true. In the section on type compatibility, it is noted that a nonzero int value converts to true.

28. 10
7
4
1

29. There would be no output, since the Boolean expression (x < 0) is not satisfied and so the while statement ends without executing the loop body.

30. The output is exactly the same as it was for Self-Test Exercise 27.

31. The body of the loop is executed before the Boolean expression is checked, the Boolean expression is false, and so the output is

-42

32. With a do-while statement the loop body is always executed at least once. With a while statement there can be conditions under which the loop body is not executed at all.

33. This is an infinite loop. The output would begin with the following and conceptually go on forever:

10
13
16
19

(Once the value of x becomes larger than the largest integer allowed on your computer, the program may stop or exhibit other strange behavior, but the loop is conceptually an infinite loop.)

```
34. #include <iostream>
using namespace std;

int main()
{
    int n = 1;
    while (n <= 20)
    {
```