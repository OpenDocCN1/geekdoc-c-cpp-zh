# 12.16 Substituting Strings or Words

The two functions in this chapter are TRANSL and TRANWRD. TRANSL allows you to substitute one character value for another. TRANWRD lets you substitute one word for another (hence the name, translate word—TRANWRD).

In this first example, you want to substitute the values A, B, C, D, and E for the character values 1, 2, 3, 4, and 5.

# Program 12.16: Demonstrating the TRANSLATE function

```
data Trans;
  input Answer : $5;
  Answer = translate(Answer,'ABCDE','12345');
datalines;
14325
AB123
51492
;
```

The resulting data set Trans contains the following three observations:

# Figure 12.18: Listing of Data Set Trans

| Listing of Data Set Trans |
| Answer |
| ABCDE |
| ABABC |
| EAD9B |

The values 1–5 are replaced by A–E. Any other characters are not changed. The translate function takes three arguments: the first argument is the character string you want to change; the second and third arguments are the to-string and the from-string. Each character in the to-string is substituted for the corresponding character in the from-string. In the program above, a 1 becomes an A, a 2 becomes a B, and so forth.

The last function in this chapter (hurray!) is TRANWRD. This function lets you substitute one word for another.