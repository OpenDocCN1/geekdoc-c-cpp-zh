```
#include <iostream>
using namespace std;
class Add {
public:
    int sum(int num1, int num2){
        return num1+num2;
    }
    int sum(int num1, int num2, int num3){
        return num1+num2+num3;
    }
};
int main() {
    Add obj;
    //This will call the first function
    cout<<"Output: "<<obj.sum(10, 20)<<endl;
    //This will call the second function
    cout<<"Output: "<<obj.sum(11, 22, 33); <<endl;
    return 0;
}
```

2. Runtime Polymorphism
Function ordering is an example of Runtime polymorphism.

Function Overriding: When child class declares a method, which is already present in the parent class, then this is called function overriding. Here, the child class overrides the parent class.

In case of function overriding, we have two definitions of the same function, one is parent class and one in child class. The call to the function is determined at runtime to decide which definition of the function is to be called. That is the reason, it is called runtime polymorphism.