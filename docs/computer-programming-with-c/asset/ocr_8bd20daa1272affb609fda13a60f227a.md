# 6.5  **2D Array of Characters**

Similar to any other 2D array, we can also create a 2D array of characters. For example, the statement

```
char a[3][4];
```

creates a 2D array of characters with 3 rows and 4 columns. The array can be initialized character by character as shown in Figure 6.36. Note that we have stored NULL character `\0` in each of the rows explicitly because C/C++ does not add `\0` automatically in the case of character-by-character initialization.

![](bbox=[0.151, 0.323, 0.593, 0.525])

**Figure 6.36:** Character-by-character initialization of a 2D array

As explained in section 6.3, an array of characters is also called a **string** when it is terminated by `\0`. The advantage of strings is that we can perform direct input and output operations with strings. As seen in Figure 6.36, each row in the 2D array is terminated by `\0` and hence we can view a 2D array as an array storing 3 strings (instead of viewing it as an array of 12 different characters).

Let us compare the structure in Figure 6.36 with a single 1D array of characters. The statement

```
char b[4] = "rat";
```

creates a 1D array named b and stores a string rat in it as shown in Figure 6.37.

Due to the presence of NULL character, we can directly print the string b using the statement

```
printf("%s",b);
```

![](bbox=[0.715, 0.825, 0.881, 0.916])

**Figure 6.37:** String stored in 1D array named b

The 2D array specified in Figure 6.36 can actually be viewed as three different 1D arrays of characters, such that each 1D array contains one string. The next question is: what are the names of these individual 1D arrays? We know that when a row index as