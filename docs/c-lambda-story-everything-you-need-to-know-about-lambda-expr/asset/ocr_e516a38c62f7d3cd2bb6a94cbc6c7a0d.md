```
#include <iostream>
#include <string>
#include <vector>

struct PrintFunctor {
    PrintFunctor(const std::string& str)
        : strText(str), numCalls(0) {}

    void operator()(int x) const {
        std::cout << strText << x << '\n';
        ++numCalls;
    }

    std::string strText;
    mutable int numCalls;
};

int main() {
    std::vector<int> v;
    v.push_back(1);
    v.push_back(2);
    const std::string introText("Elem: ");
    const PrintFunctor visitor = std::for_each(v.begin(), v.end(),
                                    PrintFunctor(introText));
    std::cout << "num calls: " << visitor.numCalls << '\n';
}
```

In this version, PrintFunctor takes an extra parameter to initialise member variable. Then this variable is used in the call operator. So the expected output is as follows:

+   - Elem: 1
- Elem: 2
- num calls: 2

# Issues with Functors

As you can see, functors are powerful. They are represented by a separate class, and you can design them any way you like.

However, in C++98/03, the problem was that you had to write a function or a functor in a different place than the invocation of the algorithm. This could mean that the code for a function could be dozens or hundreds of lines later or further in the source file.

As a potential solution, you might have tried writing a local functor class, since C++ always has support for that syntax. But that didn't work...

See this code: