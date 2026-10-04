# // VECTOR RESIZING

One of the nice features of vectors is that they can change in size. You've seen one way of doing that—by using the push_back member function. When you use that, you add an element to the back of the vector, increasing its size by 1.

When you call resize, if the new size is larger than the old one, new elements are created and they are initialized with the value 0. If the new size is smaller than the old one, the last elements of the vector are removed.

Another way you can resize a vector is with a member function resize. To resize the vector name, by a period, by a call to resize. You can give one argument, which is the new size that you want the vector to be.

Program 8_11 is an example of resizing a vector. After declaring a vector with a name, you call resize on that, with an argument of 5. This will cause the vector to have a size of 5 instead of 0. And after resizing, you print out the vector elements after see 5 elements, each with the value 0.

// Program 8_12
// Vector resizing and initializinginitializing
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v(3);
    v.resize(5, 1);
    cout << "Vector resized : ";
    for (int i = 0; i < v.size(); i++) {
        cout << v[i] << " ";
    }
cout << endl;
}

```
// Program 8_11
// Vector resizing
#include <iostream>
#include <vector>
using namespace std;

int main() {
vector<int> v;
v.resize(5);
cout << "Vector resized : ";
for (int i = 0; i < v.size(); i++) {
cout << v[i] << " ";
}
cout << endl;
```

There's another version of the resize function, that takes 2 arguments (Program 8_12). Just like initializing the constructor can take 1 argument, specifying just size, or 2 arguments, with the first specifying size and the second specifying initial value for the elements, you have the same thing here.

This example has two parts: First, you create a vector with an initial size of 3. Because you did not specify any initial values, that vector will have 3 elements, each of which has the value 0.
Next, you have a command, v.resize(5,1), that will resize the vector to size of 5. And the new elements of the vector will be initialized with the value 1. So, when you print the vector's elements, you see 5 elements, the first 3 having the value 0 and the last 2 having the value 1.