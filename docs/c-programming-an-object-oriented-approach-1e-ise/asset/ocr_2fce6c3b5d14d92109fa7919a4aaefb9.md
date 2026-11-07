![](bbox=[0.335, 0.089, 0.755, 0.272])

![](bbox=[0.335, 0.321, 0.755, 0.47])

nation of data. The cin object uses an input device (such as the keyboard) as the source of data. The cout object uses an output device (such as the monitor) as the destination of data. The cin object uses the operators (>>) to get the data; the cout object uses the operator (<<) to deliver the data. We can better understand the role of these objects if we see them together with their memory as shown in Figure 2.9.

To remember which operators we need to use, we can think of (>>) and (<<) as double arrows in the direction of data movement. In the case of input, data moves to the right; in the case of output, data moves to the left.

The most important point that we need to remember about the cin object is that we need a variable name (as the destination of data). On the other hand, we need a value as the source of data for the cout object. However, we have seen that we use a command such as cout << sum, where the sum is the name of a variable. We should be aware that in this case, we mean the value of sum, not the name of sum. This is an important issue that we need to remember. The name of the variable sometimes means the physical variable as the destination; sometimes, it means a copy of the value stored in it.

The value used with the cout object does not necessarily have to be the value of a variable; it can be an independent value such as (cout << 12), which means send the value 12 to the monitor.

> > **The cin object needs to see a variable name;**  
> > **the cout object needs to see a value.**

The following examples clarify these important concepts.