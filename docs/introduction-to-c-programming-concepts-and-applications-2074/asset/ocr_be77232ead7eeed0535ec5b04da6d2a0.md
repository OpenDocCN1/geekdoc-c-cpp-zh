# // QUEUES

An alternative container adaptor gives you a FIFO (first, first out) data structure. This is called a queue, and it's much like the stack, but instead of the last thing being the one you can access, it's the first thing in. Queues used to represent any sort of process where the first thing into the line is the first thing you want out.

You can push the numbers 10, 15, and 20 into the queue (b), just like you pushed into the stack, and you can have a loop that continues as long as the queue isn't empty (12).

Inside the loop, you'll print the element at the front by using the front function and outputting q.front() (13). Then, remove that front element by calling pop (14).

+   It has 4 operations, like the stack did:
* push adds an element to the end of the queue.
* front tells you which element is in the front of the line (analogous to top from the stack commands).
* pop removes the element at the front of the queue.
* empty tells you if the queue is empty or not.

And you see that the elements came off in the same order you put them in.

In addition to the stack, and queue, another container is the deque (short for double-ended queue).

A deque works a lot like a vector. It's just instead of having push_back and pop_back, it has push_front and pop_front, too. It has basically all the operations that a vector has. You can get the size using size or make it empty using clear. You can access elements using square brackets with the element number or using the at command that you can guarantee you're not reading or writing past the end of the allocated memory.

In Program 22_2, notice that you now #include queue at the beginning (4).

In the main body of the code, you declare a queue, where the type that you want the queue to hold is an integer. So, you write queue<int> and then the name of the queue, which in this case is q (8).

But it's less efficient than a vector, and there is rarely an instance where you all the extra functionality that a deque provides.

```
// Program 22_2
// Queue example
#include<iostream>
#include<queue>
using namespace std;
int main() {
    queue<int> q;
    q.push(10);
    q.push(15);
    q.push(20);
    while (!q.empty()) {
        cout << q.front() << endl;
        q.pop();
    }
}
```

![](bbox=[0.806, 0.386, 0.846, 0.416])