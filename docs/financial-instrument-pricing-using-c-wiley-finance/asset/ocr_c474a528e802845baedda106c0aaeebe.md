```
{ // Distance between two points in 3d taxi space

    return std::abs(x1 - x2) + std::abs(y1 - y2) + std::abs(z1 - z2);
}
```

We reuse this code to create an algorithm to define the taximan’s distance in two dimensions. We now create a function that is suitable for two-dimensional geometry:

```
std::function<double (double x1,double y1,double x2,double y2)>
Taximan2D =
    std::bind(Taximan3D, std::placeholders::_1,
        std::placeholders::_2,0.0,
        std::placeholders::_3, std::placeholders::_4,0.0);
```

We explain this cryptic code. It is an example of partial function application (see Section 3.2.4) in which a function with six arguments is morphed into one with four arguments. In particular, the third and sixth arguments (that correspond to the z coordinates of the first and second points, respectively) are bound to the value 0.0.

We now use this function to create a new function object similar to the Strategy that we created in Section 3.8:

```
struct Taximan
{ // The scenic route(aka expensive way) from A to B.

    Taximan() {}

    double operator ()(const Point<double>& p,
                    const Point<double>& p2) const
    {
        // For readability
        double x1 = p.First(); double x2 = p2.First();
        double y1 = p.Second(); double y2 = p2.Second();

        double result = Taximan2D(x1, y1, x2, y2);

        return result;
    }
};
```

A test program is:

```
Taximan myTaxi;
Point<double> pC(1.0, 1.0, myTaxi);
Point<double> pD(2.0, 2.0, myTaxi);
std::cout << "Taximan C and D points: " << pC.Distance(pD) << std::endl;
std::cout << "Taximan D and C points: " << pD.Distance(pC) << std::endl;
```

Answer the following questions:

+   a) Write and compile the above code.
+   b) Compare the efficiency of this code that uses std::bind with (possibly) more straightforward code to compute the distance between two points using the two-dimensional taximan algorithm.