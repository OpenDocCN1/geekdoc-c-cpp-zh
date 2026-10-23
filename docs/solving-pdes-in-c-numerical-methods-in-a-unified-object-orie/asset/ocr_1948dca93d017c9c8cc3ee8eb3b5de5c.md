These new objects can then be viewed as an integral part of the programming language and can add new dimensions and possibilities to it. The programming language develops dynamically by adding more and more objects at higher and higher levels of programming.

Here is the detailed implementation of the "complex" class:

```
#include<stdio.h>
class complex{
    double real;  //  the real part
    double image;  //  the imaginary part
public:
    complex(double r=0.,double i=0.):real(r), image(i){
    } //  constructor

    complex(const complex&c):real(c.real),image(c.image){
    }  //  copy constructor

    ~complex(){
    }  //  destructor
```

In the above constructors, all the work is done in the initialization lists, where memory is allocated for the data fields "real" and "image" with the right values. The bodies of these functions remain, therefore, empty. The destructor above also needs to do nothing, because the default destructor called implicitly at the end of it destroys the data fields automatically.

Because the data fields "real" and "image" are declared before the reserved word "public:", they are private members of the class. Thus, only members and friends of the class can access and change data fields of an object in the class. Still, we’d like other users to be able to read these fields from ordinary functions that are neither members nor friends of the class. For this purpose, we define the following two public member functions that can only read (but not change) the data fields:

```
double re() const{
    return real;
}  //  read real part

double im() const{
    return image;
} //  read imaginary part
```

Next, we define the assignment operator. This operator will enable users to assign the value of a "complex" object ‘d’ to a "complex" object ‘c’ simply by writing "c = d":

```
const complex&operator=(const complex&c){
    real = c.real;
    image = c.image;
    return *this;
}  //  assignment operator
```

Next, we define some member arithmetic operators that change the current "complex" object. For example, the "+=" operator allows users to write "c += d" to add ‘d’ to ‘c’: