# # Iterators

# ## Contents

+   - C6.1 Iterators 493
+   - C6.1.1 Common Iterator Operations 494
+   - C6.1.2 Using Iterator Operations 496
+   - C6.1.3 Implementing an Iterator 497
+   - C6.2 Advanced Iterator Functionality 499

# ## Prerequisites

+   - Chapter 9 List Implementations
+   - C++ Interlude 5 Overloaded Operators and Friend Access

An iterator is an object that traverses a collection of data. During the traversal, you can look at the data entries and process them. You can compare iterators to see if they point to the same entry in a collection, and C++ provides special functions that let you perform other actions with collections, such as searching and counting, when using iterators. Iterators are commonly implemented by overloading operators that correspond to the functions an iterator performs. A container can instantiate an iterator and give it to a client to use to traverse the contained data collection.

# ### C6.1 Iterators

![](bbox=[0.24, 0.74, 0.29, 0.78])

How would you count the number of lines on this page? You could use your finger to point to each line as you counted it. Your finger would keep your place on the page. If you paused at a particular line, your finger would be on the current line, and there would be a previous line and a next line. If you think of this page as a list of lines, you would be traversing the list as you counted the lines.

An iterator is a program component that enables you to traverse a collection of data, such as the data in a list, beginning with the first entry. During one complete traversal, or iteration, each data item is considered once. You control the progress of the iteration by repeatedly asking the iterator to give you a reference to the next entry in the

> An iterator is an object that traverses a collection of like objects