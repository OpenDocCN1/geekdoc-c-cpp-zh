You can also invoke a member function `f1()` with any of the objects and using a pointer to a member function named as `pftr`, which we have created in step 2.
The statement

```
```cpp
x = (o1.*pftr)(v1,v2);
```
```

will invoke the function `f1()` using object `o1` because `pftr` is attached to function `f1()` as per step 2. We assume that `v1` and `v2` are the values of data types `d1` and `d2`, respectively, and the data type of variable `x` is `R`. Similarly, the statement

```
```cpp
x = (o2.*pftr)(v1,v2);
```
```

will invoke the function `f1()` for object `o2`, by passing `v1` and `v2` as arguments and will store return value in `x`.

To illustrate the concept of binding pointers with members of the class, we create a simple class named as Data. The class has private members a, b and resultA and a public member named as resultS. The class has public function input to take the value of variables a and b as input from the user. The function operate() stores the result of addition of members a and b in variable resultA and result of subtraction of a and b in variable resultS. The operate() function returns the value of resultA, which is the result of addition. Notice that, there is no need to return the value of resultS from operate() function because it is anyway a public member of class Data. We will now access all the public members of class Data using the concept of bindable pointers in main() function. Note that, you will not be able to bind the pointers you create in main() function to private members of class Data because private members are not accessible at anyplace outside class. Bindable pointers will not breach the security of data which is provided by access specifiers of C++ in any manner.

```
```cpp
#include<iostream.h>
class Data
{
    private:
        int a,b;
        int resultA;
    public:
        int resultS;
        void input()
        {
                cout<<"Enter values of members a and b:"<<endl;
                cin>>a>>b;
        }
        int operate()
        {
                resultA = a+b;
                resultS=a-b;
                return resultA;
        }
```
```