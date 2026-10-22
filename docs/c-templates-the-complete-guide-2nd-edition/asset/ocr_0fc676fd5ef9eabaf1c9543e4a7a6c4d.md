```
#include <algorithm>
#include <iterator>

int main()
{
std::vector<Person> authors = { {"David", "Vandevoorde"},
{"Nicolai", "Josuttis"},
{"Douglas", "Gregor"} };

std::copy(project(authors.begin(), &Person::firstName),
project(authors.end(), &Person::firstName),
std::ostream_iterator<std::string>(std::cout, "\n"));
}
```

This program produces: David
Nicolai
Douglas

The facade pattern is particularly useful for creating new types that conform to some specific interface. New types need only expose some small number of core operations (between three and six for our iterator facade) to the facade, and the facade takes care of providing a complete and correct public interface using a combination of CRTP and the Barton-Nackman trick.

# 21.3 Mixins

Consider a simple Polygon class that consists of a sequence of points: Click here to view code image

```
class Point
{
public:
double x, y;
Point() : x(0.0), y(0.0) { }
Point(double x, double y) : x(x), y(y) { }
};

class Polygon
{
private:
std::vector<Point> points;
public:
... //public operations
};
```

This Polygon class would be more useful if the user could extend the set of information associated with each Point to include application-specific data