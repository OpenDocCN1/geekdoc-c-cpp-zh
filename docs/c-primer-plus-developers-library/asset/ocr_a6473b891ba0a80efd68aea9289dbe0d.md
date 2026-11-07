# **Program Notes**

The following is the input part of the program in Listing 6.5:

```

    cin >> temp;
    while (i < ArSize && temp >= 0) // 2 quitting criteria
    {
        naaq[i] = temp;
        ++i;
        if (i < ArSize)            // room left in the array,
        {
            cout << "Next value: ";
            cin >> temp;           // so get next value
        }
    }
```

The program begins by reading the first input value into a temporary variable called *temp*. Then the *while* test condition checks whether there is still room left in the array (*i* < *ArSize*) and whether the input value is non-negative (*temp* >= 0). If it is, the program copies the *temp* value to the array and increases the array index by one. At that point, because array numbering starts at zero, *i* equals the total number of entries to date. That is, if *i* starts out at 0, the first cycle through the loop assigns a value to *naaq[0]* and then sets *i* to 1.

The loop terminates when the array is filled or when the user enters a negative number. Note that the loop reads another value into *temp* only if *i* is less than *ArSize*—that is, only if there is still room left in the array.

After it gets data, the program uses an *if else* statement to comment if no data was entered (that is, if the first entry was a negative number) and to process the data if any is present.

# **Setting Up Ranges with &&**

The && operator also lets you set up a series of *if else if else* statements, with each choice corresponding to a particular range of values. Listing 6.6 illustrates the approach. It also shows a useful technique for handling a series of messages. Just as a pointer-to-char variable can identify a single string by pointing to its beginning, an array of pointers-to-char can identify a series of strings. You simply assign the address of each string to a different array element. Listing 6.6 uses the *qualify* array to hold the addresses of four strings. For example, *qualify[1]* holds the address of the string "must tug-of-war\n". The program can then use *qualify[1]* as it would any other pointer to a string—for example, with *cout* or with *strlen()* or *strcmp()*. Using the *const* qualifier protects these strings from accidental alterations.