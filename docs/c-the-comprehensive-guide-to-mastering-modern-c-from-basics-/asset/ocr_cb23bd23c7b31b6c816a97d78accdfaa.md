occasionally needs to be resized. To estimate the effort of resizing, assume the hash table is a vector with approximately as many pointers as the container has elements.

+   - deque has the most degrees of freedom when it comes to implementation. It grows well, at worst like a vector. However, it is more likely that memory is requested in larger chunks and not as much temporary storage is needed.

That's all there is to say about growth. But what about shrinking?

+   - You can't remove anything from an array.

+   - list and forward_list as well as all associative containers manage their elements individually, and removing an element also frees its memory. Only in the case of unordered associative containers might the hash table not be affected by shrinking.

+   - vector does not shrink when you remove elements. The maximum space that a vector once required it will continue to require, even if you delete elements. You can explicitly call shrink_to_fit, which releases (parts of) the excess memory. The implementation may do this, but it doesn't have to. However, all implementations known to me support shrink_to_fit to the next larger power of two. Note that you should not call shrink_to_fit after every removal.

+   - deque can be implemented like vector and therefore has shrink_to_fit, but it can also be implemented with