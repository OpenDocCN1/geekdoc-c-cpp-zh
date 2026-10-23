created by dedicated factory objects and the data can then be processed in an application at a suitable *entry point* in the code.

Some typical applications are:

+   - Modelling data for rainbow and multi-asset options by a tuple with three elements. The first and second elements are themselves tuples containing the data (such as strike and expiration) pertaining to the first and second assets respectively, while the third element contains the value of the correlation between the assets.
+   - Mathematical properties of differential equations encapsulated in reusable tuples.
+   - Essential parameters pertaining to numerical processes, for example step size, tolerances and maximum number of iterations.
+   - Any non-trivial application that needs to be configured from various sources. To this end, we use tuples that client code reads without having to know where the data comes from.

We give a simple example of how to create nested tuples that model people and their whereabouts (it can be seen as a simple database):

```
```cpp
// Nested tuples
// First and last names
typedef std::tuple<std::string, std::string> Name;

// Home address and city and code
typedef std::tuple<std::string, std::string, long> HomeAddress;
typedef std::tuple<std::string, std::string> Location;

// Name + Address + Location
typedef std::tuple<Name, HomeAddress, Location> NHL;

Name pName;
std::get<0>(pName) = std::string("Frankie");
std::get<1>(pName) = std::string("Carbone");

HomeAddress ha;
std::get<0>(ha) = std::string("Sunnyside");
std::get<1>(ha) = 199;

Location loc;
std::get<0>(ha) = std::string("Queens");

std::string code("AK");
std::get<1>(ha) = code;

// Create the top-level (Whole) tuple
NHL nhl;
std::get<0>(nhl) = pName;
std::get<1>(nhl) = ha;
std::get<2>(nhl) = loc;
```
```

We shall discuss composite and nested tuples in later chapters.