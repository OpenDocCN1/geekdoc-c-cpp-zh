**NOTES**

On each insertion the size of the queue increases by 1. We have written a function `add()` in class `Queue` to insert elements in the queue, hence `add()` contains a statement

```cpp
size++;
```

to ensure that size of the queue is increased by 1 on each insertion. Keep in mind that the default constructor of `Queue` class is only executed once, which gives initial value to variable `size` as `0`.

We will implement a generic queue using a built-in list of C++. The implementation of `Queue` is very similar to that of `Stack`, the only point to remember is we should not use the same end for insertion and deletion of elements. If insertion of elements is from the back end of the linked list `l1` then the deletion should be from the front end of the list. In the code below, method `add()` is responsible to add elements to the queue; internally, it invokes `push_back()` method of linked list `l1`. This means that we are inserting from back side of the list.

Now if you see the `remove` method it uses `pop_front()`, which removes element from front side of the list. Hence the element first inserted will be first to come out. As seen from the output of the program 10 was first added in the queue which is first to come out of the queue.

```
```cpp
#include<list.h>
   template<class G>
   class Queue
   {
   private:
   list<G> l1;
   int size;
   public:
   Queue()
   {
      size=0;
   }

   void add(G element)
   {
   l1.push_back(element);
   size++;
   }
   G remove()
   {
   G element = l1.front(); //get the front element
   l1.pop_front(); //delete the element from queue
   size--;
   return element;
```
```