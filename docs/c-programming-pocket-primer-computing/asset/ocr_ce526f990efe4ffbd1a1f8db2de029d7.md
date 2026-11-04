```
```
  }
}
```
```

Listing 5.6 starts with a character-based pointer `str` that points to a string of characters. Recall the discussion about character strings earlier in this chapter: assigning the dereferenced value of a pointer to a character string is a legitimate way to initialize a character pointer.

The next part of Listing 5.6 contains a pair of nested loops. As the outer loop iterates through each of the characters in the string referenced by `str`, the inner loop iterates through all the characters in the string `str` that precede (and include) the current character.

Listing 5.6 introduces the C built-in function `strlen()` that returns the length of a string. The output from Listing 5.6 is here:

```
```
1: t
2: th
3: thi
4: this
5: thisi
6: thisis
7: thisisa
8: thisisal
9: thisisalo
10: thisisalon
11: thisisalong
12: thisisalongs
13: thisisalongst
14: thisisalongstr
15: thisisalongstri
16: thisisalongstrin
17: thisisalongstring
```
```