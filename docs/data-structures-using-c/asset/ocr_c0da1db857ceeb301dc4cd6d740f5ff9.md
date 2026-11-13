```
line L;
circle C;
rectangle R;
int gd = detect, gm;
initgraph(&gd, &gm, " ");
p = &L;
p->Draw(); // draws a line
p = &C;
p->Draw(); // draws a circle
p = &R;
p->Draw(); // draws a rectangle
}
```

In Program Code A.23, since each derived class should implement its own Draw(), it should be pure. Pure methods must also be declared virtual because we only want to use objects from derived classes. Classes that define pure methods are called abstract classes.

# A.12 OPERATOR OVERLOADING

The mechanism of giving special meaning to an operator for the data type is called operator overloading. It helps to assign additional tasks to an operator and specify its meaning to a class to which the operator is applied. The general syntax for operator overloading is as follows:

```
return type class name::operator op(arguments list)
{
...
};
```

Here, op is the operator being overloaded, which is preceded by the keyword operator, and operator op is the function name.

Let us consider the ADT for complex numbers, Complex, as follows:

```
class Complex
{
double Real, Imag;
public:
Complex()
{
Real = 0.0;
Imag = 0.0
}
Complex(const double real, const double imag)
{
Real = real;
```