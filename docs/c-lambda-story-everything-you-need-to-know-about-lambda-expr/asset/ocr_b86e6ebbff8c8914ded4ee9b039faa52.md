The example defines a simple functor with operator(). .

While function pointers are usually stateless 1, functors can hold member variables which allow storing state. One example is to count the number of invocations of a callable object in an algorithm. This solution needs to store a counter that is updated with each lambda call:

Functor with a state. Live code @Wandbox

```
#include <algorithm>
#include <iostream>
#include <vector>

struct PrintFunctor {
    PrintFunctor() : numCalls(0) {}
    void operator()(int x) const {
        std::cout << x << '\n';
        ++numCalls;
    }

    mutable int numCalls;
};

int main() {
    std::vector<int> v;
    v.push_back(1);
    v.push_back(2);
    const PrintFunctor visitor = std::for_each(v.begin(), v.end(), PrintFunctor());
    std::cout << "num calls: " << visitor.numCalls << '\n';
}
```

In the above example, we used a member variable numCalls to count the number of invocations of the call operator. Since the call operator is a const member function, I had to use a mutable variable.

As you can easily predict, we should get the following output:

1
2
num calls: 2

We can also "capture" variables from the calling scope. To do that we have to create a member variable in our functor and initialise it in the constructor.

Functor with a 'captured' variable. Live code @Wandbox

```
#include <algorithm>
```