flag is set and that mag and theta contain valid data. If that is not true, then
this function will produce meaningless results.
One option is to add a comment to the function that warns programmers
about the precondition.

```
void Complex::calculateCartesian ()
// precondition: the current object contains valid polar coordinates\and the polar flag is set
// postcondition: the current object will contain valid Cartesian
coordinates, and both the cartesian
flag and the polar flag will be set
{
    real = mag * cos (theta);
    imag = mag * sin (theta);
    cartesian = true;
}
```

At the same time, I also commented on the postconditions, the things we
will be true when the function completes.
These comments are useful for people reading your programs, but it is
even idea to add code that checks the preconditions, so that we can print
an appropriate error message:

```
void Complex::calculateCartesian ()
{
    if (polar == false) {
        cout <<
            "calculateCartesian failed because the polar representation is invalid"
        << endl;
        exit (1);
    }
    real = mag * cos (theta);
    imag = mag * sin (theta);
    cartesian = true;
}
```

The exit function causes the program to quit immediately. The return value
is an error code that tells the system (or whoever executed the program) that
went wrong.
This kind of error-checking is so common that C++ provides a built-in
function to check preconditions and print error messages. If you include the
assert.h header file, you get a function called assert takes a boolean
value (or a conditional expression) as an argument. That takes as the argument
is true, assert does nothing. If the argument is false, assert prints an error
message and quits. Here is how to use it:

```
void Complex::calculateCartesian ()
```