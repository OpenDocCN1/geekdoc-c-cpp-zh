so that the condition in only one if statements will evaluate to true, and hence only one consequent statement will be executed. Perhaps the way in which control flows is more obvious in the flowchart of the entire program, shown in Figure 6.2. Note that once we discover a certain condition to be true, e.g. that the income is at most 180000, we know that the other conditions cannot be true. So the natural question arises: why should we even check them?

The more general if statement, discussed in the next section, allows you to prevent such unnecessary checks. But before discussing that, we discuss the notion of blocks.

# 6.2 Blocks

In the if statement discussed above, the consequent was expected to be a single statement. In general, we might want to execute several statements if a certain condition held, not just one. The block construct helps us in this case.

As discussed earlier, a block is simply a collection of statements that are grouped together in braces, { and }. By putting statements into a block, we are making a single compound statement out of them. A block can be placed wherever a single C++ statement is required, e.g. as the consequent part of the if statement. Suppose for example, we want to print a message "This person is in the highest tax bracket." if the income is more than 8 lakhs, as well as calculate the tax, we would replace the fourth if statement in the program with the following.

```
if (income > 800000){
    tax = 92000+(income - 800000)* 0.3;
    cout << "This person is in the highest tax bracket." << endl;
}
```

You have already used a block as a part of the repeat statement. Let us now note that the general form of the repeat statement is:

```
repeat (count) action
```

where action is any statement including a block. Thus we may write

```
repeat (10) cout << "Test." << endl;
```

which will cause the message "Test." to be printed 10 times.

# 6.3 Other forms of the if statement

The if-else statement has the following form.

```
if (condition) consequent
else alternate
```