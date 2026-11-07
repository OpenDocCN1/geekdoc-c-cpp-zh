
```cpp
stackType<double> stack(100);
ifstream infile;
ofstream outfile;

infile.open("RpnData.txt");

if (!infile)
{
    cout << "Cannot open the input file. "
         << "Program terminates!" << endl;
    return 1;
}

outfile.open("RpnOutput.txt");

outfile << fixed << showpoint;
outfile << setprecision(2);

infile >> ch;
while (infile)
{
    stack.initializeStack();
    expressionOk = true;
    outfile << ch;

    evaluateExpression(infile, outfile, stack, ch,
                       expressionOk);
    printResult(outfile, stack, expressionOk);
    infile >> ch; //begin processing the next expression
} //end while

infile.close();
outfile.close();

return 0;

} //end main
//Place the definitions of the function evaluateExpression,
//evaluateOp, discardExp, and printResult as described
//previously here.
```

### Sample Run

**Input File**

```text
#35 #27 + #3 * =
#26 #28 + #32 #2 ; - #5 / =
#23 #30 #15 * / =
#2 #3 #4 + =
#20 #29 #9 * ; =
#25 #23 - + =
#34 #24 #12 #7 / * + #23 - =
```

**Output**

```text
#35.00 #27.00 + #3.00 * = 186.00
---
#26.00 #28.00 + #32.00 #2.00 ; (Illegal operator) - #5 / = (Error in the expression)
---
#23.00 #30.00 #15.00 * / = 0.05
---
#2.00 #3.00 #4.00 + = (Error: Too many operands)
---
#20.00 #29.00 #9.00 * ; (Illegal operator) = (Error in the expression)
---
#25.00 #23.00 - + (Not enough operands) = (Error in the expression)
---
#34.00 #24.00 #12.00 #7.00 / * + #23.00 - = 52.14
```

## Removing Recursion: Nonrecursive Algorithm to Print a Linked List Backward

In Chapter 18, we used recursion to print a linked list backward. In this section, you will learn how a stack can be used to design a nonrecursive algorithm to print a linked list backward.

Consider the linked list shown in Figure 19-18.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1201_0.png)

**FIGURE 19-18** Linked list

To print the list backward, first we need to get to the last node of the list, which we can do by traversing the linked list starting at the first node. However, once we are at the last node, how do we get back to the previous node, especially given that links go in only one direction? You can again traverse the linked list with the appropriate loop termination condition, but this approach might waste a considerable amount of computer time, especially if the list is very large. Moreover, if we do this for every node in the list, the program might execute very slowly. Next, we show how to use a stack effectively to print the list backward.

After printing the info of a particular node, we need to move to the node immediately behind this node. For example, after printing 15, we need to move to the node with

After the statement in Line 4 executes, the loop condition in Line 2 is re-evaluated. Because `current` is not NULL, the loop condition evaluates to true, so the statements in Lines 3 and 4 execute. (See Figure 19-21.)

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1203_0.png)

**FIGURE 19-21** List and stack after the statements `stack.push(current);` and `current = current->link;` execute

After the statement in Line 4 executes, the loop condition in Line 2 is evaluated again. Because `current` is not NULL, the loop condition evaluates to true, so the statements in Lines 3 and 4 execute. (See Figure 19-22.)

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1203_1.png)

**FIGURE 19-22** List and stack after the statements `stack.push(current);` and `current = current->link;` execute

After the statement in Line 4 executes, the loop condition in Line 2 is evaluated again. Because `current` is NULL, the loop condition evaluates to false, and the while loop in Line 2 terminates. From Figure 19-22, it follows that a pointer to each node in the linked list is saved in the stack. The top element of the stack contains a pointer to the last node in the list, and so on. Let us now execute the following statements:

```cpp
while (!stack.isEmptyStack())        //Line 5
{
    current = stack.top();            //Line 6
    stack.pop();                      //Line 7
    cout << current->info << " ";     //Line 8
}
```

The loop condition in Line 5 evaluates to true because the stack is nonempty. Therefore, the statements in Lines 6, 7, and 8 execute. After the statement in Line 6 executes, current points to the last node. The statement in Line 7 removes the top element of the stack. (See Figure 19-23.)

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1204_0.png)

The statement in Line 8 outputs `current->info`, which is 15. Next, the loop condition in Line 5 is evaluated. Because the loop condition evaluates to true, the statements in Lines 6, 7, and 8 execute. After the statements in Lines 6 and 7 execute, Figure 19-24 results.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1204_1.png)

The statement in Line 8 outputs `current->info`, which is 10. Next, the loop condition in Line 5 is evaluated. Because the loop condition evaluates to true, the statements in Lines 6, 7, and 8 execute. After the statements in Lines 6 and 7 execute, Figure 19-25 results.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1205_0.png)

**FIGURE 19-25** List and stack after the statements `current = stack.top();` and `stack.pop();` execute

The statement in Line 8 outputs `current->info`, which is 5. Next, the loop condition in Line 5 is evaluated. Because the loop condition evaluates to false, the while loop terminates. The while loop in Line 5 produces the following output:

```text
15 10 5
```

## Queues

This section discusses another important data structure called a **queue**. The notion of a queue in computer science is the same as the notion of the queues to which you are accustomed in everyday life. There are queues of customers in a bank or a grocery store and queues of cars waiting to pass through a tollbooth. Similarly, because a computer can send a print request faster than a printer can print, a queue of documents is often waiting to be printed at a printer. The general rule to process elements in a queue is that the customer at the front of the queue is served next, and when a new customer arrives, he or she stands at the end of the queue. That is, a queue is a First In First Out data structure.

Queues have numerous applications in computer science. Whenever a system is modeled on the First In First Out principle, queues are used. At the end of this section, we will discuss one of the most widely used applications of queues, computer simulation. First, however, we need to develop the tools necessary to implement a queue. The next few sections discuss how to design classes to implement queues as an ADT.

A queue is a set of elements of the same type in which the elements are added at one end, called the **back** or **rear**, and deleted from the other end, called the **front**. For example, consider a line of customers in a bank, wherein the customers are waiting to withdraw/deposit money or to conduct some other business. Each new customer gets in the line at the rear. Whenever a teller is ready for a new customer, the customer at the front of the line is served.

The rear of the queue is accessed whenever a new element is added to the queue, and the front of the queue is accessed whenever an element is deleted from the queue. As in a stack, the middle elements of the queue are inaccessible, even if the queue elements are stored in an array.

**Queue:** A data structure in which the elements are added at one end, called the rear, and deleted from the other end, called the front; a First In First Out (FIFO) data structure.

### Queue Operations

From the definition of queues, we see that the two key operations are add and delete. We call the add operation **addQueue** and the delete operation **deleteQueue**. Because elements can be neither deleted from an empty queue nor added to a full queue, we need two more operations to successfully implement the **addQueue** and **deleteQueue** operations: **isEmptyQueue** (checks whether the queue is empty) and **isFullQueue** (checks whether a queue is full).

We also need an operation, **initializeQueue**, to initialize the queue to an empty state. Moreover, to retrieve the first and last elements of the queue, we include the operations **front** and **back**, as described in the following list. Some of the queue operations are:

- **initializeQueue**: Initializes the queue to an empty state.
- **isEmptyQueue**: Determines whether the queue is empty. If the queue is empty, it returns the value true; otherwise, it returns the value false.
- **isFullQueue**: Determines whether the queue is full. If the queue is full, it returns the value true; otherwise, it returns the value false.
- **front**: Returns the front, that is, the first element of the queue. Input to this operation consists of the queue. Prior to this operation, the queue must exist and must not be empty.
- **back**: Returns the last element of the queue. Input to this operation consists of the queue. Prior to this operation, the queue must exist and must not be empty.
- **addQueue**: Adds a new element to the rear of the queue. Input to this operation consists of the queue and the new element. Prior to this operation, the queue must exist and must not be full.
- **deleteQueue**: Removes the front element from the queue. Input to this operation consists of the queue. Prior to this operation, the queue must exist and must not be empty.

As in the case of a stack, a queue can be stored in an array or in a linked structure. We will consider both implementations. Because elements are added at one end and removed from the other end, we need two pointers to keep track of the front and rear of the queue, called **queueFront** and **queueRear**.
