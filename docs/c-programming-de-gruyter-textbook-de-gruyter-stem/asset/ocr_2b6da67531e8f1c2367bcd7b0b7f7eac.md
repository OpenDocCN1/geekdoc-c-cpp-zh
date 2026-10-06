# 5.2.2 Dynamic Lifetime

Besides the two situations discussed above, all the other objects have a dynamic lifetime. Objects declared to have a dynamic lifetime in local scope are customarily called local lifetime objects. Dynamic lifetimes start from the declaration point and end the ending part of the identifier's scope.

Example 5.2: Lifetime and visibility of variables.

```
//5_2.cpp
#include<iostream>
using namespace std;
int i=1; // i is a global variable with static lifetime
int main() {
    static int a; // a is a static local variable that has static
                  //lifetime, locally visible
    int b=-10; // b, c are local variables that have dynamic
               //lifetime
    int c=0;
    void other(void);
    cout<<"---MAIN--"<<\n";
    cout<< i: ""<<i<<"\" a: ""<<a<<"\" b: ""<<b<<"\" c: ""<<c<<"<<endl;
    c+=8; other();
    cout<<"---MAIN--""<<\n";
    cout<< i: ""<<i<<"\" a: ""<<a<<"\" b: ""<<b<<"\" c: ""<<c<<"<<endl;
    i=i+10; other(); 
}
void other(void) {
    static int a=2;
    static int b;
    //a,b are static local variables that have global lifetime, locally
    //visible, and only initialized when the function is executed for
    //the first time.
    int c=10; // c is a local variable that has dynamic lifetime,
              //should be initialized every time the function is
              //executed.
    a=a+2; i=i+32; c=c+5;
    cout<<"---OTHER--""<<\n";n    cout<< i: ""<<i<<"\" a: ""<<a<<"\" b: ""<<b<<"\" c: ""<<c<<"<<endl;
    b=a;
}
```