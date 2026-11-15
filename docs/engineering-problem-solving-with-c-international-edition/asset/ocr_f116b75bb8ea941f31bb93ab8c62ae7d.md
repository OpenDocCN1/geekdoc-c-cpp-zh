```
/* Count the number of occurrences of short_str in long_str. */
/* While the function strstr does not return NULL, increment */
/* count and move ptr1 to next character of the long string. */
while ((ptr1=strstr(ptr1,ptr2)) != NULL)
{
    printf("location %i \\n",ptr1-long_str+1);
    count++;
    ptr1++;
}

/* Print number of occurrences. */
printf("number of occurrences: %i \\n",count);

/* Exit program. */
return 0;
}
/*----------------------------------------------------------*\/
```

# ## 5. TESTING

We first test the program with the data from the hand example. This generates the following interaction:

location 3
location 18
location 24
number of occurrences: 3

The answer matches the hand example, so we can now test the program with additional points.

# # MODIFY!

These problems relate to the program developed in this section for finding short strings in longer strings.

+   1. Modify the program so that it prints the long string and the short string.
+   2. Modify the program so that it allows the user to enter the long string and the short string.
+   3. Modify the program so that the long string is read from a data file and the short string is input from the user.
+   4. Modify the program so that it will work with either lowercase or uppercase characters.
+   5. Modify the program so that it checks to be sure that the length of the short string is less than the length of the long string.