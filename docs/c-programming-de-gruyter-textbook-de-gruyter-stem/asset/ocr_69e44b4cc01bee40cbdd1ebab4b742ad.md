# 7.6 Program Example: Solving Linear Equations using Gaussian Elimination Method — 303

The return type of the function implementing the complete pivoting elimination approach is an integer. If the program terminates, the return value is 1; otherwise the return value is 0. According to the return value, we can determine the completion status of the solving process.

```
//9_q.cpp file main()
#include "linequ.h" //header file which includes class definitions
int main()
{
    double a[]=\ //coefficient matrix
    {
        0.2368,0.2471,0.2568,1.2671, //the first row
        0.1968,0.2071,1.2168,0.2271, //the second row
        0.1581,0.1675,0.1768,0.1871, //the third row
        1.1161,0.1254,0.1397,0.1490); //the fourth row
    }
    double b[4]={ //the vector on the right side
    {
        1.8471,1.7471,1.6471,1.5471};
    Linequ eq1(4); //define an object of the
    eq1.setLinequ(a,b); //set the equations
    eq1.print(); //output the equations
    eq1.Solve() //solve the equations
    if(eq1.Solve())
        eq1.showX(); //output the solution
    else
        cout<<"Fail"<<endl;
    }
//End of file linequain.cpp
```

In main(), we use a quaternion equation to test our algorithm. Both the coefficients and the vector on the right side of the equations are stored in one-dimensional arrays. Firstly, an object equil of quaternion equations is created. During the creation process, the constructor of the derived class is called. The constructor of the derived class in turn calls the constructor of the base class, and then dynamically allocates memory spaces. Next, the coefficients and the vector on the right side of the equations are initialized, where the selected equations are input into the object equil. The member functions printL, solve, and showX of the object complete the tasks of displaying equations, solving equations, and displaying the solution, respectively.