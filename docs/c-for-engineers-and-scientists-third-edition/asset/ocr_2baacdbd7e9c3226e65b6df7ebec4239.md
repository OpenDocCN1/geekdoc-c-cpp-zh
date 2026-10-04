# Table 11.3 Inherited Access Restrictions

| Base Class Member | Derived Class-Access Specifier | Derived Class Member |
|---|---|---|
| private | private | inaccessible |
| protected | private | private |
| public | private | private |
| private | public | inaccessible |
| protected | public | protected |
| public | public | public |
| private | protected | inaccessible |
| protected | protected | protected |
| public | protected | protected |

An Example To understand the process of deriving one class from another, examine deriving a Cylinder class from a base Circle class. The definition of the Circle class is as follows:

```
// class declaration section
class Circle
{
protected:
    double radius;
public:
    Circle(double r = 1.0); // constructor
    double calcal();
};

// class implementation section
Circle::Circle(double r)
{
    radius = r;
}

// calculate the area of a circle
double Circle::calcalc()
{
    return(PI * radius);
}
```

Except for substituting the access specifier in place of the usual private specifier for the data member, this code is a standard class definition. The only variable not defined is PI, which is used in the calcalc() function. It’s defined as follows:

```
const double PI = 2.0 * asin(1.0);
```

This definition is simply a “trick” that forces the computer to return the value of PI accurate to as many decimal places as your computer allows. This value is obtained by taking the arcsin of 1.0, which is π/2, and multiplying the result by 2.