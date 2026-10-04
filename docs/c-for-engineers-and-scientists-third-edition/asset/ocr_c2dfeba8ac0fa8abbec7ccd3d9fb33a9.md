# Repetition Statements

How do you add a single number to a total? A statement such as total = total + num does the job perfectly. It's the accumulation statement introduced in Section 3.1. After each number is entered, the accumulating statement adds the number to the total, as shown in Figure 5.5.

The complete flow of control for adding the numbers is illustrated in Figure 5.6. In reviewing Figure 5.6, observe that a provision has been made for initially setting the total to zero before the while loop is entered. If you cleared the total inside the while loop, it would be set to zero each time the loop was executed, and any value previously would be erased.

![](bbox=[0.101, 0.276, 0.924, 0.737])

**Figure 5.5** Accepting and adding a number to a total

**Figure 5.6** Accumulation flow of control

Program 5.6 incorporates the necessary modifications to Program 5.5 to the numbers entered. As shown, the statement total = total + num; is placed immediately after the cin statement. Putting the accumulating statement at this point in the program ensures that the entered number is “captured” immediately into the total.