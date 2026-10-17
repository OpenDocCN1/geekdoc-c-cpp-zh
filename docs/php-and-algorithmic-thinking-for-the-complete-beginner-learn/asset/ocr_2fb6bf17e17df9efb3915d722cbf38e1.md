Keep in mind that in computer programming languages other than PHP, such as Visual Basic, Pascal, and Delphi (to name a few), you can do this type of conversion, but only under certain circumstances. The general form of the post-test loop structure, in which conversion can actually be carried out in the majority of the programming languages, is given next.

# Post-Test Loop Structure

```
counter = initial_value;
do {
    A statement or block of statements 1
    counter = counter OP2 offset;
    A statement or block of statements 2
} while (counter OP3 final_valuel);
```

# Pre-Test Loop Structure

```
counter = initial_value;
A statement or block of statements 1
counter = counter OP2 offset;
A statement or block of statements 2
while (counter OP3 final_valuel) {
    A statement or block of statements 1
    counter = counter OP2 offset;
    A statement or block of statements 2
}
```

# Counted Loop Structure

```
counter = initial_value;
A statement or block of statements 1
counter = counter OP2 offset;
A statement or block of statements 2
for (counter = initial_value OP2 offset;
    counter OP1 final_value2;
    counter = counter OP2 offset) {
    A statement or block of statements 1
    A statement or block of statements 2
}
```