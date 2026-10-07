bool tooBig(int n){ return n > 100; }
list<int> scores;
..

scores.remove_if(tooBig);
Incidentally, this example shows where a class functor might be useful. Suppose you want to remove every value greater than 200 from a second list. It would be nice if you could pass the cut-off value to tooBig() as a second argument so you could use the function with different values, a predicate can have one argument. If, however, you design a TooBig class, you can use class members instead of function arguments to convey additional information:

```
template<class T>
class TooBig {
private:
  T cutoff;
public:
  TooBig(const T & t) : cutoff(t) {}
  bool operator()(const T & v) { return v > cutoff; }
}
```

Here one value (v) is passed as a function argument, and the second argument (cutoff) is set by the class constructor. Given this definition, you can initialize different TooBig objects to different cut-off values to be used in calls to remove_if(). 16.15 illustrates the technique.

# Listing 16.15 functor.cpp

```
// functor.cpp -- using a functor
#include <iostream>
#include <list>
#include <iterator>
#include <algorithm>
```

```
template<class T> // functor class defines operator()
class TooBig {
private:
  T cutoff;
public:
  TooBig(const T & t) : cutoff(t) {}
  bool operator()(const T & v) { return v > cutoff; }
}
```

```
void outint(int n) {std::cout << n << " ";}
```