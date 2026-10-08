
bers, logical data, etc.), the size of the data (number of digits or characters), the arrangement of the data (lists, tables, records, etc.), and any restrictions on the range of the data values. For example, a set of measurements of the depth of water in a lake might be assumed to contain at least one measurement; positive, real numbers rather than integers; be significant to two decimal places; and have a unit of measurement such as meters. Program documentation should state this and the algorithm should check that the data meets these conditions.

Design step: Describe the input and output formats.

## 1.3.4 Solution Design Methodology

Once the problem has been clearly stated and analyzed, and the details of the data specified, the solution can be developed. This involves the actual design of the input, output, internal data, the development of an algorithm, and the development of test data for the algorithm. For example, the computer must know whether the data values consist of integers or real numbers and whether they are in normal decimal notation or scientific notation. It must know how many data values are expected and how to identify the list of data values. If the algorithm includes a calculation, assumed preconditions and postconditions must be recognized.

At the design stage, the algorithm can be represented by structure charts, pseudocode and flowcharts, or by other logic representation techniques. Consider the simple problem of calculating and printing the average depth of water in a lake with a set of sample depth measurements. The basic steps in the calculation are:

- 1. Input, validate, and add the data values one by one, counting the number of data values
- 2. Divide the sum of the data values by the number of data values
- 3. Print the average depth

The first of these steps includes repeated input, validation, and addition. The program instructions must include information about the variables to be added and incremented in the repetition loop, and how to detect the end of the data. The instruction to calculate the average and print the average follows the repetition loop. Step 1 will only work if there is an internal variable to use to accumulate the sum of the data values, and an internal variable to use as a counter. Both of these must be cleared before any data is processed. The precondition for Step 1 is that total = 0 and count = 0 where total and count are names for the internal variables. The precondition for Step 2 is that count > 0. Therefore there must be at least one positive data value.

The simplest pseudocode description of this algorithm is as follows:

```
initialize total and count
process positive data values in a set of data values
calculate average
print average
```

This could also be drawn as a flowchart as shown in Figure 1.4.

![](img/8356e6c3bfe3b10354682c60b1e74b1d_39_0.png)

Figure 1.4 Flowchart to compute an average

## 1.3 Algorithms and Program Development 21

In the flowchart in Figure 1.4, arrows indicate the flow of control while different shaped boxes are used for different types of operations. Unless there are many data values to be processed the same way, the flow of control is strictly from the top down.

The following is a pseudocode description of this algorithm that assumes there is at least one valid data value.

### Algorithm

Initialize the total and the count to zero (This is necessary to meet the first precondition)

- For each Input data value greater than 0 (precondition: assume total ≥ 0, count ≥ 0) every time a new data value is obtained
  - Add the data value to the total
  - Add 1 to the count
- End for

Divide the total by the count to get the average depth (precondition: assume count > 0)
Print the average depth

Stop

> Programming Hint: Note that totals and count must always be initialized to zero to reflect the possibility that there may not be any data to process.

This can be drawn as a flowchart as shown in Figure 1.5.
The steps in the flowchart can be described in language or in mathematical notation. Note that we have not yet considered how to identify the end of the data or how to control the repetition.

The part of the pseudocode is bracketed by For and Endfor processes the entire set of data values and can be drawn in flowchart form as shown in Figure 1.6.
Note that each data value is processed separately; therefore, there is a loop back to obtain the next data value. This construct enters the top and exits at the bottom; but it exits only when there are no more data values to be processed.

## Introduction to Computers and Programming

![](img/8356e6c3bfe3b10354682c60b1e74b1d_41_0.png)

Figure 1.5 Flowchart to compute average

For each input data value > 0 the part of the pseudocode that is bracketed by If and Endif processes a single data value and can be drawn as shown in Figure 1.7.

Note that a positive value will be added to the total and the count will be incremented. However, nothing will be done if a data value is not positive. Put these...Endfor and If...Endif constructs together with the preceding sequential flowchart and we obtain the flowchart of Figure 1.8.

*Pseudocode* Pseudocode is a semiform description of the steps to be carried out by the computer, including steps that are to be repeated and decisions that are to be made. There is more than one way of writing an algorithm in pseudocode.

## 1.3 Algorithms and Program Development 23

![](img/8356e6c3bfe3b10354682c60b1e74b1d_42_0.png)

Figure 1.6 Flowchart for repetition

![](img/8356e6c3bfe3b10354682c60b1e74b1d_42_1.png)

Figure 1.7 Flowchart for selective processing

## Introduction to Computers and Programming

Another more detailed and mathematical way of describing this `algorithm` pseudocode would be:

```
total ← 0.0
count ← 0
For each input data value found
If data value > 0 (precondition: a data value was found)
    total ← total + data value
    count ← count + 1
Endif
Endfor
```

average ← total / count (precondition: positive data value was found)

print average

Stop

Note that several assumptions have been made: that there is at least one positive measurement, that the measurement is a real number rather than an integer (total is initialized to 0.0 rather than 0), and that measurement doesn't count.

The processing of a data value depends on being positive, which in turn depends on an input being found.

## Convention for Writing Pseudocode

- 1. Summations and counters must be initialized to.
- 2. Assignment of values is shown by an arrow.
- 3. The beginning and the end of any selection is indicated, as well as excluding it.
- 4. The beginning and the end of any repetition is indicated, as well as continuing or stopping.
- 5. Conditional steps and repetition steps are indented.
- 6. Either words or arithmetic operations may be used.

## 1.3 Algorithms and Program Development 25

- 7. The algorithm termination must be clearly indicated.

These conventions are demonstrated in the previous examples of pseudocode.

Flowchart A flowchart uses standard symbols to show different operations and the order of execution of the steps of the algorithm. Lines and arrows are used to show the flow of control. Figure 1.8 shows a flowchart for finding

![](img/8356e6c3bfe3b10354682c60b1e74b1d_44_0.png)

Figure 1.8 Flowchart to compute average

the depth of water in a lake. Flowcharts help the programmer understand the flow of control in complex algorithms.

**Standard Flowchart Symbols** Each flowchart symbol represents part of an algorithm or program. When flowcharts are used in a structured way, symbols are grouped together to form a single-entry, single-exit structure.

**Process box:** This is a rectangle with one control line leading into it and one leading out of it. At the lowest level it represents a single instruction that computes, moves data from one place to another in memory, or carries out some other type of data manipulation. At a higher level it represents a sequence of instructions, which jointly implement a step in the program.

![](img/8356e6c3bfe3b10354682c60b1e74b1d_45_0.png)

**A function box:** A process box that represents a complicated function that will be implemented separately is drawn as follows.![](img/8356e6c3bfe3b10354682c60b1e74b1d_45_1.png)

**Input/output box:** This is a parallelogram symbol with one control line leading into it and one leading out of it. At the lowest level it represents a single input/output instruction. At a higher level it represents a sequence of input/output instructions, which jointly implement an input/output step in the program.

![](img/8356e6c3bfe3b10354682c60b1e74b1d_45_2.png)
