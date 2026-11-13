be used to initialize private variables directly. When it is used, the compiler gives an error message as shape:: a is not accessible, i.e. the private members are not accessible outside the class, and the private member function display() also cannot be accessed directly by the object. Using the public member function sum(), the private data members are accessed and the addition operation is performed on them.

The private member function can be accessed by the public member functions. The member function can also be defined outside the class, and then their prototype must be declared inside the class.

# Program 1.9

```
#include<iostream.h>
class Shape
{
 int a,b;
 void set_val() //private function.
 {
 a=10,b=20;
 }
 void display()
 {
 cout<<"a="<<a<<"\n"<<"b="<<b;
 }
 public:
 void sum() //public section
 {
 set_val(); //call to private Functions..
 display();
 cout<<"\nSum="<<a+b;
 }
 void sub(void);
};
void Shape::sub()
{
 a=30;
 b=10;
 cout<<"\nSubtraction="<<a-b;
}
void main()
{
 Shape s;
 //s.set_val(); //not accessible
 s.sum();
 s.sub();
}
```

# Output

a=10
b=20