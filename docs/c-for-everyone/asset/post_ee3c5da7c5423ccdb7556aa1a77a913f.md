
![](img/5e58fb4c840712efd6ed6fa82bb97f57_587_0.png)

**Figure 14** Stack and Queue Behavior

Figure 14 contrasts the behaviors of the stack and queue data types.

There are many uses of stacks and queues in computer science. For example, consider an algorithm that attempts to find a path through a maze. When the algorithm encounters an intersection, it pushes the location on the stack, and then it explores the first branch. If that branch is a dead end, it returns to the location at the top of the stack and explores the next untried branch. If all branches are dead ends, it pops the location off the stack, revealing a previously encountered intersection. Another important example is the run-time stack that a processor keeps to organize the variables of nested functions. Whenever a new function is called, its parameters and local variables are pushed onto a stack. When the method exits, they are popped off again. This stack makes recursive function calls possible.

As an example for the use of a queue, consider a printer that receives requests to print documents from multiple applications. If each of the applications sends printing data to the printer at the same time, then the printouts will be garbled. Instead, each application places all data to be sent to the printer into a file and inserts that file into the print queue. When the printer is done printing one file, it retrieves the next one from the queue. Therefore, print jobs are printed using the first in, first out rule, which is a fair arrangement for users of the shared printer.

The following sample program demonstrates the first-in, first-out order of a queue and the last-in, last-out order of a stack.

**ch13/fifolifo.cpp**

```cpp
#include <iostream>
#include <string>
#include <queue>
#include <stack>

using namespace std;

int main()
{
    cout << "FIFO order:" << endl;

    queue<string> q;
    q.push("Tom");
    q.push("Diana");
    q.push("Harry");

    stack<string> s;
    while (q.size() > 0)
    {
        string name = q.front();
        q.pop();
        cout << name << endl;
        s.push(name);
    }

    cout << "LIFO order:" << endl;

    while (s.size() > 0)
    {
        cout << s.top() << endl;
        s.pop();
    }

    return 0;
}
```

### Program Run

```
FIFO order:
Tom
Diana
Harry
LIFO order:
Harry
Diana
Tom
```

![](img/5e58fb4c840712efd6ed6fa82bb97f57_588_0.png)

## SELF CHECK

- **15.** Why wouldn’t you want to use a stack to manage print jobs?
- **16.** What does this code print?

  ```cpp
  queue<int> q;
  for (int i = 1; i <= 10; i++) { q.push(i); }
  for (int i = 1; i <= 5; i++) { q.pop(); }
  cout << q.front() << endl;
  ```

- **17.** What does this code print?

  ```cpp
  stack<int> s;
  for (int i = 1; i <= 10; i++) { s.push(i); }
  for (int i = 1; i <= 5; i++) { s.pop(); }
  cout << s.top() << endl;
  ```

- **18.** Describe how a stack can be used to check whether the parentheses in an arithmetic expression are balanced correctly. For example, `3 + (4 / (5 − 6))` is correct, but `3 + (4 / 5)) − (6` is not.
- **19.** Why would it not be a good idea to use a vector for a queue?

**Practice It** Now you can try these exercises at the end of the chapter: R13.16, R13.18, P13.18.

### Random Fact 13.1 Reverse Polish Notation

![](img/5e58fb4c840712efd6ed6fa82bb97f57_589_0.png)

When you write arithmetic expressions, you are used to operators with different levels of precedence that appear between the operands, except when parentheses are used to specify a different ordering. That is, an expression such as `3 + (4 − 2) × 7` is evaluated by first subtracting the 2 from the 4, then multiplying the result by 7, and finally adding the 3. Notice how the sequence of operations jumps around instead of being analyzed in a strict left to right or right to left order.

