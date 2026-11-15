**TABLE 7.1 Operator Precedence**

| Precedence | Operation | Associativity |
|---|---|---|
| 1 | ( ) [ ] | innermost first |
| 2 | ++ -- + - ! (type) | right to left (unary) |
| 3 | * / % | left to right |
| 4 | + - | left to right |
| 5 | << >> | left to right |
| 6 | < <= > >= | left to right |
| 7 | == != | left to right |
| 8 | && | left to right |
| 9 | || | left to right |
| 10 | ?: | right to left |
| 10 | = += -= *= /= %= | right to left |
| 11 | , | left to right |

# ## Practice!

Assume that the array `s` has been defined with the following statement:
`int s[]={3, 8, 15, 21, 30, 41};`
Determine, by hand, the output for each of the following sets of statements:

```
1. for (int k=0; k<=5; k+=2)
   {
      cout << s[k] << ' ' << s[k+1] << endl;
   }
```

```
2. for (int k=0; k<=5; k++)
   {
      if (s[k]%2 == 0)
         cout << s[k] << ' ';
   }
   cout << endl;
```

# ## Function Arguments

When the information in an array is passed to a function, two parameters are usually used; one parameter specifies the specific array and the other parameter specifies the number of elements used in the array. By specifying the number of elements of the array that are to be used, the function becomes more flexible. For example, if the function specifies an integer array, then the function can be used with any integer array; the parameter that specifies the