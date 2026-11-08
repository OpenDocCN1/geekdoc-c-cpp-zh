In the most common form of the indefinite for loop, all the control expressions are omitted, as shown here:

```
```cpp
for (;;)
{
  // Statements that do something...
  // ... and include some way of ending the loop
}
```
```

You still need the semicolons (;), even though no loop control expressions exist. The only way this loop can end is if some code within the loop terminates it. You can have an indefinite while loop, too:

```
```cpp
while (true)
{
  // Statements that do something...
  // ... and include some way of ending the loop
}
```
```

The loop condition is always true, so you have an indefinite loop. This is equivalent to the for loop with no control expressions. Of course, you can also have a version of the do-while loop that is indefinite, but it is not normally used because it has no advantages over the other two types of loop.

The obvious way to end an indefinite loop is to use the break statement. You could have used an indefinite loop in Ex5_07.cpp to allow several tries at entering a valid table size, instead of ending the program immediately. This loop would do it:

```
```cpp
const size_t max_tries {3};   // Max. number of times a user can try entering a table size
do
{
  for (size_t count {1}; ; ++count)  // Indefinite loop
  {
    std::cout <<
      std::format("What size table would you like ({} to {})? ", table_min, table_max);
    std::cin >> table;  // Get the table size

    // Make sure table size is within the limits
    if (table >= table_min && table <= table_max)
    {
      break;        // Exit the input loop
    }
    else if (count < max_tries)
    {
      std::cout << "Invalid input - try again.\n";
    }
    else
    {
      std::cout << "Invalid table size entered - yet again!\nSorry, only "
        << max_tries << " allowed - program terminated." << std::endl;
      return 1;
    }
  }
  ...
}
```
```