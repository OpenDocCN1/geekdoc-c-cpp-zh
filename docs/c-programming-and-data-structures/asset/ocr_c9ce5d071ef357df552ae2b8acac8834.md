```
while (i < ITEMS)
    scanf("%s", string[i++]);
/* Sorting begins */
for (i=1; i < ITEMS; i++) /* Outer loop begins */
{
    for (j=i; j < ITEMS - i; j++) /*Inner loop begins*/
    {
        if (strcmp (string[j-1], string[j]) > 0)
        { /* Exchange of contents */
            strcpy (dummy, string[i-1]);
            strcpy (string[j-1], string[j]);
            strcpy (string[j], dummy);
        }
    } /* Inner loop ends */
} /* Outer loop ends */
/* Sorting completed */
printf ("\nAlphabetical list \n\n");
for (i=0; i < ITEMS ; i++)
    printf ("%s", string[i]);
}
Output
Enter names of 5 items
London Manchester Delhi Paris Moscow
Alphabetical list
Delhi
London
Manchester
Moscow
Paris
```

Fig. 4.10 Sorting of strings in alphabetical order

Note that a two-dimensional array is used to store the list of strings. Each string is read using a scanf function with %s format. Remember, if any string contains a white space, then the part of the string after the white space will be treated as another item in the list by the scanf. In such cases, we should read the entire line as a string using a suitable algorithm. For example, we can use gets function to read a line of text containing a series of words. We may also use puts function in place of scanf for output.

# 4.10 OTHER FEATURES OF STRINGS

Other aspects of strings we have not discussed in this chapter include:

+   - Manipulating strings using pointers.
+   - Using string as function parameters.
+   - Declaring and defining strings as members of structures.

These topics will be dealt with later when we discuss functions, structures and pointers.

# 4.11 DECISION MAKING AND LOOPING

We have seen in the previous chapter that it is possible to execute a segment of a program repeatedly by introducing a counter and later testing it using the if statement. While this method is quite satisfactory for all