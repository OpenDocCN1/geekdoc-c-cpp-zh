
## Display 19.8 The stack Template Class

## stack ADAPTER TEMPLATE CLASS DETAILS

Type name: stack<T> or stack<T, Sequence_Type> for a stack of elements of type T.

Library header: <stack>, which places the definition in the std namespace.

Defined types: value_type, size_type.

There are no iterators.

## SAMPLE MEMBER FUNCTIONS

| MEMBER FUNCTION (s IS A STACK OBJECT) | MEANING |
|---|---|
| s.size() | Returns the number of elements in the stack. |
| s.empty() | Returns true if the stack is empty; otherwise, returns false. |
| s.top() | Returns a mutable reference to the top member of the stack. |
| s.push(Element) | Inserts a copy of Element at the top of the stack. |
| s.pop() | Removes the top element of the stack. Note that pop is a void function. It does not return the element removed. |
| s1 == s2 | True if s1.size() == s2.size() and each element of s1 is equal to the corresponding element of s2; otherwise, returns false. |

The stack template class also has a default constructor, a copy constructor, and a constructor that takes an object of any sequence class and initializes the stack to the elements in the sequence. It also has a destructor that returns all storage for recycling, and a well-behaved assignment operator.

## THE ASSOCIATIVE CONTAINERS set AND map

Associative containers are basically very simple databases. They store data, such as structs or any other type of data. Each data item has an associated value known as its key. For example, if the data is a struct with an employee's record, the key might be the employee's Social Security number. Items are retrieved on the basis of the key. The key type and the type for data to be stored need not have any relationship to one another, although they often are related. A very simple case is when each data item is its own key. For example, in a set every element is its own key.

The set template class is, in some sense, the simplest container you can imagine. It stores elements without repetition. The first insertion places an element in the set. Additional insertions after the first have no effect, so that no element appears more than once. Each element is its own key. Basically, you just add or delete elements and ask if an element is in the set or not. Like all STL classes, the set template class was

## Display 19.9  The queue Template Class

## queue ADAPTER TEMPLATE CLASS DETAILS

*Type name:* `queue<T>` or `queue<Sequence_Type, T>` for a queue of elements of type T.

*For efficiency reasons, the* `Sequence_Type` *cannot be a vector type.*

*Library header:* `<queue>`, which places the definition in the std namespace.

*Defined types:* `value_type`, `size_type`.

There are no iterators.

## SAMPLE MEMBER FUNCTIONS

| MEMBER FUNCTION<br>(q IS A QUEUE OBJECT) | MEANING |
|---|---|
| `q.size()` | Returns the number of elements in the queue. |
| `q.empty()` | Returns true if the queue is empty; otherwise, returns false. |
| `q.front()` | Returns a mutable reference to the front member of the queue. |
| `q.back()` | Returns a mutable reference to the last member of the queue. |
| `q.push(Element)` | Adds Element to the back of the queue. |
| `q.pop()` | Removes the front element of the queue. Note that pop is a void function. It does not return the element removed. |
| `q1 == q2` | True if q1.size() == q2.size() and each element of q1 is equal to the corresponding element of q2; otherwise, returns false. |

The queue template class also has a default constructor, a copy constructor, and a constructor that takes an object of any sequence class and initializes the stack to the elements in the sequence. It also has a destructor that returns all storage for recycling, and a well-behaved assignment operator.

## Display 19.10  Program Using the stack Template Class (part 1 of 2)

```
//Program to demonstrate use of the stack template class from the STL.
#include <iostream>
#include <stack>
using std::cin;
using std::cout;
using std::endl;
using std::stack;

int main()
{
```

## Display 19.10 Program Using the stack Template Class (part 2 of 2)

```
10  stack<char> s;

11  cout << "Enter a line of text:\n";
12  char next;
13  cin.get(next);
14  while (next != '\n')
15  {
16      s.push(next);
17      cin.get(next);
18  }
19  cout << "Written backward that is:\n";
20  while (! s.empty())
21  {
22      cout << s.top();
23      s.pop();
24  }
25  cout << endl;
26  return 0;
27 }
```

