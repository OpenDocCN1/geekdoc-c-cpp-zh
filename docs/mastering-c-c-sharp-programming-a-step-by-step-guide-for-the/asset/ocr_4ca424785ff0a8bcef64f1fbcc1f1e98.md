```
do
{
Console.Write("Enter a number between 0 and 10: ");
string playerResponse = Console.ReadLine();
playersNumber = Convert.ToInt32(playerResponse);
}
while (playersNumber < 0 || playersNumber > 10);
```

A do-while loop is formed by adding the do keyword at the beginning of the loop with the while keyword at the end. Note that a semicolon is required at the end of the line with the while keyword. Everything else remains exactly the same but the playerNumbers variable does not need to be initialized.

# The For Loop

The for loop is a little bit different and very common in computer programming because it is an easy way of adding a counting loop type; we will see more of them in the next section on arrays but we’ll have a basic look now.

They are a bit more complex to set up because three components are needed in the parentheses; the previous loops only needed one. A for loop looks like this:

```
for(initial condition; condition to check; action at end of loop)
{
//...
}
```

The three parts to the loop statement are separated by semicolons. The first bit sets the initial state while the second bit is the actual condition – this is what was in the other two loops. The third is the