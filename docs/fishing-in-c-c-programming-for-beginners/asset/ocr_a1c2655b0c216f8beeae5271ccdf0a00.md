```
{
    counting c1,c2,c3;
    c2=c1++;
    c3=++c2;
    cout<<c2.return_value()<<endl;
    cout<<c3.return_value();
}
```

Output
2
2

# Overloading operator+

Consider the addition of two objects:

```
third=first+second;
```

Since + is not a unary operator, so the syntax of overloading operator+ is:

```
object_return_type operator+(object_return_type& rhs);
```

where rhs= Right most side object which is second in our example.

Consider the following program:

```
typedef unsigned short USHORT;
#include <iostream>
using namespace std;
class Counter
{
    public:
        Counter();
        Counter(USHORT initialValue);
```