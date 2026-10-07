# LESSON 16 Pointers to Functions and Linked Lists

```
48: void void two(void)
49: {
50:   puts("You entered 2.");
51: }
52: 
53: void other other(void)
54: {
55:   puts("You entered something other than 1 or 2.");
56: }
```

# Output ▼

Enter an integer between 1 and 10, 0 to exit:
2 You entered 2.

Enter an integer between 1 and 10, 0 to exit:
11 You entered something other than 1 or 2.

Enter an integer between 1 and 10, 0 to exit:
0

# Analysis ▼

Notice the differences between Listing 16.2 and Listing 16.3. The declaration of the pointer to a function has been moved to line 17 in main(), where it is needed. Code in main() now initializes the pointer to point to the correct function, depending on the value the user entered (lines 25 through 32), and then passes the initialized pointer to func1(). func1() serves no purpose in Listing 16.3; all it does is call the function pointed by ptr. Again, this program is for illustration purposes. The same principles can be used in real-world programs, as the example in the next section.

One programming situation in which you might use pointers functions is one in which sorting is required. For example, you might want to sort in alphabetical order one time and in reverse alphabetical order another time. By using pointers to functions, your program can call the correct sorting function. More precisely, it's usually a different comparison function's called.

Look back at Listing 15.7 in the last lesson. In the sort() function, the actual sort order is determined by the value returned by the strcmp() library function, which tells the program whether a given string is "less than" or "greater than". If you write two comparison functions—one that sorts alphabetically (where A is less than Z), and another that sorts in reverse alphabetical order (where Z is less than A)?