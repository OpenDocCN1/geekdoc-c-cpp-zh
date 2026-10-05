
# 852 Introduction to C++

where a key value (e.g., student code) is associated with a set of information (e.g., student data). Given a key value, we can quickly store or retrieve the associated information. Like the set container, each element in a map is uniquely identified by its key value, the keys are unique, and the elements are sorted by key order. Its implementation is based on some kind of balanced tree. When we create a map object we specify the type of key and the type of data it contains. For example, the declaration:

```
map<int, string> m;
```

creates a map object where the key type is int and the data type is string. A third argument can be added to indicate the sorting method to use. The default ordering is ascending. The map class uses the pair-class K, class T template to group the key and the data. In particular, if key is the key type and data_type is the stored data, the type of combined information is pair<key, data_type>. For example, the map object contains pairs of pair<int, string>. To insert elements into a map object, one method is to create a pair object and use the insert() function. For:

```
pair<int, string> p(50, "one"); // The Value of the key is 50.
m.insert(p);
```

or create an anonymous pair object and write direct:

```
m.insert(pair<int, string> (50, "one"));
```

or, each use, the overloaded [] operator that takes the key value as an argument and write:

```
m[50] = "one";
```

To access the data of a pair object we can use the first and second members. For example:

```
pair<int, string> p(50, "one");
out << p.first << ' ' << p.second;
```

Let's see an example of using the map container:

```cpp
#include <iostream>
#include <string>
#include <map>
using namespace std;

int main() {
  map<int, string> m;
  map<int, string>::iterator it;

  m[50] = "one";
  m[40] = "two";
  m[30] = "three";
  m[20] = "four";

  it = m.find(40); // We could declare here the iterator and write
  auto it = m.find(40);
  if(it != m.end()) {
    cout << "Find: " << it->first << ' ' << it->second << endl;
  } else {
    cout << "Not found" << endl;
  }

  m.erase(30);
  cout << "Map after erase: ";
  for(it = m.begin(); it != m.end(); ++it) {
    cout << it->first << ' ' << it->second << endl;
  }
  /* Alternatively, we could write:
  for(const auto& item : m) {
    cout << item.first << ' ' << item.second << endl;
  } */
  return 0;
}
```

Output:
Find: 40 two
Map after erase: 20 four 40 two 50 one

# Some more examples

In many of the examples we've seen so far we used basic types (e.g., integers) for a simple demonstration of STL capabilities. However, STL is used to store and manage objects. For example, let's use the set to create a simple database of students, sorted by grade:

```cpp
#include <iostream>
#include <string>
#include <set>
#include <algorithm>
using namespace std;

class Student
{
private:
    int code;
    string name;
    float grad;
public:
    Student(int c, string n, float g) : code(c), name(n), grad(g) {}
    Student() : code(0), name("None"), grad(0) {}
    friend bool operator<(const Student& s1, const Student& s2) {
        return s1.grad < s2.grad;
    }
    void show() const {
        cout << "C:" << code << " N:" << name << " G:" << grad << endl;
    }
};

void display(const Student& s) {
  s.show();
}

int main() {
  set<Student> s;

  s.insert(Student(200, "two", 3.5));
  s.insert(Student(100, "one", 2.5));
  s.insert(Student(300, "three", 4.5));
  for_each(s.begin(), s.end(), display());
  return 0;
}
```

Output:
C:100 N:one G:2.5
C:200 N:two G:3.5
C:300 N:three G:4.5

As a second example, let's use the same Student class and the map container to create a simple database of students, where the search key is the student's code:

```cpp
int main() {
  map<int, Student, greater<int>> m; /* The sorting is done in code descending order. */
  map<int, Student, greater<int>>::iterator it;

  m[100] = Student(100, "one", 3.5);
  m[200] = Student(200, "two", 4.5);
  m[300] = Student(300, "three", 2.5);

  it = m.find(500);
  if(it != m.end())
    (it)->second.show();
  else
    cout << "Not found" << endl;

  for(it = m.begin(); it != m.end(); ++it)
    (*it).second.show(); // Alternative way, instead of ->
}
```

Output:
Not found
C:300 N:three G:2.5
C:200 N:two G:4.5
C:100 N:one G:3.5

# FUNCTION OBJECTS

A function object or functor is an object to which the () syntax can be applied, similar to a function. To use this syntax, the class must overload the () call operator by defining the operator() function. Let's look at an example:

```cpp
class T {
  private:
    int a;
  public:
    int operator()(int v) {
        a = v;
        return a;
    }
};

int main() {
  T t;
  int i = t(20); // The Value of the key is 20.
  cout << i << endl;
}
```
