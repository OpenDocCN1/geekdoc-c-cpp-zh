# ### 1.1.2 Example Since C++11 (Using Move Semantics)

Let us now recompile the program with a modern C++ compiler (C++11 or later) that supports move semantics:

```
```cpp
#include <string>
#include <vector>

std::vector<std::string> createAndInsert()
{
    std::vector<std::string> coll;  // create vector of strings
    coll.reserve(3);                // reserve memory for 3 elements
    std::string s = "data";         // create string object

    coll.push_back(s);              // insert string object
    coll.push_back(s+s);            // insert temporary string
    coll.push_back(std::move(s));   // insert string (we no longer need the value of s)

    return coll;                    // return vector of strings
}

int main()
{
    std::vector<std::string> v;     // create empty vector of strings
    ...
    v = createAndInsert();          // assign returned vector of strings
    ...
}
```
```

There is a small modification, though: we add a `std::move()` call when we insert the last element into `coll`. We will discuss this change when we come to this statement. Everything else is as before.

Again, let us look at the individual steps of the program by inspecting both the stack and the heap.

+   - First, in `main()`, we create the empty vector `v`, which is placed on the stack with 0 elements:
+   
+     ```cpp
+     std::vector<std::string> v;
+     ```

+   - Then, we call
+   
+     ```cpp
+     v = createAndInsert();
+     ```
+   
+     where we create another empty vector `coll` on the stack and reserve uninitialized memory for three elements on the heap:
+   
+     ```cpp
+     std::vector<std::string> coll;
+     coll.reserve(3);
+     ```

+   - Then, we create the string `s` initialized with `"data"` and insert it into `coll` again:
+   
+     ```cpp
+     std::string s = "data";
+     coll.push_back(s);
+     ```