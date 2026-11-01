7. Then, we will write the for loop to do the actual looping. As in the previous code blocks, when we write the keyword (for in this example) and then press the Tab key twice on the keyboard, the structure is automatically formed as follows:

```
for (int i = 0; i < length; i++)
{
}
```

Code 9.5

We will now modify this template according to our aim. The loop variable is defined as i and initialized to 0 in the for loop, which is OK. The default loop condition, i < length, will be modified as i <= finalValueInteger.

+   - By this modification, the looping will continue as long as i is smaller or equal to finalValueInteger.
+   - Equivalently, when this condition is not satisfied, i.e. when the loop variable i is greater than finalValueInteger, the looping will end.

In addition, the loop variable has to be increased by 1 in each loop, which is already there as i++. For each loop state, the current value of the loop variable, i, will be inserted to the ListBox. The for loop will be as follows after these modifications:

```
for (int i = 0; i <= finalValueInteger; i++)
{
    valuesListBox.Items.Add(i);
}
```

Code 9.6

> Note that we didn’t need to convert the integer type variable i to string for adding to the ListBox.

The Click event handler method is also shown below after these code lines are added: