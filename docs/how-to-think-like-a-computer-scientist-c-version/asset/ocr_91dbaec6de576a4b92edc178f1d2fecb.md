# 14.10. PRIVATE FUNCTIONS

```
assert (polar);
real = mag * cos (theta);
imag = mag * sin (theta);
cartesian = true;
assert (polar && cartesian);
```

The first assert statement checks the precondition (actually just part of it);
t second assert statement checks the postcondition.

In my development environment, I get the following message when I violate an assertion:

Complex.cpp:63: void Complex::calculatePolar(): Assertion 'cartesian' failed.
Abort

There is a lot of information here to help track down the error, including the file name and line number of the assertion that failed, the function name and the contents of the assertion statement.

# 14.10 Private functions

In some cases, there are member functions that are used internally by a class, but should not be invoked by client programs. For example, calculatePolar and calculateCartesian are used by the accessor functions, but there is probable reason clients should call them (although it would not do any harm). If we wanted to protect these functions, we could declare them private the same as we do with instance variables. In that case the complete class definition for Complex would look like:

```
class Complex {
private:
double real, imag;
double mag, theta;
bool cartesian, polar;

void calculateCartesian ();

public:
Complex () { cartesian = false; polar = false; }
```

```
Complex (double r, double i) {
real = r; imag = i;
```