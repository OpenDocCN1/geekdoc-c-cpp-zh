When an object of type Counter is first created, we want its count to be initialized to 0. We could provide a setCount() function to do this and call it with an argument of 0, or we could provide a zeroCount() function which would always set count to 0. However, such functions would need to be executed every time we created a Counter object:

```
Counter cl;
cl.zeroCount();
```

To prove the constructor does its job, let's modify the class:

```
#include <iostream>
using namespace std;
class Counter {
private:
    int count;
public:
    Counter() { count = 0; cout << "I'm here." << endl; }
    void incCount() { ++count; }
    int getCount() { return count; }
};
int main() {
    Counter cl = "c1", c2;

cout << "c1 = " << cl.getCount() << endl;
    cout << "c2 = " << c2.getCount() << endl;
    cl.incCount();
    c2.incCount();
    c2.incCount();
    cout << "c1 = " << cl.getCount() << endl;
    cout << "c2 = " << c2.getCount() << endl;
    return 0;
}
```

Output:
I'm here.
I'm here.
c1 = 0;
c2 = 0;
c1 = 1;
c2 = 2;