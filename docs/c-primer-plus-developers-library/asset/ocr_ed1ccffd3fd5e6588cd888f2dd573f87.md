# Unordered Associative Containers (C++11)

An unordered associative container is yet another refinement of the container concept. Like an associative container, an unordered associative container associates a value with a key and uses the key to find the value. The underlying difference is that associative containers are based on tree structures, whereas unordered associative containers are based on another form of data structure called a hash table. The intent is to provide containers for which adding and deleting elements is relatively quick and for which there are efficient search algorithms. The four unordered associative containers are called unordered_set, unordered_multiset, unordered_map, and unordered_multimap. Appendix G looks a bit further at these additions.

# Function Objects (a.k.a. Functors)

Many STL algorithms use function objects, also known as functors. A functor is any object that can be used with () in the manner of a function. This includes normal function names, pointers to functions, and class objects for which the () operator is overloaded—that is, classes for which the peculiar-looking function operator() () is defined. For example, you could define a class like this:

```
```
class Linear
{
private:
    double slope;
    double y0;
public:
    Linear(double s1_ = 1, double y_ = 0)
        : slope(s1_), y0(y_) {}
    double operator()(double x) {return y0 + slope * x; }
};
```
```

The overloaded () operator then allows you to use Linear objects like functions:

```
```
Linear f1;
Linear f2(2.5, 10.0);
double y1 = f1(12.5);   // right-hand side is f1.operator()(12.5)
double y2 = f2(0.4);
```
```

Here y1 is calculated using the expression 0 + 1 * 12.5, and y2 is calculated using the expression 10.0 + 2.5 * 0.4. In the expression y0 + slope * x, the values for y0 and slope come from the constructor for the object, and the value of x comes from the argument to operator()().

Remember the for_each function? It applied a specified function to each member of a range:

```
```
for_each(books.begin(), books.end(), ShowReview);
```
```