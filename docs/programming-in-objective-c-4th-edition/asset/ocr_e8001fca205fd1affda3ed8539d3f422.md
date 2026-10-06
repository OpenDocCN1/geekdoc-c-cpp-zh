that follows an else could be any valid Objective-C program statement, so why not another if? Thus, in the general case, you could write the following:

```
if ( expression 1 )
  program statement 1
else
  if ( expression 2 )
    program statement 2
  else
    program statement 3
```

This effectively extends the if statement from a two-valued logic decision to a three-valued logic decision. You can continue to add if statements to the else clauses, in the manner just shown, to effectively extend the decision to an n-valued logic decision.

The preceding construct is so frequently used that it is generally referred to as an else if construct and is usually formatted differently from that shown previously:

```
if ( expression 1 )
  program statement 1
else if ( expression 2 )
  program statement 2
else
  program statement 3
```

This latter method of formatting improves the readability of the statement and makes it clearer that a three-way decision is being made.

The next program illustrates the use of the else if construct by implementing the sign function discussed earlier.

# Program 6.6