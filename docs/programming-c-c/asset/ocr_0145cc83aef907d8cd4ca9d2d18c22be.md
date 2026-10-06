# 47. Write a C++ program to implement function overloading.

```
#include<iostream>
using namespace std;

int absolute(int);
float absolute(float);

int main() {
int a = -5;
float b = 5.5;

cout << "Absolute value of " << a << " = " << absolute(a) << endl;
cout << "Absolute value of " << b << " = " << absolute(b) << endl;
return 0;
}

int absolute(int var) {
if (var<0) {
var = -var;
returnvar;
}

float absolute(float var){
if (var<0.0) {
var = -var;
returnvar;
}
```

Output
Absolute value of -5 = 5
Absolute value of 5.5 = 5.5

# 48. Write a C++ program to calculate an area of rectangle using encapsulation.

```
#include<iostream>

using namespace std;

class Rectangle
{
int length;
int breadth;
public:
```