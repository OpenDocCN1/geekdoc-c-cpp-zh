**Sample Run:** In this sample run, the user input is shaded.

Line 1: Enter the number of positive integers to be added: `100`

Line 7: The sum of the first 100 positive integers is 5050

The statement in Line 1 prompts the user to enter the number of positive integers to be added. The statement in Line 2 stores the number entered by the user in `n`, and the statement in Line 3 initializes `sum` to 0. The `for` loop in Line 5 executes `n` times. In the `for` loop, `counter` is initialized to 1 and is incremented by 1 after each iteration of the loop. Therefore, `counter` ranges from 1 to `n`. Each time through the loop, the value of `counter` is added to `sum`. The variable `sum` was initialized to 0, `counter` ranges from 1 to `n`, and the current value of `counter` is added to the value of `sum`. Therefore, after the `for` loop executes, `sum` contains the sum of the first `n` values, which in the sample run is 100 positive integers.

Recall that putting one control structure statement inside another is called **nesting**. The following programming example demonstrates a simple instance of nesting. It also nicely demonstrates counting.

# **PROGRAMMING EXAMPLE:** Classifying Numbers

This program reads a given set of integers and then prints the number of odd and even integers. It also outputs the number of zeros.

The program reads 20 integers, but you can easily modify it to read any set of numbers. In fact, you can modify the program so that it first prompts the user to specify how many integers are to be read.

+   - **Input:** 20 integers—positive, negative, or zeros.
+   - **Output:** The number of zeros, even numbers, and odd numbers.

# **PROBLEM ANALYSIS AND ALGORITHM DESIGN**

After reading a number, you need to check whether it is even or odd. Suppose the value is stored in `number`. Divide `number` by 2 and check the remainder. If the remainder is 0, `number` is even. Increment the even count and then check whether `number` is 0. If it is, increment the zero count. If the remainder is not 0, increment the odd count.

The program uses a `switch` statement to decide whether `number` is odd or even. Suppose that `number` is odd. Dividing by 2 gives the remainder 1 if `number` is positive and the remainder -1 if it is negative. If `number` is even, dividing by 2 gives the remainder 0 whether `number` is positive or negative. You can use the mod operator, `%`, to find the remainder. For example:

```
```
6 % 2 = 0; -4 % 2 = 0; -7 % 2 = -1; 15 % 2 = 1
```
```