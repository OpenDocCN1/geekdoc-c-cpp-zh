# LIFO, FIFO, LINKS & KEYS

Both the Array and the ArrayList contain elements that can be accessed in any order. You can sort them, of course, or add the elements in a particular order, but by default the elements are stored randomly. The .NET Framework also supports classes that allow their elements to be accessed in particular ways.

Push() puts new item on the top of the stack.

Pop() takes the top item off the top of the stack.

![](bbox=[0.2, 0.3, 0.38, 0.55])

You can only access the top element on the stack.

You've already met the stack. It stores its elements in LIFO order, which is pronounced "Life-oh", and stands for Last In, First Out.

![](bbox=[0.65, 0.23, 0.88, 0.51])

The Hashtable and Dictionary store items in key/value pairs. The keys of a Dictionary must be unique. Hash codes don't have to be, but it's best if they are.

![](bbox=[0.1, 0.58, 0.52, 0.7])

In a linked list, each item knows about the item in front of and behind it. We'll talk about the LinkedList<T> class in the next section.

Enqueue() adds an item to the end of the line.

![](bbox=[0.65, 0.65, 0.8, 0.88])

Dequeue() takes an element from the head of the line.

The Queue stores its elements in FIFO order, which is pronounced "Fife-oh", and stands for First In, First Out.