wants). So when you’re at a party with your friend, you can call him over using either Eugene or Gibby. Your friend is only one person, but you can call him using either his name or a nickname. This is the same way a variable and a reference to that variable work. You can get to a single value stored in a variable by using its variable name or the name of a reference to that variable. Finally, whatever you do, try not to name your variables Eugene—for their sakes.

# Trap

Because a reference must always refer to another value, you must initialize the reference when you declare it. If you don’t, you’ll get a compile error. The following line is quite illegal:

```
int& mikesScore; //don't try this at home!
```

# Accessing Referenced Values

Next I send both myScore and mikesScore to cout.

```
cout << "myScore is: " << myScore << "\n";
cout << "mikesScore is: " << mikesScore << "\n\n";
```

Both lines of code display 1000 because they each access the same single chunk of memory that stores the number 1000. Remember, there is only one value, and it is stored in the variable myScore. mikesScore simply provides another way to get to that value.

# Altering Referenced Values

Next I increase the value of myScore by 500.

```
myScore += 500;
```

When I send myScore to cout, 1500 is displayed, just as you’d expect. When I send mikesScore to cout, 1500 is also displayed. Again, that’s because mikesScore is just another name for the variable myScore. In essence, I’m sending the same variable to cout both times.

Next I increase mikesScore by 500.

```
mikesScore += 500;
```

Because mikesScore is just another name for myScore, the preceding line of code increases the value of myScore by 500. So when I next send myScore to cout, 2000 is displayed. When I send mikesScore to cout, 2000 is displayed again.