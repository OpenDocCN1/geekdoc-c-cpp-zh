# 1.3 Algorithms and Program Development 21

In the flowchart in Figure 1.4, arrows indicate the flow of control while different shaped boxes are used for different types of operations. Unless there are many data values to be processed the same way, the flow of control is strictly from the top down.

The following is a pseudocode description of this algorithm that assumes there is at least one valid data value.

# Algorithm

Initialize the total and the count to zero (This is necessary to meet the first precondition)

+   For each Input data value greater than O (precondition: assume total ≥ 0, count ≥ 0) every time a new data value is obtained
Add the data value to the total
Add 1 to the count
End for

Divide the total by the count to get the average depth (precondition: assume count > 0)
Print the average depth

Stop

> Programming Hint: Note that totals and count must always be initialized zero to reflect the possibility that there may not be any data to process.

This can be drawn as a flowchart as shown in Figure 1.5.
The steps in the flowchart can be described in language or in mathematical notation. Note that we have not yet considered how to identify the end of the data or how to control the repetition.

The part of the pseudocode is bracketed by For and Endfor processes the entire set of data values and can be drawn in flowchart form as shown in Figure 1.6.
Note that each data value is processed separately; therefore, there is a loop back to obtain the next data value. This construct enters the top and exits at the bottom; but it exits only when there are no more data values to be processed.