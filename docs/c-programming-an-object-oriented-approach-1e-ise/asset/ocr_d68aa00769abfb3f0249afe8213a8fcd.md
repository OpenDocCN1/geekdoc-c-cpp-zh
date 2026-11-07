| Table 7.5 | The public interface for the Circle class |
|---|---|
| **Constructors and Destructor** | |
| Circle :: Circle ()<br>A default constructor to build a circle with length = 0.0 and height = 0.0. | |
| Circle :: Circle (double radius)<br>A parameter constructor to build a circle with the given radius. | |
| Circle :: Circle (const Circle& c)<br>A copy constructor to build a circle the same as an existing circle. | |
| Circle :: ~Circle ().<br>The destructor to clean up the circle object that goes out of scope. | |
| **Accessor Functions** | |
| Circle :: double getRadius () const<br>An accessor function that returns the radius of the host object. | |
| Circle :: double getArea () const<br>An accessor function that returns the area of the host object. | |
| Circle :: double getPerimeter () const<br>An accessor function that returns the perimeter of the host object. | |
| **Mutator Functions** | |
| Circle:: void setRadius (double radius)<br>A mutator function that changes the radius of the host object. | |

# 7.7 DESIGNING CLASSES

In this section we create two new types using classes: one to represent a *fraction* and one to represent a *timer*.

# 7.7.1 Fraction Class

A **fraction**, also called a *rational number*, is a ratio of two integers such as 3/4, 1/2, 7/5, and so on. There is no built-in type in C++ that can represent a fraction; we need to create a new type for it with two data members of type integer. We call the first the *numer* (abbreviation for *numerator*) and the second the *denom* (abbreviation for *denominator*).

We create three constructors, one destructor, some accessors, and some mutators. We also add a private member function called *normalize*, which is used to handle class invariants. We add a private member function called *gcd* that finds the greatest common divisor, as discussed in Chapter 5. This function is called by the *normalize* function.

Note that we play the roles of both the designer and the user, but in real life these two roles are performed by different people.