```
```
double* x, double* y) {
    *x = r*cos(theta);
    *y = r*sin(theta);
}

void testPolarToCartesian() {
    double r = 2;
    double theta = atan(1);
    double x;
    double y;
    polarToCartesian(r, theta, &x, &y);
    ASSERT_APPROX_EQUAL(x, sqrt(2), 0.0001);
    ASSERT_APPROX_EQUAL(y, sqrt(2), 0.0001);
}
```
```

This code passes the parameters **r** and **theta** by value in the usual way, but passes pointers to the parameters **x** and **y**. These are local variables of the test function. When **polarToCartesian** is called it directly changes these local variables. It is able to do this because it has been passed the memory addresses where the variables **x** and **y** are stored.

There is very little practical difference between passing data using a pointer and passing data using a reference. In the C language, you have to use pass by pointer because the concept of reference does not exist.

In the C++ language, using pass by reference is the preferred approach.

The most practical difference is that the user of the function **polarToCartesian** is forced to use the & symbol to obtain pointers to the variables **x** and **y**. This is, in some regards, a good thing because it makes it clear that **x** and **y** might be modified by the function call. On the other hand, using pointers does add a layer of conceptual difficulty.

The only real difference in what you can achieve using pointers and references is that if you pass a pointer it is not entirely clear whether or not it is acceptable to use pointer operators such as incrementing the pointer with ++ or calling **delete**. On the other hand, if you use pass by reference it is clear that the object won't be deleted and the ++ operator won't be called because you simply cannot apply these operators to a reference. This is why pass by reference is the preferred approach in C++.

Just as with references, you can use the keyword **const** with a pointer. There are two possible ways to combine the keyword **const** with a pointer. Writing **const** on the right of the * means that the pointer itself cannot be modified. Writing **const** on the left of the * means it is *the data that is pointed to* that cannot be modified rather than the pointer itself. This distinction is illustrated in the code below. If you remove the comment characters, the code will not compile.

```
```
void constPointerExamples() {
    const char* ptr = "A string";
```
```