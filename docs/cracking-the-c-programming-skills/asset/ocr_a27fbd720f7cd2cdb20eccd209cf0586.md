```
    }
    return 0;
}
```

+   - (a) Throws the compile time error - 'range_error' is not a member of 'std'
+   - (b) Prints Range Overflow
+   - (c) Prints the value of array[index]
+   - (d) None of the above

**Answer:** (a) It is mandatory to include the header stdexcept in order to use the exception classes.

8. Which of the following symbols is used in catch block in order to make the catch block catch any type of exception?

+   - (a) ::
+   - (b) ??
+   - (c) ...
+   - (d) \*\*

**Answer:** (c) ... ellipsis symbol is used in the catch block in order to make it catch any type of exception.

9. Which of the following exception types doesn't get derived from logic_error class? (L2)

+   - (a) Invalid_argument
+   - (b) Domain_error
+   - (c) Out_of_range
+   - (d) Range_error

**Answer:** (d) range_error. It is derived from the class runtime_error.

10. Predict the error of the following code. (L3)

```
#include <iostream>
#include <typeinfo>
struct Chocolate { virtual ~Chocolate() { } };
struct Biscuits { virtual ~Biscuits() { } };
int main()
{
    Chocolate c;
    try {
```

```
    Biscuits& b = dynamic_cast<Biscuits&>(c);
} catch(const std::bad_cast& e)
{
    std::cout << e.what();
}
```

+   - (a) It throws a compile time error
+   - (b) It executes without any exception
+   - (c) It generates std::bad_cast exception and prints the message std::bad_cast
+   - (d) None of the above

**Answer:** (c) It generates bad_cast exception as we are trying to do a dynamic cast of a Chocolate class instance to a Biscuits class instance.

11. Predict the output of the following code, provided a=100 and b=100 (L2)

```
#include <iostream>
using namespace std;
class TestException
{
    int a, b;
    public:
        TestException(int a, int b)
        {
            this->a = a;
            this->b = b;
        }
        int divide()
        {
            std::cout<<"a="<<a<<"b="<<b<<"\n"<<"b/a="<<b/a<<"\n";
            return a/b;
        }
};
int main (void)
{
    try
```