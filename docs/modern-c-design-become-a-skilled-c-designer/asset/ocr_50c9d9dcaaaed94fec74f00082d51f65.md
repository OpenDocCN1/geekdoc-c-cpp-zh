solution, and my preferred choice, would be to simply define a struct as in

```
struct Complex {
 double re;
 double im;
 };
```

to complement the interface functions, replacing the current use of double with Complex. While this new Complex struct does duplicate the storage of the standard complex class, we cannot use the standard complex class in a pure C interface.

# 8.2.1.3 Modifying Commands

Modifying commands to work with complex numbers is really quite easy since the C++ library provides overloads for all of the mathematical operations required by our calculator. Minus the syntactic changes of replacing Stack with Stack<complex<double>> (hopefully we’ve aliased that somewhere) and swapping complex<double> for double in