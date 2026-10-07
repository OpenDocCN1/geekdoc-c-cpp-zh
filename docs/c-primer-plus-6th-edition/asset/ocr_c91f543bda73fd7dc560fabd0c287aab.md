# Additional Members for Sequence Containers

container precedes the second. If two containers compare equally until one runs out of
elements, the shorter precedes the longer.

# Additional Members for Sequence Containers

The vector, forward_list, list, deque, and array template classes are all sequence
containers, and they all have the methods listed previously, with the exception that
forward_list is not reversible and does not support the methods ofTable G.3. A sequence
container, surprisingly, holds a homogeneous set of items in linear order. The
sequence has a fixed number of elements, array is the usual choice. Otherwise, vector,
which combines the random access of array with the ability to add and delete items
be your first recourse. however, if there are frequent additions in the middle of the
sequence, consider using list or forward_list. And additions and deletions primarily
occur at the two ends of the sequence, consider deque.

The fixed size of array prevents array from using many of the sequence
methods. Table G.5 lists additional methods available for sequence containers than other
array. (forward_list has somewhat different definitions for resize()). Again, X is a
type, such as vector<int>, and T is the stored in the container, such as
int is a value of type X. is an equal or const value of type X::value_type. rv is a
on-const value of that type. i and j are input iterators. [i,j) is a valid range. is a
valid transferable const iterator to a. [q1,q2) is a valid range of const iterators. n is
an integer of X::size_type. Args is a template parameter, and is a function
parameter with the pattern Args&&.

| Table G.5 Additional Operations Defined for Sequence Containers |
| Operation | Description |
| X(n, t) | Constructs a sequence container with n copies of t. |
| X a(n, t) | Constructs a sequence container with n copies of t. |
| X(i, j) | Constructs a sequence container equal to the range [i,j]. |
| X a(i, j) | Constructs a sequence container equal to the range [i,j]. |
| X(il) | Constructs a sequence container initialized to the contents of il. |
| a = il; | Copies the values in il to a. |
| a.emplace(p, args); | Inserts an object of type t before p using the T constructor with
t arguments passed into args. |
| a.insert(p,t) | Inserts a copy of t before p; returns an iterator pointing to the\inserted copy of t. The default value for t is T()—that is, the
used for type T in the absence of explicit initialization. |
| a.insert(p,rv) | Inserts a copy of rv before p; returns an iterator pointing to the
inserted copy of t; move semantics may be used. |