The member function pop removes one element, but does not return that element. pop is a void function. Therefore, we needed to use top to read the element we removed.

## Sample Dialogue

```
Enter a line of text:
straw
Written backward that is:
warts
```

written with efficiency as a goal. To work efficiently, a set object stores its values in sorted order. You can specify the order used for storing elements as follows:

```
set<T, Ordering> s;
```

Ordering should be a well-behaved ordering relation that takes two arguments of type T and returns a bool value.² T is the type of elements stored. If no ordering is specified,

> ² The ordering must be a strict weak ordering. Most typical ordering used to implement the < operator is strict weak ordering. For those who want the details: A strict weak ordering must be: (irreflexive) Ordering(x, x) is always false; (antisymmetric) Ordering(x, y) implies !Ordering(y, x); (transitive) Ordering(x, y) and Ordering(y, z) implies Ordering(x, z); and (transitivity of equivalence) if x is equivalent to y and y is equivalent to z, then x is equivalent to z. Two elements x and y are equivalent if Ordering(x, y) and Ordering(y, x) are both false.

## Display 19.12 Program Using the set Template Class

```
//Program to demonstrate use of the set template class.
#include <iostream>
#include <set>
using std::cout;
using std::endl;
using std::set;
using std::set<char>::const_iterator;

int main()
{
    set<char> s;

    s.insert('A');
    s.insert('D');
    s.insert('D');
    s.insert('C');
    s.insert('C');
    s.insert('B');

    cout << "The set contains:\n";
    const_iterator p;
    for (p = s.begin(); p != s.end(); p++)
        cout << *p << " ";
    cout << endl;

    cout << "Removing C.\n";
    s.erase('C');
    for (p = s.begin(); p != s.end(); p++)
        cout << *p << " ";
    cout << endl;

    return 0;
}
```

> No matter how many times you add an element to a set, the set contains only one copy of that element.

## SAMPLE DIALOGUE

The set contains:
A B C D
Removing C.
A B D

you want to assign a unique number to each string name, you could declare a map object as follows:

```
map<string, int> numberMap;
```

For string values known as keys, the numberMap object can associate a unique int value.

Like a set object, a map object stores its elements in sorted order by its key values. You can specify the ordering on keys as a third entry in the angular brackets, < >. If you do not specify an ordering, a default ordering is used. The restrictions on orderings you can use are the same as those on the orderings allowed for the set template class. Note that the ordering is on key values only. The second type can be any type and need not have anything to do with any ordering. As with the set object, the sorting of the stored entries in a map object is done for reasons of efficiency.

Some basic details about the map template class are given in Display 19.13. In order to understand these details, you need to first know something about the pair template class.

The STL template class pair<T1, T2> has objects that are pairs of values such that the first element is of type T1 and the second is of type T2. If aPair is an object of type pair<T1, T2>, then aPair.first is the first element, which is of type T1, and aPair.second is the second element, which is of type T2. The member variables first and second are public member variables, so no accessor or mutator functions are needed.

The header file for the pair template is <utility>. So, to use the pair template class, you need the following, or something like it, in your file:

```
#include<utility>
using std::pair;
```

We will mention two other associative containers, although we will not give any details about them. The template classes multiset and multimap are essentially the same as set and map, respectively, except that multiset allows repetition of elements and multimap allows multiple values to be associated with each key value.

## EFFICIENCY

The STL was designed with efficiency as an important consideration. In fact, the STL implementations strive to be optimally efficient. For example, the set and map elements are stored in sorted order so that algorithms that search for the elements can be more efficient.

Each of the member functions for each of the template classes has a guaranteed maximum running time. These maximum running times are expressed using what is called big-O notation, which we discuss in Section 19.3. (Section 19.3 also gives some guaranteed running times for some of the container member functions we have already discussed. These are given in the subsection entitled "Container Access Running Times.") When using more advanced references or even later in this chapter, you will be told the guaranteed maximum running times for certain functions.
