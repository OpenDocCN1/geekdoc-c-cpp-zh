# One Argument Constructor

Let's now modify the `Counter` class to allow us to initialize its value to anything we want:

```
#include <iostream>
using namespace std;
class Counter {
private:
    int count;
public:
    Counter(int num) { count = num; }
    void incCount() { ++count; }
    int getCount() { return count; }
};
int main() {
    Counter c1(10);
    c1.incCount();
    cout << c1.getCount() << endl;
    // Note that c1(10); is not a call to a function named c1().
    // Instead it calls the constructor Counter() with the
    // specified arguments.
    Counter c2 = 20;
    c2.incCount();
    cout << c2.getCount() << endl;
    // Here is another way for constructor to be called.
    // If a constructor has a single argument, one-arg constructor,
    // we don't have to use the function call syntax. We can use the
    // = operator for initialization.
    Counter c3 = Counter(30);
    c3.incCount();
    cout << c3.getCount() << endl;
    return 0;
}
```

Output:
11
21
31

In this last example, the constructor is called explicitly and initializes c3. Although you can't specify a return value, a constructor, in a sense, does have one. It returns a reference to the object being created.