return 0;
}

Output:

Enter two numbers:
6
Sum of two number is: 9

# 50. Write a C++ program to overload binary operators.

```
#include <iostream>
using namespace std;
class A {
    int x;
    public:
    A(){}
    A(int i{
        x=i;
    }
    void operator+(A){
        cout<<"The result of the addition of two objects is : "<<m;
    }
    void display();
};
void A ::operator+(A a){
    int m = x+a.x;
    cout<<"The result of the addition of two objects is : "<<m;
}
int main(){
    int x,y;
    cout<<"Enter the First number : ";
    cin>>x;
    cout<<"Enter the Second number : ";
    cin>>y;
    A a1(5);
    A a2(4);
    a1+a2;
    return 0;
}
```

Output:
Enter First Number: 3
ter Second Number: 6
The result of the addition of two numbers is: 9