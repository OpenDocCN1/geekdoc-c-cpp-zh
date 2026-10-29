Assuming istream is a type defined in the namespace MySpace, then p1 will have the type istream as defined in MySpace and p2 will have the type istream as defined in the std namespace.

# Self-Test Exercises

8. What is the output produced by the following program?

```
#include <iostream>
using namespace std;

namespace Hello
{
    void message();
}

namespace GoodBye
{
    void message();
}

void message();

int main()
{
    using GoodBye::message;

    {
        using Hello::message;
        message();
        GoodBye::message();
    }

    message();

    return 0;
}

void message()
{
    cout << "Global message.\n";
}

namespace Hello
{
    void message()
    {
```