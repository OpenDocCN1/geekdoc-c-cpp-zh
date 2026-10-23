(13.39). Then we have \(f^{(p)}(x)-S^{(p)}(x)=o(\|\Delta_k\|^{3-p})\) (\(p=0, 1, 2, 3\)) (where \(f^{(p)}(x)\) is the \(p\)th derivative of \(f\) with respect to \(x\)).

# 13.6 SOME HANDY UTILITIES

In this chapter we examined a number of algorithms and their implementation in C++. In particular, the numerical methods produced an array of values as output. But how do we know that the results are accurate and that the algorithm is run-time efficient? We focus on accuracy and we discuss how to execute *initial tests*. Some attention areas are:

+   - A1: We need an exact or de-facto exact solution that we can test the approximate solutions against.
+   - A2: What is the maximum error (measured in some norm) between exact and approximate solutions and at which points in index space does it occur?
+   - A3: What is the error (measured in some norm) between exact and approximate solutions at some randomly chosen point?
+   - A4: In which subinterval is a given point?
+   - A5: Create a mesh array.
+   - A6: Create an array of values from functions of arity one and two.

We have used a number of these choices when testing the code in this chapter. For A2 the return type is a tuple consisting of the maximum error and where that error occurs:

```
double LInfinityNorm(const std::vector<double>& v1,
                    const std::vector<double>& v2)
{ // Max of absolute value of elements of v1 - v2

    double result = std::abs(v1[0] - v2[0]);

    for (std::size_t j = 1; j < v1.size(); ++j)
    {
        result = std::max<double>(result, std::abs(v1[j] - v2[j]));
    }

    return result;
}
```

```
std::tuple<double,std::size_t> HotSpotError(
                              const std::vector<double>& v1,
                              const std::vector<double>& v2)
{ // Max abs value of elements of v1 - v2; identify *where* it occurs

    double result = std::abs(v1[0] - v2[0]);
    std::size_t index = 0;

    for (std::size_t j = 1; j < v1.size(); ++j)
    {
```