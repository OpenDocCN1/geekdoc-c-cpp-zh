# Output and Formatting Output

Other than writing efficient programs, generating the desired output is one of a programmer’s highest priorities. Chapter 2 briefly introduced the process involved in generating output on the standard output device. More precisely, you learned how to use the insertion operator `<<` and the manipulator `endl` to display results on the standard output device.

However, there is a lot more to output than just displaying results. Sometimes, floating-point numbers must be output in a specific way. For example, a paycheck must be printed to two decimal places, whereas the results of a scientific experiment might require the output of floating-point numbers to six, seven, or perhaps even ten decimal places. Also, you might like to align the numbers in specific columns or fill the empty space between strings and numbers with a character other than the blank. For example, in preparing the table of contents, the space between the section heading and the page number might need to be filled with dots or dashes. In this section, you will learn about various output functions and manipulators that allow you to format your output in a desired way.

Recall that the syntax of `cout` when used together with the insertion operator `<<` is:

```
cout << expression or manipulator << expression or manipulator...;
```

Here, expression is evaluated, its value is printed, and manipulator is used to format the output. The simplest manipulator that you have used so far is endl, which is used to move the insertion point to the beginning of the next line.

Other output manipulators that are of interest include setprecision, fixed, showpoint, and setw. The next few sections describe these manipulators.

# setprecision Manipulator

You use the manipulator setprecision to control the output of floating-point numbers. Usually, the default output of floating-point numbers is scientific notation. Some integrated development environments (IDEs) might use a maximum of six decimal places for the default output of floating-point numbers. However, when an employee’s paycheck is printed, the desired output is a maximum of two decimal places. To print floating-point output to two decimal places, you use the setprecision manipulator to set the precision to 2.

The general syntax of the setprecision manipulator is:

```
setprecision(n)
```

where n is the number of decimal places.