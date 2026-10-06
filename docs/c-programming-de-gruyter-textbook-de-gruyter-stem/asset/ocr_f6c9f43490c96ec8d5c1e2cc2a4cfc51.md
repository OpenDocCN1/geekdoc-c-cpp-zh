# 8.6 Program Instance: Improvement on Staff Information Management System — 341

```
int main()    //main()
{
    Fun f; //declare an object of class Fun
    Trapez trap1(f); //declare an object of class Trapz
    cout<<"TRAPZ Int:"<<setprecision(7)<<trap1(@0,2,1e-7)<<endl;

    //calculate and output the result
}
```

In main(), an object f of class Fun and an object trap1 of class Trapz are defined and trap1 is initialized by the object of class Fun. A data member of class Trapz, the reference of abstract class F becomes an alias of object f. A reference operation on base class F in trap1 was performed on objectf of class Fun. Through trap1's calling the overloaded operator(), calculation was implemented in interval [0,2] with an error of less than 1e-7.

# 8.5.4 Execution Result and Analysis

The execution result is:

TRAPZ Int:0.5548952 <

To calculate another function's integral, we can modify the program as follows. The new integrand should be given in class Fun and then out the interval a and b and error control especially when object trap1 calls the overloaded operator(). If there are other integral algorithms, such as the variable size Simpson algorithm, then we should derive a new class, e.g., a class named Simpson, and change the overload function of operator() to a Simpson algorithm. In main function, we also need to define a Simpson object.

This is a complicated example where we solve a problem involving almost all important aspects of object-oriented programming, such as inheritance, operator overload, abstract classes, and so on. It implements polymorphism using abstract classes. It is worthwhile for readers to carefully analyze this program and test to run this program.

# 8.6 Program Instance: Improvement on Staff Information Management System for a Small Corporation

In Chapter 7, we used the staff information management system as an example to illustrate derivation, virtual functions, and virtual classes. There are two drawbacks to the program of Example 7.10:

+   First, the base-class member function pay() is empty. It is necessary but cumbersome to implement its body.