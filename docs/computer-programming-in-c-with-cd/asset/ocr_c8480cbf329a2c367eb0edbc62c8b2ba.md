Q12. What is the output of the following program?

```
```cpp
#include <iostream.h>
class BaseSample1 {
    int a;
public:
    BaseSample1(int x) {
        a = x;
    }
    int geta() {
        return a;
    }
};
class BaseSample2 {
    int b;
public:
    BaseSample2(int x)
    {
        b = x;
    }
    int getb() {
        return b;
    }
};
class DerivedNewSample : public BaseSample1, public BaseSample2 {
    int c;
public:
    DerivedNewSample(int x, int y, int z) : BaseSample1(z), BaseSample2(y){
        c = x;
    }
    void show() {
        cout << geta() << ' ' << getb() << ' ';
        cout << c;
    }
};
int main()
{
    DerivedNewSample object(7,17,77);
    object.show();
    return 0;
}
```
```

Ans  The output of the preceding program is as follows:

77 17 7