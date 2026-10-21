We will study about conversion operators in Chapter 6. There are situations wherein we do not want the compiler to do the automatic conversion. The procedure to be followed in such cases is explained in Section 5.7.

# 5.7 EXPLICIT CONSTRUCTORS

In most cases, automatic conversion adds to readability. It is, therefore, very useful. However, there are times when we can do without such implicit conversion. The creation of the conversion operator can be avoided by using the keyword explicit before the class name while defining the object. If we do not want a form of brother FourthBrother = "Ricky Ponting" to work like brother FourthBrother("Ricky Ponting") then we need to precede the constructor name by the keyword explicit. Let us discuss this using a modified example given in Program 5.4.

```
//ExplicitCons.cpp
#include <iostream>
#include <string>
using namespace std;

class brother
{
    string Name;
public:
    explicit brother(string BrotherName)
    {
        /* See the explicit keyword before the constructor */
        {
            Name = BrotherName;
        }
    }
};

void main()
{
    brother FirstBrother = brother("Steve Waugh");
    brother SecondBrother("Mark Waugh");
    brother ThirdBrother("Gilchrist");

    // The following statement is erroneous
    brother FourthBrother = "Ricky Ponting";

    /* A compiler would flag an error such as "initializing": cannot convert from "char[11]"
    to "brother" */
}
```

# How the Program Works

Why is it that the statement
brother fourthBrother = "Ricky Ponting"
will not work whereas
will work