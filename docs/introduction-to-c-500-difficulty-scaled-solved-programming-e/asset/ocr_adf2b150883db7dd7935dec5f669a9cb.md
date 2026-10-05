# 840 Introduction to C++

```
int main() {
    vector<string> v = {"First", "Second", "Third"};
    int i = count_if(v.begin(), v.end(), islong);
    cout << i << '\\n';
    return 0;
}
```

```
bool islong(const string& s) {
    return (s.size() > 5) ? true : false;
}
```

islong() accepts one argument whose type is that of the element. It is called three times, for each of the three string objects contained in v. Because only one has more than five characters, the program displays 1. Note if we want to compare the size of the string with another value (e.g. 10) we'd have to write another function or define a variable (e.g., size) that we'd change. Both approaches are not flexible. What we really need is to pass the size as a kind of argument in islong(). We'll see later how we can do that with the function objects.

# ITERATORS

An iterator is an object or a simple pointer that points to the elements of the container. The iterator can be used to move through the contents of the container. With iterators we can access the elements of different containers in the same way regardless of the stored data types. The same STL algorithms can be applied to different containers in a uniform way. For example, suppose we search for a value in a vector<int> object:

```
vector<int> vec;
for(i = 0; i < vec.size(); i++)
    if(vec[i] == val) // We search for val.
```

Suppose that we search for a value in a list<int> object, which is a linked list of integers:

```
list<int> lst;
for(i = 0; i < lst.size(); i++)
    if(lst[i] == val) // It is not allowed to write lst[i].
```

Although we use index notation here, we are not allowed to do this because the list container does not provide an overload function of [].
However, with iterators we can search the code in the same way for both containers. The use of iterators is similar to pointers. For example, suppose the name of the object (vector or list) is c. In the case of vector<int>::iterator it; we write:

```
vector<int>::iterator it;
for(it = c.begin(); it != c.end(); ++it)
    if(*it == val)
```