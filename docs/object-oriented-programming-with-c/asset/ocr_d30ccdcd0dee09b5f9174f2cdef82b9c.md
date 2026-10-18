# cout <<item1<<item2 <<....<<itemN

The items _item1_through _itemN_may be variables or constants of any basic type. We have used such statements in a number of examples illustrated in previous chapters.

# put() and get() Functions

The classes _istream_ and _ostream_ define two member functions _get_() and _put_() respectively to handle the single character input/output operations . There are two types of _get_() functions. We can use both _get_(char _⋆_) and _get_(void) prototypes to fetch a character including the blank space, tab and the newline character. The _get_(char _⋆_) version assigns the input character to its argument and the _get_(void) version returns the input character.

Since these functions are members of the input/output stream classes, we must invoke them using an appropriate object.

# Example:

```
char c;
cin.get(c); // get a character from keyboard
// and assign it to c
while(c != '\n')
{
cout << c; // display the character on screen
cin.get(c); // get another character
}
```

This code reads and displays a line of text (terminated by a newline character). Remember, the operator >> can also be used to read a character but it will skip the white spaces and newline character. The above while loop will not work properly if the statement

```
cin >> c;
```