# PARAMETERIZING WITH A CLASS

When your template is expecting a class for its parameter (remember, a class, not an instance of a class), you can use the word typename in the template parameter. You then instruct the compiler to create a class based on the template by passing a class name into the template, as in MyContainer<MyClass> inst;. Typically, you use a container class as a template parameter if you have a template that you intend to hold instances of a class. However, instead of using typename, you use class, like so:

```
```cpp
template <class T>
class MyContainer {
public:
    T member;
};
```
```

# Including multiple parameters

You’re not limited to only one parameter when you create a template. For example, the Standard C++ Library has a template called map. The map template works like an array, but instead of storing things based on an index as you would in an array, you store them based on a key and value pair. To retrieve an item from map, you specify the key, and you get back the value. When you create a class based on the map template, you specify the two types map will hold, one for the key and one for the value. These are types, rather than objects or instances. After you specify the types, the compiler creates a class, and inside that class you can put the instances.

To show how this works, instead of using the actual map template, the following example creates a template that works similarly to a map. Instances of classes based on this template will hold only as many items as you specify when you create the class, whereas a real map doesn’t have any limitations beyond the size of the computer’s memory. The MultipleParameters example, shown in Listing 5-5, demonstrates an alternative map template.

# LISTING 5-5: Using Multiple Parameters with Templates

```
```cpp
#include <iostream>

using namespace std;

template<typename K, typename V, int S>
class MyMap {
```
```