
As mentioned at the end of Section 2.13, we assume that no inverse conversion is available, because the "operator doublet()" that converts "point" to "double" is dropped. Therefore, since both arguments in "operator+" are of type reference-to-constant-point, "operator+" can be called not only with two "point" arguments (like "W+Q") but also with one "point" argument and one "double" argument (like "W+1." or "1.+W"). Indeed, thanks to the implicit double-to-point conversion in Section 2.5, the "double" number "1." is converted to the point (1.0) before being added to "W". Furthermore, thanks to the lack of inverse conversion, there is no ambiguity, because it is impossible to convert "W" to "double" and add it to "1." as "double" numbers.

If one is not interested in implicit conversion because of its extra cost and risks and wants the compiler to announce an error whenever it encounters an attempt to add a "double" number to a "point" object, then one can drop conversion altogether by not specifying default values for the "double" arguments in the constructor in Section 2.3. This way, the constructor expects two "double" arguments rather than one and will not convert a single "double" number to a "point" object.

In the above implementation, the '+' operator is defined as an ordinary function outside the block of the "point" class. This way, however, it is unavailable in the class block, unless it is declared there explicitly as a "friend":

```
friend const point operator+(const point&,const point&);
```

With this declaration, the '+' operator can also be called from inside the class block. Furthermore, it has access to the data fields of its "point" arguments. In fact, it can be defined inside the class block as follows:

```
friend const point operator+(
    const point& p, const point& q){
    return point(p.x+q.x,p.y+q.y);
} // defined as "friend" in the class block
```

The '+' operator can also be implemented as a member function inside the class block as follows:

```
const point operator+(const point& p) const{
    return point(x+p.x,y+p.y);
} // defined as "member" in the class block
```

With this implementation, the '+' operator is still called in the same way (e.g., "W+Q"). The first argument ('W') serves as the current object in the above code, whereas the second argument ('Q') is the concrete argument passed by reference to the above function.

This, however, is a rather nonsymmetric implementation. Indeed, implicit conversion can take place only for the second argument, which is a reference-to-constant-point, but not for the first argument, the current object. Therefore, mixed calls such as "W+1." are allowed, but not "1.+W". This nonsymmetry makes no apparent sense.

The original implementation of "operator+" as an ordinary function outside the class block is more in the spirit of object-oriented programming. Indeed, it avoids direct access to the private data field 'x' or 'y' in "point" objects and uses only the public member functions "X()" and "Y()" to read them. This way, the '+' operator is independent of the internal implementation of "point" objects.

One could also write two more versions of "operator+" to add a "double" number and a "point" object explicitly. These versions increase efficiency by avoiding the implicit conversion used above. They are also implemented as ordinary functions outside the class block:

```
const point operator+(const point& p, double xx){
    return point(p.X()+xx,p.Y());
} // point plus real number
```

```
const point operator+(double xx, const point& p){
    return point(p.X()+xx,p.Y());
} // real number plus point
```

These versions are invoked by the compiler whenever a call such as "W+1." or "1.+W" is encountered, avoiding implicit conversion.

The original implementation of the '+' operator as an ordinary function can also be written in a more elegant way, using the "operator+=" member function defined in Section 2.14:

```
const point
operator+(const point& p, const point& q){
    return point(p) += q;
} // point plus point
```

Thanks to the fact that the "+=" operator is defined in Section 2.14 as a member (rather than a mere friend) of the "point" class, it accepts even temporary "point" objects as concrete arguments. In particular, even the first argument (the current object that is incremented in the "+=" operator) may be a temporary object. This property is used in the above code, where the temporary object "point(p)" returned from the copy constructor is incremented by the "+=" operator before being returned as the output of the entire '+' operator. This elegant style of programming will be used in what follows.

## 2.16 Example: Complex Numbers

In Fortran, the "complex" type is built in and available along with the required arithmetic operations. The programmer can define a complex variable 'c' by writing simply "complex c" and apply arithmetic operations and some other elementary functions to it.

The C and C++ compilers, on the other hand, don't support the "complex" type. If one wants to define and use complex numbers, then one must first define the "complex" class that implements this type. Naturally, the block of the class should contain two "double" fields to store the real and imaginary parts of the complex number and some member operators to implement elementary arithmetic operations. Once the implementation is complete, one can define a "complex" object 'c' simply by writing "complex c" and then apply arithmetic operations to it as if it were built into the programming language.

Some standard C libraries do support complex numbers. Still, the "complex" object implemented here is a good example of object-oriented programming in C++.

This example illustrates clearly how the object-oriented approach works: it provides new objects that can then be used as if they were built into the programming language.

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
