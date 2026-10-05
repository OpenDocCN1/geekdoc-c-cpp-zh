# PITFALL: Compiler Problems

Some compilers have problems with iterator declarations. You can declare an iterator in different ways. For example, we have been using the following:

```
using std::vector;
..
vector<char>::iterator p;
```

Alternatively, you could use the following:

```
using std::vector<char>::iterator;
iterator p;
```

You could also use the following, which is not as quite nice:

```
using namespace std;
..
vector<char>::iterator p;
```

There are other, similar variations. Your compiler should accept any of these alternatives. However, we have found that some compilers will accept only certain of these alternatives. If one form does not work with your compiler, another.

> Iterator
Iterator is an object that can be used with a container to gain access to elements in the container. An iterator is a generalization of the notion of the pointer. The operators ==, !=, ++ and -- behave the same as the iterators as they do for pointers. The basic outline of how an iterator cycle through all the elements in a container is as follows:

STL_container<datatype>::iterator p;
for (p = container.begin(); p != container.end(); p++)
Process_Element_At_Location p;

STL_container is the name of the container (e.g., vector) and is the data type of elements to be stored in the container. The member function begin( ) returns an iterator located at the first element. The member function end( ) returns a value that serves as a sentinel value one location past the last element in the container.

> Dereferencing
The dereferencing operator, *p, when applied to an iterator p, produces the element located at the iterator p. In some situations *p produces read-only access, which does not allow you to change the element. In other situations it gives you access to the element and will let you change the element.