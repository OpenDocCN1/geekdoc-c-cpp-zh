It attempts to declare a map that holds references, but the code generates a compiler error instead. Try uncommenting the commented line and see the error message. Here’s an example of what you might see (make sure to add the comment back in when you’re done):

```
error: conflicting declaration 'std::map<StoreMe&, StoreMe&> pointers'
error: 'pointers' has a previous declaration as
  std::map<StoreMe*, StoreMe*> pointers
```

![](bbox=[0.163, 0.264, 0.227, 0.314])

REMEMBER

References are out of the question because the map is making a copy of everything you put in it.

# Working with copies

All C++ containers, not just maps, generally make copies of whatever you stick inside them as shown in the previous section. The Vectors3 example, shown in Listing 6-6, replicates the essential functionality of the Maps2 example shown in Listing 6-5.

# LISTING 6-6: The vector Version of the Maps2 Example

```
```cpp
#include <iostream>
#include <vector>

using namespace std;

class StoreMe {
public:
  int Item;
};

int main() {
  vector<StoreMe> instances;
  StoreMe value1 = {20};
  StoreMe value2 = {40};
  instances.push_back(value1);
  instances.push_back(value2);

  value1.Item = 12345;
  cout << instances[0].Item << endl;
  instances[0].Item = 34567;
  cout << instances[0].Item << endl;
```

```