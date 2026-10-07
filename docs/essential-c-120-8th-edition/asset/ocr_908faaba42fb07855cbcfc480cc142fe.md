```
// --------+-----
// 7 | 8 | 9
// --------+-----
char[] cells = {
  '1', '2', '3', '4', '5', '6', '7', '8', '9'
};
```

```
Console.Write(
  "The available moves are as follows: ");
```

```
// Write out the initial available moves
foreach(char cell in cells) {
  if(cell != '0' && cell != 'X') {
    Console.Write("$ cell " ");
  }
}
```

# OUTPUT 4.23

The available moves are as follows: 1 2 3 4 5 6 7 8 9

When the execution engine reaches the foreach statement, it assigns to the variable cell the first item in the cells array—in this case, the value '1'. It then executes the code within the block that makes up the foreach loop body. The if statement determines whether the value of cell is '0' or 'X'. If it is neither, the value of cell is written out to the console. The next iteration assigns the next array value to cell, and so on.

Note that the compiler prevents modification of the variable (cell) during the execution of a foreach loop.

# BEGINNER TOPIC

# Where the switch Statement Is More Appropriate

Sometimes you might compare the same value in several continuous if statements, as shown with the input variable in Listing 4.49.