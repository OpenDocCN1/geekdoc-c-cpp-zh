
```cpp
LISTING 6-4: (continued)

int main() {
    map<string, string> marriages;
    marriages["Tom"] = "Suzy";
    marriages["Harry"] = "Harriet";

    cout << marriages["Tom"] << endl;
    cout << marriages["Harry"] << endl;
    return 0;
}
```

To use map, you declare a variable of class map, supplying two template parameters, the key class and the value class, which are both string in the example. To store a map value, you place a key inside brackets and set it equal to a value:

```
marriages["Tom"] = "Suzy";
```

To retrieve that particular item, you supply the key in brackets:

```cpp
cout << marriages["Tom"] << endl;
```

When you run this example, you see the following two strings as output:

```
Suzy
Harriet
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_663_0.png)

**REMEMBER**

Even though the keys can be any type or class, you must specify the type or class you're using when you set up map. After you do that, you can use only that type for the particular map. Thus, if you say that the keys will be strings, you cannot then use an integer for a key, as in `marriages[3] = "Suzy";`.

### Containing instances, pointers, or references

One of the most common discussions you encounter when people start talking about how to use the container templates is whether to put instances in the containers, pointers, or references. For example, which of the following should you type?

```cpp
vector<MyClass>
vector<MyClass *>
vector<MyClass &>
```

In other words, do you want your container to store the actual instance (whatever that might mean), a reference to the actual instance, or a pointer to the instance? To explore this idea, look at the Maps2 example in Listing 6-5. Here, you're trying out the different ways of storing things in map: instances, pointers, and references.

### **LISTING 6-5:** Making Decisions: Oh, What to Store?

```cpp
#include <iostream>
#include <map>

using namespace std;

class StoreMe {
    public:
        int Item;
};

bool operator < (const StoreMe & first,
const StoreMe & second) {
    return first.Item < second.Item;
}

int main() {
    // First try storing the instances
    map<StoreMe, StoreMe> instances;
    StoreMe key1 = {10}; // braces notation!
    StoreMe value1 = {20};
    StoreMe key2 = {30};
    StoreMe value2 = {40};
    instances[key1] = value1;
    instances[key2] = value2;

    value1.Item = 12345;
    cout << instances[key1].Item << endl;
    instances[key1].Item = 34567;
    cout << instances[key1].Item << endl;

    // Next try storing pointers to the instances
    map<StoreMe*, StoreMe*> pointers;
    StoreMe key10 = {10};
    StoreMe value10 = {20};
    StoreMe key11 = {30};
    StoreMe value11 = {40};
```

*(continued)*

```cpp
pointers[&key10] = &value10;
pointers[&key1] = &value11;

value10.Item = 12345;
cout << (*pointers[&key10]).Item << endl;

// Finally try storing references to the instances.
// Commented out because it causes an error.)
// map<StoreMe&, StoreMe&> pointers;
return 0;
}
```

To create the instances of StoreMe, you use the braces notation. You can do that when you have no constructors. So the line

```cpp
StoreMe key1 = {10};
```

creates an instance of StoreMe and puts 10 in the Item property. To create an individual instances entry, you need both a key and a value instance of StoreMe. You then use the key to provide a name for the value stored in the map. Consequently, instances contains two entries consisting of two StoreMe objects each. Here’s what you see when you run the application:

```text
20
34567
12345
```

This output doesn’t precisely match expectations because the code changes the Item property in value1:

```cpp
value1.Item = 12345;
```

When the code outputs the value of instances[key1].Item, you see an output of 20, not 12345. That means that the value stored in map is a copy, not the original. However, when the code changes the value in instances like this:

```cpp
instances[key1].Item = 34567;
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_665_0.png)

the value portion of the instances entry does change. You see 34567 as output. Consequently, when working with map instances, you must modify the map entry directly.

It attempts to declare a map that holds references, but the code generates a compiler error instead. Try uncommenting the commented line and see the error message. Here’s an example of what you might see (make sure to add the comment back in when you’re done):

```
error: conflicting declaration 'std::map<StoreMe&, StoreMe&> pointers'
error: 'pointers' has a previous declaration as
  std::map<StoreMe*, StoreMe*> pointers
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_667_0.png)

**REMEMBER**

References are out of the question because the map is making a copy of everything you put in it.

### Working with copies

All C++ containers, not just maps, generally make copies of whatever you stick inside them as shown in the previous section. The Vectors3 example, shown in Listing 6-6, replicates the essential functionality of the Maps2 example shown in Listing 6-5.

### **LISTING 6-6:** The vector Version of the Maps2 Example

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

```cpp
vector<StoreMe*> pointers;
StoreMe value10 = {20};
StoreMe value11 = {40};
pointers.push_back(&value10);
pointers.push_back(&value11);

value10.Item = 12345;
cout << (*pointers[0]).Item << endl;
return 0;
}
```

Oddly enough, the output from this example is precisely the same as the Maps2 example and for the same reason. Whether the container is a vector or a map doesn't matter; both of them hold copies of the objects or pointers you provide. Consequently, you can remember these two rules about deleting your original objects:

- **When the container holds instances:** If you're putting instances in the container, you can delete the original instances after they're added. This is okay because the container has its own copies of the instances.
- **When the container holds pointers:** If you're putting pointers in the container, you don't want to delete the original instances because the pointers in the container still point to these instances.

It's up to you to decide which method is better. But here are a couple of things to consider:

- **Keeping instances around:** If you don't want to keep instances lying around, you can put the instances in the container, and it will make copies.
- **Copyability:** Some classes, such as classes filled with pointers to other classes or classes that are enormous, don't copy well. In that case, you may want to put pointers in the container.

### Comparing instances

When you work with classes that contain other classes (such as vector), you need to provide the class with a way to compare two things. The following sections describe how to provide comparison capability when working with containers.

### Performing comparisons

The previous section provides details on two issues you must resolve when comparing objects. Here’s how to resolve these two issues: If you’re dealing with your own classes, in addition to setting up a container class, you also provide a function that compares two instances of your own class. Your comparison function can determine whether two classes are equal, the first is less than the second, or the first is greater than the second.

![](img/128ab511de4e7360e167e3b15cdd5dd0_670_1.png)

At first, how less than and greater than can apply to things like an Employee class may not seem apparent. But the idea behind less than and greater than is to give the container class a way to determine a sort order. For example, you might choose to sort an Employee class in one of these ways:

- Social Security number
- Last name, first name
- First name, last name
- Employee ID
- Address
- Organizational department
