The vector definition is given in the library vector, which places it in the std namespace. Thus, a file that uses vectors would include the following (or something similar):

```
#include <vector>
using namespace std;
```

# PITFALL Using Square Brackets Beyond the Vector Size

If v is a vector and i is greater than or equal to v.size( ), then the element v[i] does not yet exist and needs to be created by using push_back to add elements up to and including position i. If you try to set v[i] for i greater than or equal to v.size( ), as in

```
v[i] = n;
```

then you may or may not get an error message, but your program will undoubtedly misbehave at some point.

# Vectors

Vectors are used very much like arrays are used, but a vector does not have a fixed size. If it needs more capacity to store another element, its capacity is automatically increased. Vectors are defined in the library <vector>, which places them in the std namespace. Thus, a file that uses vectors would include the following (or something similar):

```
#include <vector>
using namespace std;
```

The vector class for a given Base_Type is written vector <Base_Type>. Two sample vector declarations are

```
vector<int> v; //default constructor
               //producing an empty vector.
vector<AClass> record(20); //vector constructor
                           //for AClass to initialize
                           //20 elements.
```

Elements are added to a vector using the member function push_back, as illustrated below:

```
v.push_back(42);
```

Once an element position has received its first element, either with push_back or with a constructor initialization, that element position can then be accessed using square bracket notation, just like an array element.