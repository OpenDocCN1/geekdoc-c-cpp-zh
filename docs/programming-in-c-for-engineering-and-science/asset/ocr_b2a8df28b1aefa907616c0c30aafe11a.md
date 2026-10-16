we must remember that these increment expressions are assignment expressions and thus produce values. They both increment a variable, but the value produced by the postfix form is the original (nonincremented) value of the variable, whereas that produced by the prefix form is the incremented value.

To illustrate this, consider the following program segments where, as before, count and number are integer variables:

```
//POSTFIX: Use first, then increment
count = 10;
cout << "count =" << count << endl;
```

Output

count = 10

```
number = count++;
cout << "number =" << number << endl;
cout << "count =" << count << endl;
```

number = 10
count = 11

and

```
//PREFIX: Increment first, then use
count = 10;
cout << "count =" << count << endl;
```

Output

count = 10

```
number = ++count;
cout << "number =" << number << endl;
cout << "count =" << count << endl;
```

number = 11
count = 11

Note that both sets of statements increment the value of count from 10 to 11. However, in the first set of assignments, number is assigned the value 10, but in the second set, number is assigned the value 11.

Just as an integer variable’s value can be incremented with the ++ operator, it can be decremented (i.e., 1 is subtracted from it) by using the decrement operator (--). For example, the assignment statement

```
count = count - 1;
```

can be written more compactly as

```
count--;
```

or

```
--count;
```

The differences between the prefix and postfix versions are similar to those for the increment operator.