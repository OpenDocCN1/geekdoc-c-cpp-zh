# **Program 18.8** Reversing a string using a stack (Continued)

```
```cpp
int main ( )
{
    // Instantiation of a stack object and two string objects
    Stack <char> stack;
    string origin;
    string reversed;
    // Input a string
    cout << "Enter a string to be reversed: ";
    getline (cin, origin);
    // Pushing the copy of characters in the origin string into the stack
    for (int i = 0; i < origin.size(); i++)
    {
        stack.push (origin [i]);
    }
    // Poping the stack and adding characters to the reversed string
    while (stack.size () > 0)
    {
        reversed.push_back (stack.top());
        stack.pop ();
    }
    // Printing both string for comparison
    cout << "Original string: " << origin << endl;
    cout << "Reversed string: " << reversed;
    return 0;
}
```
```

**Run:**

Enter a string to be reversed: **Hello my friends.**

Original string: Hello my friends.

Reversed string: .sdneirf ym olleH

**Run:**

Enter a string to be reversed: **rotor**

Original string: rotor

Reversed string: rotor

# 18.3.2 Queues

A **queue** is a linear list in which data can only be inserted at one end, called *back*, and deleted from the other end, called *front*. These restrictions ensure that the data are output through the queue in the order in which they are input. In other words, a queue is a *first-in-first-out (FIFO)* structure.

A queue is the same as a line. A line of people waiting for the bus in a bus station is a *queue*; a list of calls put on hold to be answered by a telephone operator is a queue; and a list of jobs waiting to be processed by a computer is a queue.

Figure 18.14 shows two representations of a queue: one a queue of people and the other a queue of data items. Both people and data enter the queue at the back and progress through the queue until they arrive at the front. Once they are at the front of the queue, they can leave the queue.