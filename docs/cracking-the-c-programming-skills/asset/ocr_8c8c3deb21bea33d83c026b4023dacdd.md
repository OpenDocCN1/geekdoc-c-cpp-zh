11. Why could someone overload constructor? Select the probable reasons from the below given options. (L2)

+   - (a) To attain more flexibility
+   - (b) Because it is mandatory
+   - (c) To support the concept of copy constructors
+   - (d) To avoid compilation faults

Answer: (a) and (c) It is not mandatory to overload the constructors and if it is not overloaded it would not result in any compilation faults.

12. What is the output of the following code? (L3)

```
~~~cpp
#include <iostream>
using namespace std;
class constructor_overloading
{
    public:
    int a;
    constructor_overloading (int b)
    {
        cout <<"n" << "single parameter"<< endl;
        a = b;
    }
    constructor_overloading ()
    {
        cout <<"n" << "No Argument"<< endl;
    }
};
int main()
{
    constructor_overloading obj1(2);
    cout << obj1.a << endl;
    constructor_overloading obj2;
    return 0;
}
~~~
```

+   - (a) Syntax error
+   - (b) Constructors cannot be overloaded

+   - (c) Single parameter
+     2
+     No argument
+   - (d) Since there is no destructor in the code, it will fail.

Answer: (c) is the correct answer as the constructors can be overloaded and the first one would call the constructor with one argument and the second will call the constructor with none. It would have been preferred if the destructor is added in the code, but, not mandatory.

13. What is the output of the following code? (L3)

```
~~~cpp
#include <iostream>
using namespace std;
class constructor_overloading
{
    public:
    int a,c;
    constructor_overloading (int b)
    {
        cout <<"n" << "simple parameter"<< endl;
        a = b;
    }
    constructor_overloading ()
    {
        cout <<"n" << "No Argument"<< endl;
    }
    constructor_overloading (int d)
    {
        cout <<"p" << "simple parameter"<< endl;
        c = d;
    }
};
int main()
{
    constructor_overloading obj1(2);
    cout << obj1.a << endl;
    constructor_overloading obj2;
~~~
```