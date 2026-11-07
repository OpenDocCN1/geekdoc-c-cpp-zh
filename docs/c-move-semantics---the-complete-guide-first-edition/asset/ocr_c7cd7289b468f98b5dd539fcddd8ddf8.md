```
```cpp
std::vector<std::string> createAndInsert()
{
    std::vector<std::string> coll;
    coll.reserve(3);
    std::string s = "data";

    coll.push_back(s);

    coll.push_back(s+s);

    coll.push_back(s);

    return coll;
}
std::vector<std::string> v;
...
v = createAndInsert();
```

**Memory illustration:** Stack and Heap layout showing `coll`, `s`, `s+s`, and `v` during insertion.
```

3. At the end of the statement, the temporary string s+s is destroyed because we no longer need it:

```
```cpp
std::vector<std::string> createAndInsert()
{
    std::vector<std::string> coll;
    coll.reserve(3);
    std::string s = "data";

    coll.push_back(s);

    coll.push_back(s+s);

    coll.push_back(s);

    return coll;
}
std::vector<std::string> v;
...
v = createAndInsert();
```

**Memory illustration:** The temporary `s+s` object is crossed out and destroyed after the statement.
```

Here, we have the first moment where we generate code that is not performing well: we create a copy of a temporary string and destroy the source of the copy immediately afterwards, which means that we unnecessarily allocate and free memory that we could have just moved from the source to the copy.

+   - With the next statement, again we insert s into coll:
+   
+     ```cpp
+     coll.push_back(s);
+     ```