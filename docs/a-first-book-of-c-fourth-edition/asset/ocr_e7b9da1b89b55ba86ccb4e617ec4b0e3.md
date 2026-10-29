# Point of Information

# Nesting try Blocks (continued)

```
} // end of outer try block
catch (string in) // catch for outer try block
{
    cout << "The input file " << in
         << " was not successfully opened." << endl
         << " No backup was made." << endl;
    exit(1);
}

cout << "A successful backup of " << fileOne
     << " named " << fileTwo << "was made." << endl;

return 0;
}
```

The important point to notice is nesting the try blocks. If the two try blocks aren’t nested and the input stream declaration, ifstream infile;, is placed in the first block, it can’t be used in the second try block without producing a compiler error. The reason is that all variables declared in a block of code (defined by an opening and closing brace pair) are local to the block in which they’re declared.

are necessary to make sure a value is read and then assigned to the variable ch before the retrieved value is compared with the EOF value. Without parentheses, the complete expression would be ch = inFile.get()!= EOF. Given the precedence of operations, the relational expression inFile.get()!= EOF would be executed first. Because it’s a relational expression, its result is a Boolean true or false value based on the data the get() method retrieves. Attempting to assign this Boolean result to the character variable ch is an invalid conversion across an assignment operator.

# EXERCISES 14.4

+   1. (Practice) List two conditions that cause a fail condition when a file is opened for input.

+   2. (Practice) List two conditions that cause a fail condition when a file is opened for output.

+   3. (Practice) If an existing file is opened for output in write mode, what happens to the data currently in the file?

+   4. (Modify) Modify Program 14.15 to use an identifier of your choice, in place of the letter e, for the catch block’s exception parameter name.