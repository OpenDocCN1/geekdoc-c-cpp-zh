The asinhf() and asinhl() functions were introduced by the C99 compiler.

# ### sin()

The sin() family of functions returns the sine of the argument passed to them. The value of argument must be in radians. The signature of the sin() family of functions is as follows:

```
```c
float sinf(float arg);
double sin(double arg);
long double sinl(long double arg);
```
```

The sinf() and sinl() functions were introduced by the C99 compiler. Let's take an example of the sin() function mentioned in Listing 8.4:

Listing 8.4: Usage of sin() function.

```
```c
#include<stdio.h>
#include<math.h>

int main()
{
    double val = -1.0;
    printf("\n The Sine of %f is %f ",val, sin(val));
    getch();
}
```
```

Output of the preceding example is as follows:

```
```
The Sine of -1.000000 is -0.841471
```
```

# ### sinh()

The sinh() family of functions returns the hyperbolic sine of the argument passed to them. The signature of the sinh() family of functions is as follows:

```
```c
float sinhf(float param);
double sinh(double param);
long double sinhl(long double param);
```
```

The sinhf() and sinhl() functions were introduced by the C99 compiler. The sinhf() function is used for the float data type; whereas, the sinhl() function is used for the long double data type.

# ### atan()

The atan() family of functions returns the arc tangent of the argument passed to them. The signature of the atan() family of functions is as follows:

```
```c
float atanf(float param);
double atan(double param);
long double atanl(long double param);
```
```

The atanf() and atanl() functions were introduced by the C99 compiler. The atanf() function is used for the float data type; whereas, the atanl() function is used for the long double data type. Let's take an example of the atan() function mentioned in Listing 8.5:

Listing 8.5: Usage of atan() function.

```
```c
#include<stdio.h>
#include<math.h>

int main()
{
```
```