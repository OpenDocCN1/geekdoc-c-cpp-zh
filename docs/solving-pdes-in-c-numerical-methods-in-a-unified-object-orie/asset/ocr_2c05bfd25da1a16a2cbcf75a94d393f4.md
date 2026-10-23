The constant polynomials 1 and −1 are defined in a similar way:

```
polynomial<double> one(1,1.);
polynomial<polynomial<double> > One(1,one);
polynomial<double> minus1(1,-1.);
polynomial<polynomial<double> > Minus1(1,minus1);
```

Next, the constructor that takes two "double" arguments is used to define the polynomial 1 − x:

```
polynomial<double> oneMinusx(1.,-1.);
```

Next, the constructor that takes two polynomial arguments is used to define the polynomial of two variables 1 − x − y:

```
polynomial<polynomial<double> >
    oneMinusxMinusy(oneMinusx,minus1);
```

The polynomials of two variables y and x are defined in a similar way:

```
polynomial<polynomial<double> > yy(zero,one);
polynomial<double> x1(0.,1.);
polynomial<polynomial<double> > xx(1,x1);
```

Note that "x1" and "xx" are different kinds of polynomials: "x1" is the polynomial of one variable p(x) = x, whereas "xx" is the polynomial of two variables p(x,y) = x, which doesn't depend on y at all. Similarly, "xxx" below is the polynomial of three variables p(x,y,z) = x, which depends on neither y nor z:

```
polynomial<polynomial<polynomial<double> > >
    xxx(1,xx);
```

We are now ready to define the nodal basis functions p0, p1, p2, and p3 and store them in a list of polynomials of three variables:

```
list<polynomial<polynomial<polynomial<double> > > >
    P(4,xxx);
P(0) = polynomial<polynomial<
    polynomial<double> > >(oneMinusxMinusy,Minus1);
P(2) = polynomial<polynomial<
    polynomial<double> > >(1,yy);
P(3) = polynomial<polynomial<
    polynomial<double> > >(Zero, One);
```

This completes the definition of the nodal basis functions p0, p1, p2, and p3. These definitions can now be used to calculate the integral over the unit tetrahedron of the triple products of three distinct nodal basis functions: