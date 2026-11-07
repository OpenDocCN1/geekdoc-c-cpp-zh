The statement in Line 8 outputs `current->info`, which is 10. Next, the loop condition in Line 5 is evaluated. Because the loop condition evaluates to **true**, the statements in Lines 6, 7, and 8 execute. After the statements in Lines 6 and 7 execute, Figure 17–25 results.

![](bbox=[0.199, 0.198, 0.897, 0.307])

**FIGURE 17–25** List and stack after the statements `current = stack.top();` and `stack.pop();` execute

The statement in Line 8 outputs `current->info`, which is 5. Next, the loop condition in Line 5 is evaluated. Because the loop condition evaluates to **false**, the while loop terminates. The while loop in Line 5 produces the following output:

15 10 5

# Queues

This section discusses another important data structure called a **queue**. The notion of a queue in computer science is the same as the notion of the queues to which you are accustomed in everyday life. There are queues of customers in a bank or in a grocery store and queues of cars waiting to pass through a tollbooth. Similarly, because a computer can send a print request faster than a printer can print, a queue of documents is often waiting to be printed at a printer. The general rule to process elements in a queue is that the customer at the front of the queue is served next, and when a new customer arrives, he or she stands at the end of the queue. That is, a queue is a First In First Out data structure.

Queues have numerous applications in computer science. Whenever a system is modeled on the First In First Out principle, queues are used. At the end of this section, we will discuss one of the most widely used applications of queues, computer simulation. First, however, we need to develop the tools necessary to implement a queue. The next few sections discuss how to design classes to implement queues as an ADT.

A queue is a set of elements of the same type in which the elements are added at one end, called the **back** or **rear**, and deleted from the other end, called the **front**. For example, consider a line of customers in a bank, wherein the customers are waiting to withdraw/deposit money or to conduct some other business. Each new customer gets in the line at the rear. Whenever a teller is ready for a new customer, the customer at the front of the line is served.

The rear of the queue is accessed whenever a new element is added to the queue, and the front of the queue is accessed whenever an element is deleted from the queue. As in a