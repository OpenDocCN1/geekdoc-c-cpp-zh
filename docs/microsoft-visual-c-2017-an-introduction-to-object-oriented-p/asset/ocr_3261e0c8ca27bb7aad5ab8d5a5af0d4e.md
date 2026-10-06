# CHAPTER 6 Using Arrays

Storing values in variables provides flexibility; a program that uses variables to replace constants can manipulate different values each time it executes. When you add loops to your programs, the same variable can hold different values during successive cycles through the loop within the program execution. Learning to use the data structure as an array offers further flexibility. Arrays allow you to store multiple values in adjacent memory locations and access them by varying a value that indicates which of the stored values to use. In this chapter, you will learn to create and manage C arrays.

# Declaring an Array and Assigning Values

Sometimes, just one value in memory at a time isn't adequate. For example, a sales manager who supervises 20 employees might want to determine whether each employee produced sales above or below the average amount. When you enter the employee's sales into a program, you can't determine whether it is above or below because you won't know the average until you have entered all 20 values. You might plan to assign 20 values to separate variables, with a unique name, then sum and average them. However, that is awkward and unwieldy: You need 20 prompts, 20 inputs using 20 separate storage locations (in other words, 20 separate names), and 20 additions. This method might work for 20 salespeople, but what if you have 30, 40, or 10,000 salespeople?

You could enter data for 20 salespeople using just one variable in 20 successive iterations through a loop that contains one prompt, one input, and one addition statement. Unfortunately, when you enter the value for the second employee, data replaces the value for the first employee, and the first employee's value is no longer available to compare to the average of all 20 values. With this approach, when the data-entry loop finishes, the only individual value left in memory is the last one.

The best solution to this problem is to create an array. An array is a list of items that all have the same data type and the same name. Each object in an array is an array element. You can distinguish each element from the others in an array with a subscript. A subscript (also called an index) is an integer that indicates the position of a particular element. In C#, a subscript is written between square brackets that follow an array name.

You declare an array variable with a data type, a pair of square brackets, and an identifier. For example, to declare an array of double values to hold sales values for salespeople, you write the following:

```
double[] sales;
```

In some programming languages, such as C++ and Java, you can also declare an array variable by placing the square brackets after the array name, as in double sales[]. This format is illegal in C.