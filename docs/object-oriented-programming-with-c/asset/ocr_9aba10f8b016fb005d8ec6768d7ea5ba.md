# Program 9.14 Pure Virtual Function

```
```cpp
#include <iostream>
using namespace std;
class Balagurusamy //base class
{
public:
virtual void example( )=0; //Denotes pure virtual Function
Definition
};
class C:public Balagurusamy //derived class 1
{
public:

void example() {

cout<<“C text Book written by Balagurusamy”;

}     };     class oops:public Balagurusamy //derived class 2     {
public:

void example( )

{

cout<<“C++ text Book written by Balagurusamy”;

}

};
void main( )
{
Exforsys* arra[2];
C e1;
oops e2;
arra[0]=&e1;
```
```