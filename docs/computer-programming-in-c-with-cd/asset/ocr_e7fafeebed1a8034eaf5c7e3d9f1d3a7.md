The following code snippet calls the friend operator function:

```
NegativeNumberShow n(2,27);
…

-n;
…
```

In the preceding code snippet, the compiler resolves -n; as operator -(n):

# TEST YOUR KNOWLEDGE

Q6. Create a program that shows the overloading of the -- operator as a friend function.
Ans.

```
#include <iostream.h>

class UnaryFriendoverload {
public:
    int x, y;
    UnaryFriendoverload() {
        x=0;
        y=0;
    }
    UnaryFriendoverload(int i, int j) {
        x=i;
        y=j;
    }
    friend UnaryFriendoverload operator--(UnaryFriendoverload &ob);
    friend UnaryFriendoverload operator--(UnaryFriendoverload &ob, int
    notuse);
};

UnaryFriendoverload operator--(UnaryFriendoverload &ob)
{
    ob.x--;
    ob.y--;
    return ob;
}

UnaryFriendoverload operator--(UnaryFriendoverload &ob, int)
{
    ob.x--;
    ob.y--;
    return ob;
}
int main()
{
    UnaryFriendoverload obj(10, 10);
```