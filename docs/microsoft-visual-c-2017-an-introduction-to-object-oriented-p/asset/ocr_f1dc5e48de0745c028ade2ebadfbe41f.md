You learned about Boolean expressions and the bool data type in Chapter 2. Table 2-4 summarizes comparison operators are used.

In the chapter "Introduction to Methods," you will learn to write methods that return values. A method that returns a Boolean value can also be used as the tested expression in an if statement.

In some programming languages, such as C++, nonzero numbers evaluate as true and O evaluates false. However, in C#, only Boolean expressions evaluate as true and false.

For example, the code segment diagrammed in Figure 4-3 displays A and B when number holds a value less than 5, but when number is 5 or greater, only B is displayed. The tested Boolean expression number < 5 is false, the statement that displays A never executes.

![](bbox=[0.134, 0.516, 0.725, 0.813])

Figure 4-3 Flowchart and code including a typical if statement followed by a separate statement

Although you can create a meaningful flowchart using only rectangles, diamonds, and flowlines, parallelograms have traditionally been used to represent input and output statements, so they are used in Figure 4-3 and in other figures in this chapter.