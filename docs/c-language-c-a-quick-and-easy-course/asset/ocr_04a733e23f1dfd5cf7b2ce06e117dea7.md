As we have seen before, the mathematical functions are stored, mostly, in the file header called math.h. The stdlib.h header file contains some mathematical functions, such as the non-elementary functions abs() and rand(), for absolute value and random number, and the function div(), which provides the quotient and the remainder of a division.

The math.h file defined by ANSI C contains the functions acos(), asin(), atan(), atan2(), ceil(), cos(), cosh(), exp(), fabs(), floor(), fmod(), frexp(), ldexp(), log(), log10(), modf(), pow(), sin(), sinh(), sqrt(), tan() and tanh().

The functions acos(), asin() and atan() provide the arc cosine, arc sine and arc tangent. The function atan2() uses for the arc tangent two arguments x and y, the two cathetus; cosh() is the hyperbolic cosine, whereas exp() and log() are the exponential and logarithm functions in the base e (natural base e = 2.718 ..., the decimal logarithm is log10()); fabs() gives the absolute (non-negative) value, modf() provides the rest of the division between two values, floor() and ceil() respectively provide the smallest and largest integer contained in the argument (floor() in many other languages is int()), pow() calculates the power, with two arguments, frexp() provides a mantissa, from .5 to 1, whereas ldexp() provides the result of x*2^k, for arguments x and k.

Using stdio.h and math.h you may experience the following example:

```
main() {float x,y,w,t; x=4.81; y=cos(2*log(x+1));

w=floor(y); t=pow(4,w); printf("\n%f %f %f",y,w,t);}
```

# Alphanumeric functions

The alphanumeric functions, or string functions, are contained, mostly, in the header files ctype.h and string.h.

In the ANSI standard the functions of the ctype.h file are: isalnum(), isalpha(), iscntrl(), isdigit(), isgraph(), islower(), isprint(), ispunct(), isspace(), isupper(), isxdigit(), tolower() and toupper(). The latter converts an uppercase character (‘upper’), whereas tolower() converts a lowercase character (‘lower’). The other functions check whether the character is of a particular type. So isalnum() checks whether the character is alphanumeric, isalpha() checks if it is letter of the alphabet, iscntrl() checks if it is control character, and so on.

The standard string.h header file contains the functions that follow: memchar(), memcmp(), memcpy(), memmove(), memset(), strcat(), strchr(), strcmp(), strcoll(), strcpy(), strerror(), strlen(), strncat(), strncmp(), strncpy(), strpbrk(), strrchr(), strspn(),