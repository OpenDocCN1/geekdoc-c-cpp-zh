# Display 19.9 The queue Template Class (part 2 of 2)

# Sample Member Functions

| MEMBER FUNCTION (q IS A QUEUE OBJECT) | MEANING |
|---|---|
| q.size() | Returns the number of elements in the queue. |
| q.empty() | Returns true if the queue is empty; otherwise, returns false. |
| q.front() | Returns a mutable reference to the front member of the queue. |
| q.back() | Returns a mutable reference to the last member of the queue. |
| q.push(Element) | Adds Element to the back of the queue. |
| q.pop() | Removes the front element of the queue. Note that pop is a void function. It does not return the element removed. |
| q1 == q2 | True if q1.size() == q2.size() and each element of q1 is equal to the corresponding element of q2; otherwise, returns false. |

The queue template class also has a default constructor, a copy constructor, and a constructor that takes an object of any sequence class and initializes the stack to the elements in the sequence. It also has a destructor that returns all storage for recycling, and a well-behaved assignment operator.

# Display 19.10 Program Using the stack Template Class (part 1 of 2)

```
1 //Program to demonstrate use of the stack template class from the STL.
2 #include <iostream>
3 #include <stack>
4 using std::cin;
5 using std::cout;
6 using std::endl;
7 using std::stack;
8 
9 int main( )
10 {
11     stack<char> s;
12     cout << "Enter a line of text:\n";
13     char next;
14     cin.get(next);
```