In the 1920s a Polish mathematician, Jan Łukasiewicz, noticed that if you wrote the operators first, before the operands, the need for both parentheses and precedence was eliminated and expressions could be read easily from left to right. In Łukasiewicz's notation, the expression would be written as `+ 3 × − 4 2 7`. The scheme was termed Polish Notation in Łukasiewicz's honor (although one can argue it should be called Łukasiewicz Notation). Of course, an entrenched notation is not easily displaced, even when it has distinct disadvantages, and Łukasiewicz's discovery did not cause much of a stir for about 50 years.

In the 1950s, Australian computer scientist Charles Hamblin noted that an even better scheme would be to have the operators follow the operands. This was termed Reverse Polish Notation, or RPN. The expression given would be written as `3 4 2 - 7 × +` in RPN. As you have seen, the evaluation of RPN is relatively simple if you have a stack. Each operand is pushed on the stack. Each operator pops the appropriate number of values from the stack, performs the operation, and pushes the result back onto the stack.

In 1972, Hewlett-Packard introduced the HP 35 calculator that used RPN. For example, to compute `3 + 4 × 5`, you enter `3 4 5 × +`. RPN calculators have no keys labeled with parentheses or an equals symbol. There is only a key labeled ENTER to push a number onto a stack. For that reason, Hewlett-Packard's marketing department used to refer to their product as "the calculators that have no equal". Indeed, the Hewlett-Packard calculators were a great advance over competing models that were unable to handle algebraic notation and left users with no other choice but to write intermediate results on paper.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_589_1.png)

Over time, developers of high quality calculators have adapted to the standard algebraic notation rather than forcing users to learn a new notation. However, those users who have made the effort of learning RPN tend to be fanatic proponents, and some Hewlett-Packard calculator models still support it.

**Table 2 Polish Notation Examples**

| Standard Notation | Łukasiewicz Notation | RPN |
|---|---|---|
| 3 + 4 | + 3 4 | 3 4 + |
| 3 + 4 × 5 | + 3 × 4 5 | 3 4 5 × + |
| 3 × (4 + 5) | × 3 + 4 5 | 3 4 5 + × |
| (3 + 4) × 5 | × + 3 4 5 | 3 4 + 5 × |
| 3 + 4 + 5 | + + 3 4 5 | 3 4 5 + + |

## CHAPTER SUMMARY

### Describe the linked list data structure and the use of list iterators.

- A linked list consists of a number of nodes, each of which has a pointer to the neighboring nodes.
- Adding and removing elements in the middle of a linked list is efficient.
- Visiting the elements of a linked list in sequential order is efficient, but random access is not.
- You can inspect and edit a linked list with an iterator. An iterator points to a node in a linked list.

### Explain how linked lists are implemented.

- When implementing a linked list, we need to define list, node, and iterator classes.
- A list object contains pointers to the first and last nodes.
- An iterator contains a pointer to the current node, and to the list that contains it.
- List nodes are allocated on the heap, using the new operator.
- When a list node is erased, it is recycled to the heap with the delete operator.
- Implementing operations that modify a linked list is challenging—you need to make sure that you update all node pointers correctly.

### Know the efficiencies of the fundamental operations on lists, arrays, and vectors.

- Locating the *k*th element is an *O(k)* operation for linked lists.
- Locating an element is an *O(1)* operation for arrays and vectors.
- Adding an element in a linked list is an *O(1)* operation.
- Adding an element in the middle of an array or vector of size *n* is an *O(n)* operation.
- Adding an element to the end of an array is an *O(1)* operation.
- An element can be added to the end of a vector in amortized *O(1)* time.

### Describe the stack and queue data structures.

- A stack is a container of items with “last in, first out” retrieval.
- A queue is a container of items with “first in, first out” retrieval.

## REVIEW EXERCISES

- **R13.1** If a list has *n* elements, how many legal positions are there for inserting a new element? For erasing an element?
- **R13.2** What happens if you keep advancing an iterator past the end of the list? Before the beginning of the list? What happens if you look up the value at an iterator that is past the end? If you erase the past-the-end position? All these are illegal operations, of course. What does the list implementation of your compiler do in these cases?
