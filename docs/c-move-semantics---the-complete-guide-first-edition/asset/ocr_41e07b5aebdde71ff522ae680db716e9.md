So far, there is nothing to optimize and we get the same state as with C++03:

```
```cpp
std::vector<std::string> createAndInsert()
{
    std::vector<std::string> coll;
    coll.reserve(3);
    std::string s = "data";

    coll.push_back(s);

    coll.push_back(s+s);

    coll.push_back(std::move(s));

    return coll;
}

std::vector<std::string> v;
...
v = createAndInsert();
```
```

![](bbox=[0.476, 0.126, 0.757, 0.435])

We have two vectors, v and coll, and two strings, s and its copy, which is the first element in coll. They should all be separate objects with their own memory for the value, because modifying one of them should not impact any of the other objects.

+   - This is where things change. First, let us look at the statement that creates a new temporary string and inserts it into the vector:

```
```cpp
coll.push_back(s+s);
```
```

Again, this statement is performed in three steps:

+   1. We create the temporary string s+s:

```
```cpp
std::vector<std::string> createAndInsert()
{
    std::vector<std::string> coll;
    coll.reserve(3);
    std::string s = "data";

    coll.push_back(s);

    coll.push_back(s+s);

    coll.push_back(std::move(s));

    return coll;
}

std::vector<std::string> v;
...
v = createAndInsert();
```
```

![](bbox=[0.495, 0.621, 0.781, 0.929])