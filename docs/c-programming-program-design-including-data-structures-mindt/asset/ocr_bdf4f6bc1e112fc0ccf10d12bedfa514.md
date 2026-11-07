+   c. x y - zu / * ts + -
+   d. x y z w + - *

+   12. What is the output of the following program?

```
~~~cpp
#include <iostream>
#include <string>
#include "myStack.h"

using namespace std;

template <class type>
void mystery(stackType<type>& s, stackType<type>& t);

int main()
{
    stackType<string> stack1;
    stackType<string> stack2;
    stackType<string> newStack;

    string fNames[] = {"Chelsea", "Kirk", "David",
                       "Stephanie", "Bianca", "Katie", "Holly"};
    string lNames[] = {"Jackson", "McCarthy", "Miller",
                       "Pratt", "Holman", "Smith", "Klien"};

    for (int i = 0; i < 7; i++)
    {
        s1.push(fNames[i]);
        s2.push(lNames[i]);
    }

    mystery(stack1, stack2, newStack);

    while (!newStack.isEmptyStack())
    {
        cout << newStack.top() << endl;
        newStack.pop();
    }
}

template <class type>
void mystery(stackType<type>& s1, stackType<type>& s2,
             stackType<type>& s3)
{
    while (!s1.isEmptyStack() && !s2.isEmptyStack())
    {
        s3.push(s1.top() + " " + s2.top());
        s1.pop();
        s2.pop();
    }
}
~~~
```