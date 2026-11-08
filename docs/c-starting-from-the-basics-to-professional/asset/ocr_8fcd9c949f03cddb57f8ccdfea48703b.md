```
```cpp
{
    if (nextBox->compare(*largestBox) > 0)
        largestBox = nextBox;
    nextBox = truckload.getNextBox();
}

return largestBox;
}
```
```

Unfortunately, however, this function does not compile! Can you see why not? The root cause of the problem is that both getFirstBox() and getNextBox() have to update the m_current member inside truckload. This implies that they both must be non-const member functions, which in turn implies that neither of these functions can be called on truckload, which is a reference-to-const argument. Nevertheless, using a reference-to-const parameter is the normal thing to do. Nobody would or should expect the searching for the largest Box requires a Truckload to be modified. As it stands, however, it is impossible to traverse the content of a const Truckload, which renders our Truckload objects nearly useless. A proper const Truckload& reference would allow code to traverse the Boxes contained in it, but at the same time prevent it from invoking either AddBox() or RemoveBox().

> **Note** You could try to work around the problem by making the m_current member variable of the Truckload class mutable. That would then allow you to turn both getFirstBox() and getNextBox() into const members. While this may be interesting for you as a bonus exercise, this solution still suffers some drawbacks in general. First, you’d run into problems with nested loops over the same collection. Second, even though concurrency is out of the scope of this discussion, you can probably imagine that using the mutable approach would never allow for concurrent traversals by multiple threads of execution either. In both cases, one m_current pointer would be required per traversal—not one per Truckload object.

The correct solution to this problem is the so-called iterator pattern. The principle is easy enough. Instead of storing the m_current pointer inside the Truckload object itself, you move it to another object that is specifically designed and created to traverse the Truckload. Such an object is called an iterator.

> **Note** Later in this book, you’ll learn that the containers and algorithms of the Standard Library make extensive use of iterators as well. While Standard Library iterators have a slightly different interface than the Iterator class we are about to define for Truckload, the underlying principle is the same: Iterators allow external code to traverse the content of a container without having to know about the data structure’s internals.

Let’s see what that could look like for us. We’ll start from the Truckload class of Ex12_18—the version where PageCache is already a nested class—and add a second nested class called Iterator. Just to show you the possibility, we will also define both nested classes outside of the definition of the outer class.

```
```cpp
export module truckload;
import box;
import <memory>;
import <vector>;
```
```