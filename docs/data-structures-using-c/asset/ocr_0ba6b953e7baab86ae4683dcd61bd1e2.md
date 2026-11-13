The first arrangement is similar to arrays, a sequential organization. The second arrangement is a linked list, a linked organization. Now, let us compare both the arrangements. The first method needs continuous empty spaces to accommodate 10 books, whereas the second method can accommodate books in any of the 10 empty places, which may or may not be continuous. Hence, even if a continuous space to keep the 10 books is not available in the second method, the books can be accommodated.

In the first method, we have direct access to any i-th book in the sequence, whereas in the second method, until we traverse through the first i books sequentially, we cannot find where the (i + 1)-th book is kept. In the first method, we must know well in advance how many books are to be kept so that we can reserve the space for the same. However, in the second method, we can keep every new book in the empty location found anywhere in the shelf; we need not reserve a location for the same.

The next point to be taken into consideration is the utilization of shelf space. In the first method, if the number of the books to be kept in a continuous space is not known in advance, this creates two problems. First, we reserve a continuous block, m, of arbitrary size. In general, m denotes maximum size. Suppose the number of books to be kept is n, which is much smaller than m. Then, (m - n) locations remain unused. The second problem is when the number of books n is greater than the reserved space m, we will not be able to accommodate the books in the continuous block.

The next aspect for comparison is with respect to the various operations on the data elements such as insertion and deletion of a book. In the first method, inserting a book at the i-th location needs a shifting of (i to n) books to the right side, each by one position. Similarly, taking out the i-th book from the shelf creates an empty space in the sequence of books. Hence, we need to shift (i + 1 to n) books to the left, each by one position.

The second method needs no shifting of data elements to insert or delete a data element. It only needs a few changes in the tags of the books, which are called links. For the applications where the data elements to be stored are of varying sizes, that is, sequential representation, arrays are inadequate. This leads to an elegant solution, that is, linked organization.

# 6.2.1 Comparison of Sequential and Linked Organizations

Although linked lists are often used in computing, they are not simple to master. However, the flexibility and performance they offer are worth the pain of learning and using them. The brief features of sequential and linked organizations are described here.

**Sequential organization** The features of this organization are the following:

+   1. Successive elements of a list are stored a fixed distance apart.

+   2. It provides static allocation, which means, the space allocation done by a compiler once cannot be changed during execution, and the size has to be known in advance.

+   3. As individual objects are stored a fixed distance apart, we can access any element randomly.