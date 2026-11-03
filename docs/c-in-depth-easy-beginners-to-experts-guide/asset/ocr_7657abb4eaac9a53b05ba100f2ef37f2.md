And hence the order of the messages,also became unpredictable.as the result,the order of calling the functions in the program (that react to different messages) is dicatated by the order of occurrence of events. Hence this programming model is called “Event Driven Programming Model”.

There can be hundreds of the ways in which the user may interact with an application. In addition to this , some events may occur without any user user interaction. For example, events occur when we create a window, when the window contant are to be drawn,etc.

Thus ,literally hundereds of the messages may be sent to an application thereby creating a chaos. Naturally a question comes- in which order would thease messages get processed by the application. Order is brought to this chaos by putting all the messages that reach the application into a “Queue”. The messages in the queue are processed in first in first out (FIFO) Algorithm order.

In fact the o.s maintains several such queues. There is one queue, which is common for all application. This queue is known as “system Message Queue”. In addition, there is one queue per application. Such queues are called “Application Message Queue”. Let understand the need for maintaining so many queues. When we click a mouse and an event occurs the device driver posts a message into the system message queue. The OS retrives this message finds out with regard to which application the message has been sent. Next it posts a message into the Application Message Queue of the application in which the mouse was clicked.

Thus really all that is there to event-driven programming. Your job is to anticipate what user are likely to do with ur Application’s user interface objects and have a function waiting,Ready to execute at the appropriate time.just when that time is, no one except the user really wanna to say.

You need to understand this first that the difference of simple software programming and window o.s development programming, the window programming model is in the “MACRO” level, let us dig futher and see some obvious issues that will need while u developing programming for the window o.s enviornment.

# There are following issues:-

+   (A) SIZE OF POINTERS.
+   (B) SIZE OF INTEGERS.