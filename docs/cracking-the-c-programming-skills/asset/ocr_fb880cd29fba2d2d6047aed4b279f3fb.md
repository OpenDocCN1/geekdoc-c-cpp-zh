36. Predict the output of the following. (L2)

```
```cpp
#include <iostream>
using namespace std;
class Inc
{
    private:
        int num;
    public:
        Inc(int b)
        {
            num=b;
        }
        int operator ++() {
            return num=num+1;
        }
        bool operator ==(Inc op1) {
            if(op1.num==this->num)
                return true;
        }
};
int main()
{
    Inc t1(10),t2(0);
    t2=t1;
    if(t1==t2)
        cout<<"Both objects are same";
    else
        cout<<"Both objects are not same";
    return 0;
}
```
```

+   (a) Error since there is no definition for !=
+   (b) Prints both objects are same
+   (c) Prints both objects are not same
+   (d) None of the above

**Answer:** (b) This is a way of overloading relational operators.

37. Say Yes or No: Can you use == operator to compare two strings? (L1)

(a) Yes                         (b) No

**Answer:** (b) No, because, when we overload a binary operator, at least one of the operands should be of type class or any other user defined type.

38. Predict the output of the following code. (L2)

```
```cpp
#include <iostream>
using namespace std;
class Inc
{
    private:
        int num;
    public:
        Inc(int b)
        {
            num=b;
        }
        int operator ++() {
            return num=num+1;
        }
        bool operator !=(Inc op1)
        {
            if(op1.num!=this->num)
                return true;
        }
};
int main()
{
    Inc t1(10),t2(0);
    if(t1!=t2)
        cout<<"Both objects are not same";
    return 0;
}
```
```

+   (a) Prints Both objects are not same
+   (b) Prints nothing