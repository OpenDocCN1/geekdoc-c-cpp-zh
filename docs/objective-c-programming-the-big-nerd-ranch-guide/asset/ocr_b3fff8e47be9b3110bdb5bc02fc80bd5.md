# ## Getting the data at an address

If you have an address, you can get the data stored there using the * operator. Have the log display the value of the integer stored at `addressOfI`.

```
```
int main(int argc, const char * argv[])
{
    int i = 17;
    int *addressOfI = &i;
    printf("i stores its value at @%p\n", addressOfI);
    printf("this function starts at @%p\n", main);
    printf("the int stored at addressOfI is %d\n", *addressOfI);
    return 0;
}
```
```

Notice that the asterisk is used two different ways The first is in the declaration where you declare the variable `addressOfI` to be an int *. That is, it is a pointer to a place where an int can be stored.

The second is where you read the int value that is stored at the address stored in `addressOfI`. (Pointers are also called references. Thus, using the pointer to read data at the address is sometimes called *dereferencing* the pointer.)

You can also use the * operator on the left-hand side of an assignment to store data at a particular address:

```
```
int main(int argc, const char * argv[])
{
    int i = 17;
    int *addressOfI = &i;
    printf("i stores its value at @%p\n", addressOfI);
    *addressOfI = 89;
    printf("Now i is %d\n", i);
    return 0;
}
```
```

Build and run your program.

Don’t worry if you don’t have pointers squared away in your mind just yet. We’ll spend a lot of time working with pointers in this book, so you’ll get plenty of practice.

Now let’s make a common programming mistake. Remove the * from the fourth line of `main()` so that it reads

```
```
addressOfI = 89;
```
```

Notice Xcode pops up a warning that says Incompatible integer to pointer conversion assigning to ‘int *’ to ‘int’. Fix the problem.

# ## How many bytes?

Given that everything lives in memory and that you now know how to find the address where data starts, the next question is “How many bytes does this data type consume?”

Using `sizeof()` you can find the size of a data type. For example,