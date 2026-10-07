# MISCELLANEOUS TOPICS

```
J = j;
}
int getI(){return I;}
int getJ(){return J;}
//void setI(int i){I = i;}
```

```
int main() {
X x(1, 2);
cout << x.getI() << " " << x.getJ() << endl;
x.J = 3;
//x.I = 4;
return 0;
}
```

The program will print the integers 1 and 2 to standard output. Removal of the comments before the setI function in the X definition will produce a compile error. The value of a const member variable can be set only within a constructor initializer list. Because we are working with a struct, member variables are public by default and their values can be changed. Thus, it is legal to change the value of the J variable from next to last inside main. The same is not true for I and removing the comment from next to last line will also produce a compilation error.

An equivalently constructor for the Class X

```
X(int i, int j) : I(i), J(j) {}
I = i;
J = j;
```

```
//constEx2.cpp
#include <iostream>
```

```
using namespace std;
class X{
const int I;
static const int J = 2;
```

```
public:
X(int i) : I(i) {}
int getI(){return I;}
int getJ(){return J;}
}
```