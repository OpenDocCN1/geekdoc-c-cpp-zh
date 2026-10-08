and telephone numbers. This is the kind of program for which different approaches appear
“simple and obvious” to people of different backgrounds. The Entry class from §11.5 can be used
to hold a simple phone book entry. Here, we deliberately ignore many real-world complexities,
such as the fact that phone numbers do not have a simple representation as a 32-bit int.

# 12.2 vector

The most used standard-library container is vector. A vector is a sequence of elements of a given
type. The elements are stored continuously in memory. A typical implementation of vector
(§5.2.2, §6.2) will consist of a handling pointers to the first, one-past-the-last
and one-past-the-last allocated space (§13.1) (or the equivalent information represented
as a pointer plus offsets:

![](bbox=[0.238, 0.333, 0.725, 0.449])

In addition, it holds an allocator (alloc), from which the vector can acquire memory for its
elements. The default allocator uses new and delete to acquire and release memory (§12.7). Using
a slightly different implementation technique, we can avoid storing any data for simple
allocators in a vector object.

We initialize a vector with a set of values of its element type:

Click here to view code image

```
vector<Entry> phone_book = {
  "David Hume",123456,
  "Karl Popper",234567,
  "Bertrand Arthur Russell",345678
};
```

Elements can be accessed through subscribing. So, assuming that we have defined << Entry,
 can write:

Click here to view code image

```
void print_book(const vector<Entry>& book)
(
  for (int i = 0; i != book.size(); ++i)
    cout << book[i] << "\n";
);
```

As usual, index starts at 0 so book[0] holds the entry for David Hume. The vector member
function size() gives the number of elements.

The elements of a vector constitute a range, so we can use a range-for loop (§1.7):

Click here to view code image