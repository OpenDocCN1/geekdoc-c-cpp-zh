```
```cpp
Volume(double a, double b, double c)
{
    len = a;
    wd = b;
    hgt = c;
    result = len * wd * hgt;
}
void Calcol();
};
void Volume::Calcol()
{
    cout << "Volume is: " << result << endl;
}
int main()
{
    Volume v1(5.2,3.4,7.3), v2(10,5,6);
    v1.Calcol();
    v2.Calcol();
    return 0;
}
```
```

Output:

```
```text
Volume is: 129.064
Volume is: 300
```
```

In Listing 15, the Volume class includes an inline constructor. Volume(double a, double b, double c). Note that the use of the inline keyword is optional for an inline constructor, when the inline constructor is used within the class definition.

Listing 16 shows an example of an inline constructor outside a class by using the inline keyword (you can find this example in the InlineConstructor2.cpp file on the CD in the code\chapter6 folder):

# ▶ Listing 16: Creating an Inline Constructor outside a Class

```
```cpp
#include <iostream.h>

class Volume {
    double len, wd, hgt;
    double result;
public:
    Volume(double a, double b, double c);
    void Calcol();
};
inline Volume::Volume(double a, double b, double c)
{
    len = a;
    wd = b;
```
```