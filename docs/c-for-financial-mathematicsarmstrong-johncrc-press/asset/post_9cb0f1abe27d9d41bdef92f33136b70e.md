
## 18.5 The container set

One useful container class is set. To use it you must `#include <set>`.

One key difference between a set and a vector is that a set does not contain duplicate elements (just like the mathematical concept of a set). Another difference is that the data stored in a set is always sorted.

For this reason, you cannot store arbitrary data in a set, you must be able to compare two elements using the operator <. Two elements a and b are considered to be the same if neither a<b nor b<a.

If you want to store a particular data type in a set you will need to overload the < operator. Actually, this isn’t quite true. You can choose to tell the set to use another function other than < to perform the comparisons if you like, but we will only discuss the standard case where you overload <.

Fortunately the data types one most often wants to store in a set, namely numeric types and string, already have appropriate implementations of <.

Here is an example of how you can insert elements into a set using insert, confirm that the set does not contain duplicates, and then print out the contents of the set using the for syntax.

```cpp
set<int> ints;
ints.insert(1);
ints.insert(3);
ints.insert(2);
ints.insert(3);  // duplicate ignored
ASSERT(ints.size() == 3);
for (auto i : ints) {
    std::cout << "Item " << i <<"\n";
}
```

Note that if you do not mind whether the elements in the set are sorted, you can use an unordered_set instead. It is usually faster to use an unordered_set. See Section 18.9.2 for more information on unordered_set.

## 18.6 The container vector

We are familiar with the container **vector** already, but we have not given a great deal of detail about when it should be used and when other containers should be used.

A **vector** stores its data in memory in a single contiguous region just as happens if you create a block of memory using `new []`. **vector** improves upon creating memory using `new []` yourself in the following ways.

-   (i) A vector stores the size of the memory block as well as just a pointer.
-   (ii) When you add elements to a vector, it will decide if it needs to allocate more memory and, if required, it will allocate a new block of memory and copy the data in. A vector has a *capacity* which is the size of the memory it has allocated and a *size* which is the number of elements it contains. The vector will always make sure the capacity is larger than the size by allocating new memory as needed.
-   (iii) In debug mode, the iterator and the operator `[]` contain extra checks that you are only accessing data that lies inside the vector. This is very helpful for debugging.
-   (iv) A vector obeys all the conventions of the standard template library so it can be used more easily than a raw pointer.

As we have seen already, vectors are easy to use. They are also very fast because they use contiguous blocks of memory which the computer finds easy to work with. In particular you can access the $i$-th element of a vector extremely rapidly. It does not take significantly longer than accessing the first element.

The downside of a vector is that it is very slow to insert a new item in the middle of a vector. The worst case is if you wish to insert a single item at the beginning of a vector. You will then need to copy all the old contents of the vector into new memory locations before inserting the new element. This is illustrated in Figure 18.1.

![](img/70e8b6971c8420e92597c05233ce9700_333_0.png)

**FIGURE 18.1:** Inserting into a vector is $O(N)$. Blank squares indicate unused capacity.

This means that a **vector** is not the right data type to use to store the characters in a spreadsheet document. Nobody wants it to take a long time to insert a single character at the beginning of a document.

We say that the time taken to insert an element into a vector is $O(N)$ where $N$ is the length of the vector. On the other hand, reading a single element at a specified index is $O(1)$. In other words, reading a single item in a vector is independent of the length of the vector. Adding elements to the end of a vector is typically of $O(1)$ unless you are unlucky and the vector has to expand its capacity, in which case it is $O(N)$ as the entire vector has to be copied.

A **set** is faster than a **vector** for inserting data. Inserting is $O(\log N)$. We will explain why when we discuss the very similar **map** container in Section 18.9.1.

## 18.7 The container list

A **list** is very similar to a **vector** but it is designed so that it is easy to insert data at arbitrary points in $O(1)$. In particular, you can add data efficiently to either the front or end of a list. By contrast, with vectors you can only add data at the end efficiently.

This means that the **list** class is very useful for organising priority lists. You can put high-priority items at the front of the list and low-priority items at the end.

Under the covers, each element in a **list** is stored using a data type that looks something like this:

```cpp
class Link {
  Data d;
  Link* next;
  Link* previous;
};
```

Each **Link** is stored in an arbitrary location in memory, but by following the pointer **next** you can always quickly find the next item in the list. If you wish to go backwards you can follow the pointer **prev**. The actual **list** class itself needs to store a pointer to the first and last elements. The situation is depicted in Figure 18.2.

This data structure is called a doubly linked list. You can quickly insert a new element by creating a new **Link** and re-routing a few of the pointers. The changes that need to be made are indicated in Figure 18.3 using bold and dashed arrows. The important point is that the number of changes is independent of the length of the list. This means that insertion takes $O(1)$.

![](img/70e8b6971c8420e92597c05233ce9700_335_0.png)

**FIGURE 18.2:** A doubly linked list storing the numbers 1 to 5.

However, if you want to find the *i*-th element of the list, you have no choice but to run through each element in sequence. This takes *O(i)*.

![](img/70e8b6971c8420e92597c05233ce9700_335_1.png)

**FIGURE 18.3:** The changes needed to insert the number 3.5 into the list.

Here is a code example showing how to insert some items at the beginning and end of a list using **push_front** and **push_back**. We then print out the list.

```cpp
// use a list to store items in priority order
list<string> list;
list.push_back("Drinking");
list.push_back("Dancing");
list.push_front("Exam");
list.push_front("Revision");

std::cout << "Todo list\n";
for (auto item : list) {
    std::cout << "Item " << item << "\n";
}
```

This then prints out:

```
Todo list
Item Revision
Item Exam
Item Drinking
Item Dancing
```

Suppose we now wish to insert an item before “Exam”. The class `list` has a function `insert` but it takes two parameters. The first is an iterator which must be pointing to the point where you want to insert, the second is the data we want to insert. Therefore we will first want to iterate through the list up to the desired point and then call `insert`. The code is below.

```cpp
auto i = list.begin();
while (i != list.end()) {
    if (*i == "Exam") {
        list.insert(i, "Dentist");
        break;
    }
    i++;
}
std::cout << "Todo list\n";
for (auto item : list) {
    std::cout << "Item " << item << "\n";
}
```

As expected, this code will print out the same list but with the item “Dentist” inserted before “Exam”.

Naturally you will think that this code is longer than is necessary and will want to write a helper function to make it easier to insert elements. In fact, C++ already contains a function `find` which makes this code fairly easy.

```cpp
auto iter = find(list.begin(), list.end(), "Exam");
list.insert(iter, "Dentist");
```

The function `find` will search through a range of values looking for a specific item and returns an iterator to that point. To specify the range of values you provide an iterator that points to the beginning of your search region and an iterator that points to the end (i.e., one after the last element).

The function `find` is defined in the library `<algorithm>`. The class `list` is defined in `<list>`.

`<algorithm>` contains a number of helpful functions to perform tasks such as remove specified items from a container, sort the elements of a container, find the smallest element in a container, and so forth.
