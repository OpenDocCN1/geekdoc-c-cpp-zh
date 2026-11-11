Ans.  The output of the preceding program is as follows:

```
10 50
500
100 55
5500
45
```

# Q11.  What is the output of the following program?

```
#include <iostream.h>

class TestA
{
    int i;
public:
    int j, k;
    void seti(int x) {i = x;}
    int geti() {return i;}
};

class TestB : private TestA
{
public:
    TestA::j;
    TestA::seti;
    TestA::geti;
    int a;
};

int main()
{
    TestB object;
    object.j = 5;
    object.a = 600;
    object.seti(80);
    cout << object.geti() << ", " << object.j << ", " << object.a;

    return 0;
}
```

Ans.  The output of the preceding program is as follows:

```
80, 5, 600
```