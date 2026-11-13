```
friend void rectangle::display(Shape s );
};
void rectangle::display(Shape sh)
{
    cout<<"x="<<x<<"y="<<sh.y;
}
void main()
{
    clrscr();
    Rectangle r;
    r.set_val(x);
    Shape s1;
    s1.set_val(y);
    r.display(s1);
}
```

# Output

x=10
y=20

In Program 1.19, two classes Rectangle and Shape are declared. Here, rectangle is the friend of shape. The member function of class Rectangle can access the member of class Shape. The display() method displays the values of members of both classes.

# 1.7.4 Function Overloading

C++ provides a facility called function overloading to serve the different functionalities with a common function name. Function overloading allows the developers to define two or more functions with a common name and with different arguments or with a different number of arguments within a class or within a program.

# Example

```
int area(int,int)
int area(int,int,int)
double area(double) //here the function area() has been
//overloaded and differentiated
//based upon data type and number of arguments.
```

# Properties of overloaded functions:

+   - All the overloaded functions should share the common function name.
+   - They should differ with the number of arguments or data types of the arguments.

a. area(int,int)
area(int,int,int)

The above two functions can be overloaded though the data types of the arguments are the same, because they differ in the number of arguments.