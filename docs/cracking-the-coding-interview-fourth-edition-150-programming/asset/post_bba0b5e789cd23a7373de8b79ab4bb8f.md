
# Interview Questions

## Part 1
Data Structures

## Chapter 1 | Arrays and Strings

### Hash Tables

While not all problems can be solved with hash tables, a shocking number of interview problems can be. Before your interview, make sure to practice both using and implementing hash tables.

```java
public HashMap<Integer, Student> buildMap(Student[] students) {
    HashMap<Integer, Student> map = new HashMap<Integer, Student>();
    for (Student s : students) map.put(s.getId(), s);
    return map;
}
```

### ArrayList (Dynamically Resizing Array):

An ArrayList, a dynamically resizing array, is an array that resizes itself as needed while providing O(1) access. A typical implementation is that when a vector is full, the array doubles in size. Each doubling takes O(n) time, but happens rarely that its amortized time is still O(1).

```java
public ArrayList<String> merge(String[] words, String[] more) {
    ArrayList<String> sentence = new ArrayList<String>();
    for (String w : words) sentence.add(w);
    for (String w : more) sentence.add(w);
    return sentence;
}
```

### StringBuffer / StringBuilder

```java
public String setName(String[] words) {
    String sentence = "";
    for (String w : words) sentence = sentence + w;
    return sentence;
}
```

**Answer:** O(n^2), where n is the number of letters in sentence. Here's why: each time you append a string to sentence, you create a copy of sentence and run through all the letters in sentence to copy them over. If you have to iterate up to n characters each time in the loop, and you are looping up to n times, that gives you an O(n^2) run time. Auch!

StringBuffer (or StringBuilder) can help you avoid this problem.

```java
public String setName(String[] words) {
    StringBuilder sentence = new StringBuilder();
    for (String w : words) sentence.append(w);
    return sentence.toString();
}
```

## Chapter 1 | Arrays and Strings

1.1 Implement an algorithm to determine if a string has all unique characters. What if you cannot use additional data structures?

1.2 Write code to reverse a C-Style String. (C-String means that "abcd" is represented as five characters, including the null character.)

1.3 Design an algorithm and write code to remove the duplicate characters in a string without using any additional buffer. NOTE: One or two additional variables are fine. An extra copy of the array is not.

FOLLOW UP Write the test cases for this method.

1.4 Write a method to decide if two strings are anagrams or not.

1.5 Write a method to replace all spaces in a string with %20:

1.6 Given an image represented by an NxN matrix, where each pixel in the image is 4 bytes, write a method to rotate the image by 90 degrees. Can you do this in place?

1.7 Write an algorithm such that if an element in an MxN matrix is 0, its entire row and column is set to 0.

1.8 Assume you have a method isSubstring which checks if one word is a substring of another. Given two strings, s1 and s2, write code to check if s2 is a rotation of s1 using only one call to isSubstring (i.e., "waterbottle" is a rotation of "erbottewat").

## Chapter 2 | Linked Lists

### How to Approach:

Linked lists are extremely common. These can range from simple (delete a node in a linked list) to much more challenging. Either way, we advise you to be extremely comfortable with the easiest questions. Being able to easily manipulate a linked list in the simplest ways will make the tougher list questions much less tricky. With that said, we present some "must know" code about linked list manipulation. You should be able to easily write this code yourself prior to your interview.

### Creating a Linked List:

NOTE: When you're discussing a linked list in an interview, make sure to understand whether it is a single linked list or a doubly linked list.

```java
class Node {
    Node next = null;
    int data;
    public Node(int d) { data = d; }
    void addNodeToTail(int d) {
        Node end = new Node(d);
        Node n = this;
        while (n.next != null) { n = n.next; }
        n.next = end;
    }
}
```

### Deleting a Node from a Singly Linked List

```java
Node delete(Node head, int d) {
    Node n = head;
    if (n.data == d) {
        return head.next; /* moved head */
    }
    while (n.next != null) {
        if (n.next.data == d) {
            n.next = n.next.next;
            return head; /* head didn't change */
        }
        n = n.next;
    }
}
```

![](img/50974dc108b2978cf2cacf9397df9934_55_0.png)

## Chapter 2 | Linked Lists

2.1 Write code to remove duplicates from an unsorted linked list.
FOLLOW UP
How would you solve this if temporary buffer is not allowed?

2.2 Implement an algorithm to find the nth element of a linked list.

2.3 Implement an algorithm to delete a node in the middle of a linked list, given only access to that node.
EXAMPLE
Input: a->b->c->d->e
Result: a->b->e

2.4 You have two numbers represented by a linked list, where each node contains a digit. Write an algorithm that sums the two.
EXAMPLE
Input: (3 -> 5) + (5 -> 2)
Output: 8 -> 7

2.5 Given a circular list, implement an algorithm which returns the beginning of the loop.
DEFINITION
Circular list: A linked list in which next pointer points to an earlier node.
EXAMPLE
input: A->B->C->D->E
output: C

## Chapter 3 | Stacks and Queues

### How to Approach:

Whether you are asked to implement a simple stack / queue, or you are asked to implement a modified version, you will have big up if you can flawlessly work with stacks and queues. Practice makes perfect! Here is some skeleton code for a Stack.

# Implementing a Stack

```java
class Stack {
2 top;
    Node pop() {
        if (top != null) {
            Object item = top.data;
            top = top.next;
            return item;
        }
        return null;
    }
    void push(Object item) {
        Node t = new Node(item);
        t.next = top;
        top = t;
    }
}
```

# Implementing a Queue

```java
class Queue {
2 first, last;
    void enqueue(Object item) {
        if (!first) {
            last = new Node(item);
            first = last;
        } else {
            last.next = new Node(item);
            last = last.next;
        }
    }
    Node dequeue() {
        if (first != null) {
            Object item = first.data;
            first = first.next;
            return item;
        }
        return null;
    }
}
```

## Chapter 3 | Stacks and Queues

3.1 Describe how you could use a single array to implement three stacks.

3.2 How would you design a stack which, in addition to push and pop, also has a function which returns the minimum element? Push, pop and min all operate in O(1).

3.3 Imagine a (literal) stack of plates. If the stack gets too high, it might topple. Therefore, in real life, we would likely start a new stack when the previous one exceeds some threshold. Implement a data structure SetOfStacks that mimics this. SetOfStacks composed of several stacks, should create a new stack after the previous one exceeds capacity. SetOfStacks.push() and SetOfStacks.pop() should behave identically to a single stack (that is, pop()) should return the same values as if there were just a single stack.

FOLLOW UP

Implement a function popAt(int index) which performs a pop operation on a specific sub-stack.

3.4 In the classic problem of the Towers of Hanoi, you have 3 rods and N disks of different sizes which can slide onto any tower. The puzzle starts with disks sorted in ascending order of size from top to bottom (e.g., each disk sits on top of an even larger one). You have the following constraints:

- (A) Only one disk can be moved at a time.
- (B) A disk is slid off the top of one rod onto the next rod.
- (C) A disk can only be placed on top of a larger disk.

Write a program to move the disks from the first rod to the last using Stacks.

3.5 Implement a MyQueue class which implements a queue using two stacks.

3.6 Write a program to sort a stack in ascending order. You should not make any assumptions about how the stack is implemented. The following are the only functions that should be used to write this program: push | pop | peek | isEmpty.
