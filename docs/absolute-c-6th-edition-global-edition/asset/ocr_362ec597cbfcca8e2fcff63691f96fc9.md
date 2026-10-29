The basic use of iterators with vector (or any container class) is illustrated by the following lines from Display 19.1:

```
```cpp
vector<int>::iterator p;
for (p = container.begin(); p != container.end(); p++)
    cout << *p << " ";
```
```

Recall that container is of type vector<int>, and that the type iterator really means std::vector<int>::iterator.

A vector v can be thought of as a linear arrangement of its data elements. There is a first data element v[0], a second data element v[1], and so forth. An iterator p is an object that can be located at one of these elements (or points to one of these elements). An iterator can move its location from one element to another element. If p is located at, say, v[7], then p++ moves p so it is located at v[8]. This allows an iterator to move through the vector from the first element to the last element, but it needs to find the first element and needs to know when it has seen the last element.

You can tell if an iterator is at the same location as another iterator by using the operator, ==. Thus, if you have an iterator pointing to the first, last, or other element, you could test another iterator to see if it is located at the first, last, or other element.

If p1 and p2 are two iterators, then the comparison

```
```text
p1 == p2
```
```

is true when and only when p1 and p2 are located at the same element. (This is analogous to pointers. If p1 and p2 were pointers, this comparison would be true if they pointed to the same thing.) As usual, != is just the negation of ==, and so

```
```text
p1 != p2
```
```

is true when p1 and p2 are not located at the same element.

The member function begin( ) is used to position an iterator at the first element in a container. For vectors, and many other container classes, the member function begin( ) returns an iterator located at the first element. (For a vector v the first element is v[0].) Thus,

```
```cpp
vector<int>::iterator p = v.begin( );
```
```

initializes the iterator variable p to an iterator located at the first element. The basic for loop for visiting all elements of the vector v is therefore

```
```cpp
vector<int>::iterator p;
for (p = v.begin( ); Boolean_Expression; p++)
    Action_At_Location p;
```
```

The desired stopping condition is

```
```text
p = v.end( )
```
```