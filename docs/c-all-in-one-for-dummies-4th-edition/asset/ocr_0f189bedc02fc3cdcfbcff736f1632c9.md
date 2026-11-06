AddIt() works as you expect. You call it as you would any other function and provide a beginning point and an end point within vector. The first two calls to AddIt sum the entire vector, and the third creates an iterator, changes its offset, and then sums a range within vector. Here is the output from this example:

```
30.431
30.431
12.82
```

![](bbox=[0.164, 0.256, 0.227, 0.322])

A random-access iterator can go in either direction. In addition, you can work with individual members within the container supplied to iterator. As a result, the functions you create for iterator must be able to work with the inputs in any order. How you handle this requirement depends on the kind of function you create.

# Locating Values Using the Find Algorithm

The Standard Library contains a number of functions to find something you need within a container. Locating what you need as efficiently as possible is always a good idea. The four common `find()` algorithms are

+   - `find()`
+   - `find_end()`
+   - `find_first_of()`
+   - `find_if()`

The algorithm you use depends on what you want to find and where you expect to find it. You’ll likely use the plain `find()` algorithm most often. The FindString example shows how to locate a particular string within vector. You can use the same approach to locate something in any container type:

```
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main() {
  vector<string> Words;
  Words.push_back("Blue");
```