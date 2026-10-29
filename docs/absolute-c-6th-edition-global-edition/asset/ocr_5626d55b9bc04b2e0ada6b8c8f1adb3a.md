# Random Number Generator

| FUNCTION DECLARATION | DESCRIPTION | HEADER FILE |
|---|---|---|
| int random(int); | The call random(n) returns a pseudorandom integer greater than or equal to 0 and less than or equal to n − 1. (Not available in all implementations. If not available, then you must use rand.) | cstdlib |
| int rand(); | The call rand() returns a pseudorandom integer greater than or equal to 0 and less than or equal to RAND_MAX. RAND_MAX is a predefined integer constant that is defined in cstdlib. The value of RAND_MAX is implementation dependent but will be at least 32767. | cstdlib |
| void srand(unsigned int);\n(The type unsigned int is an integer type that allows only nonnegative values. You can think of the argument type as int with the restriction that it must be nonnegative.) | Reinitializes the random number generator. The argument is the seed. Calling srand multiple times with the same argument will cause rand or random (whichever you use) to produce the same sequence of pseudorandom numbers. If rand or random is called without any previous call to srand, the sequence of numbers produced is the same as if there had been a call to srand with an argument of 1. | cstdlib |

# Trigonometric Functions

These functions use radians, not degrees.

| FUNCTION DECLARATION | DESCRIPTION | HEADER FILE |
|---|---|---|
| double acos(double); | Arc cosine | cmath |
| double asin(double); | Arc sine | cmath |
| double atan(double); | Arc tangent | cmath |
| double cos(double); | Cosine | cmath |
| double cosh(double); | Hyperbolic cosine | cmath |
| double sin(double); | Sine | cmath |
| double sinh(double); | Hyperbolic sine | cmath |
| double tan(double); | Tangent | cmath |
| double tanh(double); | Hyperbolic tangent | cmath |