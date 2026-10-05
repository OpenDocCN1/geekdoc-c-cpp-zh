# 17.3 Impossible Problems

are likewise assigned to bins, strings of length four, and so on. In this way, a string of any given length can be assigned to some bin.

By this process, any string of finite length is assigned to some bin. So any program, which is merely a string of finite length, is assigned to some bin. Because all programs are assigned to some bin, the set of all programs is countable. Naturally most of the strings in the bins are not legal programs, but this is irrelevant. All that matters is that the strings that do correspond to programs are also in the bins.

Now we consider the number of possible functions. To keep things simple, assume that all functions take a single integer as input and yield a single integer as output. We will call such integer functions. A function is simply a mapping from input values to output values. Of course, not all programs literally take inputs and yield integers as output. However, everything that computers read and yield is essentially a series of numbers, which may be interpreted as letters or something else. Any useful computer program's input and output can be coded as integer values, so our simple model of computer input and output is simply general to cover all possible programs.

Now we see if it is possible to assign all of the integers to the infinite set of bins. If so, then the number of integers is countable, and it might be possible to assign every integer to a program. If the set of integer functions cannot be assigned to bins, then there will be integers that must have no corresponding program.

Imagine each integer function as a table with two columns and an infinite number of rows. The first column lists the positive integers starting at 1. The second column lists the output of the function when given the value in the first column as input. Thus, the table explicitly describes the mapping from input to output for each function. Each we call a function.

Next we try to assign function tables to bins. To do so we must order the functions, but it does not matter what we choose. For example, Bin 1 could store the function that always returns 1 regardless of the value of input. Bin 2 could store the function that returns its input. Bin 3 could store the function that doubles its input and adds 5. Bin 4 could store a function for which we can see no simple relationship between input and output. These four functions as assigned to the first four bins are in Figure 17.

Can we assign every to a bin? The answer is no, because there is always a way to create a new function that is not in any of the bins. Suppose somebody finds a way of assigning functions to bins that they claim includes all of the functions. We can build a new function that has not been assigned

> There is no requirement for a function to have any discernible relationship between input and output. A function is simply a mapping of inputs to outputs, with no constraint on how the mapping is determined.