In this example, it makes no difference to the output of the program whether you use prefix or postfix increment. The reason is that the statement ++num has only one operator; the same is true of num++. However, there is a difference between prefix and postfix increment when the statement has more than one operator. This is discussed later in this chapter in the section "The Difference Between Prefix and Postfix."

# The Decrement Operator

In the following program, the statement num -= decreases the value of the integer variable num, which was initialized to the value of 2, by 1, so the output will be 1.

```
#include <iostream>
using namespace std;
int main(void)
{
    int num = 2;
    num -= 1;
    cout << num;
    return 0;
}
```

Another way to accomplish the same result is by using the decrement operator, --. The decrement operator, like the increment operator, is unary, operating on one operand which generally is a whole number variable, as an int. We can use the decrement operator simply by changing the program we use just and replacing the statement num -= with the statement num--.

```
#include <iostream>
using namespace std;
int main(void)
{
    int num = 2;
    num--;
    cout << num;
    return 0;
}
```

The same output would occur if you substituted the statement --num for num--:

```
#include <iostream>
using namespace std;
int main(void)
{
    int num = 2;
    --num;
    cout << num;
    return 0;
}
```

As with the increment operator, placing the -- before the variable num is called prefix decrementing, while placing the -- after the variable num is called postfix decrementing.

Also, with the example of the increment operator, in this example it makes no difference to the output of the program you use prefix or postfix decrementing because the statement --num (or num--) has only one operator. However, as discussed in