
![](img/c6f2c4fe3e0701d95a17354ad517147a_26_0.png)

+   - Finally, we come to the assignment of the return value to v:
+     v = createAndInsert();

Here, we really get behavior that can be improved: the usual assignment operator has the goal of giving v the same value as the source value that is assigned. In general, any assigned value should not be modified and should be independent from the object that the value was assigned to. So, the assignment operator will create a deep copy of the whole return value:

![](img/c6f2c4fe3e0701d95a17354ad517147a_26_1.png)

However, right after that, we no longer need the temporary return value and we destroy it:

```
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

![](img/c6f2c4fe3e0701d95a17354ad517147a_27_0.png)

Again, we create a copy of a temporary object and destroy the source of the copy immediately afterwards, which means that we again unnecessarily allocate and free memory. This time it applies to four allocations, one for the vector and one for each string element.

For the state of this program after the assignment in main(), we allocated memory ten times and released it six times. The unnecessary memory allocations were caused by:

+   - Inserting a temporary object into the collection
+   - Inserting an object into the collection where we no longer need the value
+   - Assigning a temporary vector with all its elements

We can more or less avoid these performance penalties. In particular, instead of the last assignment, we could do the following:

+   - Pass the vector as an out parameter:
+     createAndInsert(v); // let the function fill vector v
+   - Use swap():
+     createAndInsert().swap(v);

However, the resulting code looks uglier (unless you see some beauty in complex code) and there is not really a workaround when inserting a temporary object.

Since C++11, we have another option: compile and run the program with support for move semantics.

## 1.1.2 Example Since C++11 (Using Move Semantics)

Let us now recompile the program with a modern C++ compiler (C++11 or later) that supports move semantics:

basics/motiv11.cpp

```
#include <string>
#include <vector>

std::vector<std::string> createAndInsert()
{
    std::vector<std::string> coll;    // create vector of strings
    coll.reserve(3);                  // reserve memory for 3 elements
    std::string s = "data";          // create string object

    coll.push_back(s);                // insert string object
    coll.push_back(s+s);              // insert temporary string
    coll.push_back(std::move(s));     // insert string (we no longer need the value of s)

    return coll;                      // return vector of strings
}

int main()
{
    std::vector<std::string> v;       // create empty vector of strings
    ...
    v = createAndInsert();            // assign returned vector of strings
    ...
}
```

There is a small modification, though: we add a std::move() call when we insert the last element into coll. We will discuss this change when we come to this statement. Everything else is as before.

Again, let us look at the individual steps of the program by inspecting both the stack and the heap.

+   - First, in main(), we create the empty vector v, which is placed on the stack with 0 elements:
+     std::vector<std::string> v;
+   - Then, we call
+     v = createAndInsert();
+     where we create another empty vector coll on the stack and reserve uninitialized memory for three elements on the heap:
+     std::vector<std::string> coll;
+     coll.reserve(3);
+   - Then, we create the string s initialized with "data" and insert it into coll again:
+     std::string s = "data";
+     coll.push_back(s);

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
```
```

![](img/c6f2c4fe3e0701d95a17354ad517147a_29_0.png)

We have two vectors, v and coll, and two strings, s and its copy, which is the first element in coll. They should all be separate objects with their own memory for the value, because modifying one of them will not impact any of the other objects.

+   • This is where things change. First, let us look at the statement that creates a new temporary string and inserts it into the vector:

```
coll.push_back(s+s);
```

Again, this statement is performed in three steps:

+   1. We create the temporary string s+s:

![](img/c6f2c4fe3e0701d95a17354ad517147a_29_1.png)

```
```cpp
std::vector<std::string> v;
...
v = createAndInsert();
```
```

2. We insert this temporary string into the vector coll. However, here something different happens now: we steal the memory for the value from s+s and move it to the new element of coll.

![](img/c6f2c4fe3e0701d95a17354ad517147a_30_0.png)

This is possible because since C++11, we can implement special behavior for getting a value that is no longer needed. The compiler can signal this fact because it knows that right after performing the push_back() call, the temporary object s+s will be destroyed. So, we call a different implementation of push_back() provided for the case when the caller no longer needs that value. As we can see, the effect is an optimized implementation of copying a string where we no longer need the value: instead of creating an individual deep copy, we copy both the size and the pointer to the memory. However, that shallow copy is not enough; we also modify the temporary object s+s by setting the size to 0 and assigning the nullptr as new value. Essentially, s+s is modified so that it gets the state of an empty string. The important point is that it no longer owns its memory. And that is important because we still have a third step in this statement.

3. At the end of the statement, the temporary string s+s is destroyed because we no longer need it. However, because the temporary string is no longer the owner of the initial memory, the destructor will not free this memory.

```
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

![](img/c6f2c4fe3e0701d95a17354ad517147a_31_0.png)

Essentially, we optimize the copying so that we move the ownership of the memory for the value of s+s to its copy in the vector.

This is all done automatically by using a compiler that can signal that an object is about to die, so that we can use new implementations to copy a string value that steals the value from the source. It is not a technical move; it is a semantic move implemented by technically moving the memory for the value from the source string to its copy.

+   - The next statement is the statement we modified for the C++11 version. Again, we insert s into coll, but the statement has changed by calling std::move() for the string s that we insert:
+     coll.push_back(std::move(s));

Without std::move(), the same would happen as with the first call of push_back(): the vector would create a deep copy of the passed string s. However, in this call, we have marked s with std::move(), which semantically means "I no longer need this value here." As a consequence, we have another call of the other implementation of push_back(), which was used when we passed the temporary object s+s. The third element steals the value by moving the ownership of the memory for the value from s to its copy:

## 1.1 Motivation for Move Semantics

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

![](img/c6f2c4fe3e0701d95a17354ad517147a_32_0.png)

Note the following two very important things to understand about move semantics:

+   - std::move(s) only marks s to be movable in this context. It does not move anything. It only says, "I no longer need this value here." It allows the implementation of the call to benefit from the mark by performing some optimization when copying the value, such as stealing the memory. Whether the value is moved is something the caller does not know.
+   - However, an optimization that steals the value has to ensure that the source object is still in a valid state. A moved-from object is neither partially nor fully destroyed. The C++ standard library formulates this for its types as follows: after an operation called for an object marked with std::move(), the object is in a valid but unspecified state.

That is, after calling coll.push_back(std::move(s)); it is guaranteed that s is still a valid string. You can do whatever you want as long as it is valid for any string where you do not know the value. It is like using a string parameter where you do not know which value was passed.

Note that it is also not guaranteed that the string either has its old value or is empty. The value it has is up to the implementers of the (library) function. In general, implementers can do with objects marked with std::move() whatever they like, provided they leave the object in a valid state. There are good reasons for this guarantee, which will be discussed later.

• Again, at the end of createAndInsert() we come to the return statement:

return coll;

It is still up to the compiler whether it generates code with the named return value optimization, which would mean that coll just becomes the return value. However, if this optimization is not used, the return statement is still cheap, because again we have a situation where we create an object from a source that is in a valid but unspecified state.
