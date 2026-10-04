Inside the loop, 2 things happen:

>> dereference the iterator—that is, like a pointer, you get the value of the thing iterator is referring to. In this case, you output it. So, the first time through the loop, you are looking at the first element of the vector, which is 18, so 18 is output.

There's a feature in C++ that will let you writing long vector<int>::iterator. You can just use auto, and the compiler will automatically infer the type of the variable needed.

A C++ list is referred to by computer scientists as a linked list. Each element exists in memory, not necessarily contiguous with the next element in the list. Each element has a pointer to the next element in the list and a doubly linked list also has a pointer to the previous.

You can actually use auto in other contexts, to get the type of a automatically variable rather than specifying it. It still has a fixed, size type, but it simplifies the programmer's work.

In very rare cases, iterators can't be dereferenced.

So, if you are at one element, it's easy to get to the next one, and in a doubly linked list, it's also easy to go to the previous one. You can easily see any iterator would go from first until last ending.

The other thing that happens is something that is guaranteed to be possible for every iterator: an increment. This is the ++ you would use for incrementing an index value. It's OK to write ++ before after the iterator: it moves to the next element in the container.

In Program 22_7, you create a vector with 3 elements: 10, 20, and 30 (8). You then declare an iterator named iter(9). You set this to begin and increment it once so that iter is the next element in the vector (d). You can insert command for the vector, passing in iter and the value you want to insert. So, 40 gets inserted before the second element (12).

```
// Program 22_7
// Insertion on a vector
#include <iostream>
#include<vector>
using namespace std;
int main() {
vector<int> v = { 10, 20, 30 };
vector<int>::iterator iter = v.begin(); // Iterator is at first element
iter++; // Now at second element
v.insert(iter, 40);
for (int i = 0; i < v.size(); i++) {
cout << v[i] << endl;
}
}
```

So, in this case, you have a loop that causes the iterator to go through every element in the container, and you print it out.

When you print out the contents of the vector, you see that the elements are in order, as expected.

There's a similar process for erasing data from a container.

This way of iterating through a container like a vector is very common, it's not unusual to see a statement that starts from the beginning of the container and iterates to the end. And because the iterator is usually only defined for that, you loop over elements of the container, it's common to put the declaration into the loop itself.

Iterators are important for specifying routines to insert or erase data in a container.

Inserting and deleting are not very efficient for containers like vectors and dequeues; there's another container that is much better at handling insertion and deletion: the list, related, the forward list.