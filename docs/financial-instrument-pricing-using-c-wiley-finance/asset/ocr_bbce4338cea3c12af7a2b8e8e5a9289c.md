Some test code is:

```
double d1 = 1.0; double d2 = 20.4;
double f = +1.6F;
std::cout << "Min\n";
std::cout << minNew(d1, d2) << '\n';
std::cout << minNew(d1, f) << '\n';
std::cout << minNew(f, d2) << '\n';
int i = 1; double d3 = -1.0001;
std::cout << minNew(i, d3) << '\n';
```

The examples in this section were taken for pedagogical reasons. The situation could change however, for more complicated algorithms and cases in which pre- and post-processing needs to be carried out on the input arguments and on the algorithm’s return value, respectively.

We now take a more extended example to compute the inner product of two STL containers, for example:

```
// Sums of products + initVal
std::vector<double> vec{ 1.0, 2.0, 3.0, 4.0 };
std::vector<double> vec2{ 4.0, 3.0, 2.0, 1.0 };

double initVal = 0.0;
double ip1 = std::inner_product(std::begin(vec), std::end(vec),
std::begin(vec2), initVal);
std::cout << "Inner product STL: " << ip1 << std::endl;
```

We now wish to create a user-defined function that can handle heterogeneous data types and that uses std::inner_product as internal algorithm. To this end, we create two static member functions, each one delivering a different implementation of the same functionality (note that we use template–template parameters):

```
template < typename T1, typename T2,
    template <typename TC1, typename TAlloc1> class Container1 =
    std::vector,
    template <typename TC2, typename TAlloc2> class Container2 =
    std::vector,

    typename TAlloc1 = std::allocator<T1>, typename TAlloc2 =
    std::allocator<T2>>

class Algorithms
{ // Wrappers/Composition for STL algorithms

public:
    static auto InnerProduct(const Container1<T1, TAlloc1>& con1,
    const Container2<T2, TAlloc2>& con2, const T1& initVal)
        -> typename std::common_type<T1, T2>::type
    {

        // Possible preprocessing on T1 and T2

        // Body
```